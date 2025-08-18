---
title: Atribución de Google Analytics y UTM
description: Obtenga información acerca del proceso de atribución de origen de Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Atribución de [!DNL Google Analytics] y UTM

Es fundamental para [rastrear el origen de adquisición de usuarios](../../data-analyst/analysis/google-track-user-acq.md) para [identificar las campañas publicitarias con mejor rendimiento](../../data-analyst/analysis/most-value-source-channel.md). En este tema se explora el proceso de atribución de origen de [!DNL Google Analytics]. En otras palabras, qué parte de la información se registra cuando.

## ¿Qué es la atribución?

`Attribution` trata de especificar un origen de referencia de una actividad en particular. Estas actividades suelen ser conversiones o microconversiones, ya que las macros son cosas como **compras**, las micro son cosas como **registro, registro por correo electrónico, comentario en el blog**, etc.

Lo ideal es que, cada vez que se produzca un evento de conversión, se registre un origen de referencia. Pero, ¿cómo se determina la fuente?

La realidad es que los usuarios a menudo vienen de muchas fuentes antes de golpear / cometer una conversión micro o macro. Por ejemplo, pueden llegar al sitio a través de la información orgánica, luego salir, luego venir a través de la búsqueda de pago, luego salir y luego venir directamente al sitio en sí. Esta información de seguimiento de la fuente se proporciona a menudo al sitio a través de parámetros de UTM, pero también hay sistemas más sofisticados. Para tus propósitos, céntrate en [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## ¿Cómo atribuye [!DNL Google Analytics] fuentes de referencia a través de parámetros de UTM?

Cuando se especifican los parámetros de UTM en la dirección URL, estos se analizan y se colocan en una [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un sitio web no tiene [!DNL Google Analytics], no tiene sentido tener UTM. [!DNL Google Analytics] tiene reglas para tratar con un usuario que visita varias URL con UTM durante su vida útil (más información más adelante). Suponiendo que el sitio web está configurado para capturar parámetros de UTM en una base de datos externa, cuando se produce una conversión micro o macro, lo que esté en la cookie [!DNL Google Analytics] en el momento de la conversión se replica en la base de datos.

## Primer clic frente a último clic

### Atribución de último clic

La atribución de último clic es el modelo de atribución más común empleado por [!DNL Google Analytics]. En este caso, la cookie [!DNL Google Analytics] representa los parámetros de UTM para el origen más reciente antes del evento de conversión, y esto es [registrado en la base de datos](../../data-analyst/analysis/google-track-user-acq.md). La cookie [!DNL Google Analytics] solo sobrescribe los parámetros de UTM anteriores si el usuario hace clic en una nueva dirección URL que contiene un nuevo conjunto de parámetros de UTM.

Por ejemplo, piense en un usuario que visita por primera vez un sitio web a través de [!DNL Google Analytics] *búsqueda de pago*, luego regresa a través de *búsqueda orgánica* y finalmente regresa al *sitio web directamente* o a través de un *vínculo de correo electrónico* **sin parámetros de UTM** antes del evento de conversión. En este ejemplo, la cookie [!DNL Google Analytics] indica que el origen del usuario es orgánico, ya que representa el último origen antes de la conversión. La *ruta* del usuario antes de ese evento de conversión final se omite. Si, en cambio, el usuario visitó el sitio web desde un vínculo de correo electrónico con UTM, la cookie [!DNL Google Analytics] diría que el origen es &quot;correo electrónico&quot;. Por lo tanto, si hay parámetros de UTM existentes en la cookie y el usuario entra mediante comunicación directa, la cookie [!DNL Google Analytics] muestra los parámetros de UTM en lugar de &quot;directa&quot;.

>[!NOTE]
>
>Los parámetros de cookie [!DNL Google Analytics] de un usuario específico se borran cuando la cookie [caduca](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage), o cuando un usuario borra sus cookies en el explorador.*

### Atribución del primer clic

Algunas herramientas de atribución de pago le permiten capturar &quot;la pila de tortitas&quot; de fuentes en la ruta de un usuario. En ese caso, en el ejemplo anterior, la atribución del primer clic nos diría que la búsqueda de pago. Como alternativa, algunos sitios web implementan sus propias cookies que capturan una pila de panqueques y almacenan la primera fuente en su base de datos.

## ¿Cómo analizar la atribución?

[!DNL Google Analytics] tiene algunas funciones sólidas en su interfaz web que le permiten realizar cuatro modelos de atribución diferentes:

1. primer clic
1. último clic
1. lineal (divida los ingresos equitativamente entre todas las fuentes de la ruta)
1. ponderado (atribución personalizada)

Ahora que comprende cuál es el modelo de atribución para cada micro o macro-conversión, la pregunta es &quot;¿Qué hace con la totalidad de las conversiones de un usuario?&quot;.  Por ejemplo, observe las UTM registradas en función de la lógica de último clic de GA:

* Los registros de usuario están bajo orgánico
* Primera compra del usuario en la búsqueda de pago: 5,00 $
* Segunda compra del usuario por correo electrónico: 50,00 $
* Tercera compra del usuario en 10,00 $ orgánicos

Aquí es donde se pregunta: &quot;¿Cuántos ingresos obtuve de la búsqueda de pago? ¿Del correo electrónico?  ¿De orgánica?&quot;. Podría decirse que las respuestas son 5, 50 y 10 (cualquiera que sea la última fuente), o también que atribuye todos los ingresos a la primera fuente (los 65 van a orgánica). También puede aplicar algún análisis ponderado o aplicar el modelo lineal (es decir, aproximadamente 22 cada uno).

## Documentación relacionada

* [Rastrear origen de referencia de pedidos a través de  [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../analysis/google-track-user-acq.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecta tu cuenta de  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../analysis/roi-ad-camp.md)
* [Cinco prácticas recomendadas para el etiquetado UTM en  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
