---
title: Google Analytics y atribución de UTM
description: Obtenga información acerca del proceso de atribución de origen de Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] Atribución de y UTM

Es fundamental para [origen de adquisición de usuario de seguimiento](../../data-analyst/analysis/google-track-user-acq.md) hasta [identificar las campañas publicitarias con mejor rendimiento](../../data-analyst/analysis/most-value-source-channel.md). En este tema se exploran las [!DNL Google Analytics] proceso de atribución de origen. En otras palabras, qué parte de la información se registra cuando.

## ¿Qué es la atribución?

`Attribution` se trata de especificar una fuente de referencia de una actividad concreta. Estas actividades suelen ser macro-conversiones o micro-conversiones, siendo las macro cosas como **compras**, microser cosas como **registro, registro por correo electrónico, comentario en el blog,** y demás.

Lo ideal es que, cada vez que se produzca un evento de conversión, se registre un origen de referencia. Pero, ¿cómo se determina la fuente?

La realidad es que los usuarios a menudo vienen de muchas fuentes antes de golpear / cometer una conversión micro o macro. Por ejemplo, pueden llegar al sitio a través de la información orgánica, luego salir, luego venir a través de la búsqueda de pago, luego salir y luego venir directamente al sitio en sí. Esta información de seguimiento de la fuente se proporciona a menudo al sitio a través de parámetros de UTM, pero también hay sistemas más sofisticados. Para sus fines, céntrese en [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## ¿Cómo? [!DNL Google Analytics] ¿atribuir fuentes de referencia a través de parámetros UTM?

Cuando se especifican los parámetros de UTM en la dirección URL, estos se analizan y se colocan en una [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un sitio web no tiene [!DNL Google Analytics]Sin embargo, no tiene sentido tener UTM. [!DNL Google Analytics] tiene reglas para el tratamiento de un usuario que visita varias URL con UTM durante su vida útil (más información más adelante). Suponiendo que el sitio web está configurado para capturar parámetros de UTM en una base de datos externa, cuando se produce una conversión micro o macro, lo que esté en la [!DNL Google Analytics] La cookie en el momento de la conversión se replica en la base de datos.

## Primer clic frente a último clic

### Atribución de último clic

La atribución de último clic es el modelo de atribución más común empleado por [!DNL Google Analytics]. En este caso, la variable [!DNL Google Analytics] La cookie representa los parámetros de UTM del origen más reciente antes del evento de conversión y este es [registrado en la base de datos](../../data-analyst/analysis/google-track-user-acq.md). El [!DNL Google Analytics] La cookie solo sobrescribe los parámetros de UTM anteriores si el usuario hace clic en una nueva dirección URL que contiene un nuevo conjunto de parámetros de UTM.

Por ejemplo, piense en un usuario que visita por primera vez un sitio web a través de [!DNL Google Analytics] *búsqueda de pago* y, a continuación, devuelve mediante *búsqueda orgánica*, y finalmente regresa al *sitio web directamente* o a través de un *vínculo de correo electrónico* **sin parámetros de UTM** antes del evento de conversión. En este ejemplo, la variable [!DNL Google Analytics] La cookie indica que la fuente del usuario es orgánica, ya que representa la última fuente antes de la conversión. El *ruta* del usuario antes de que se ignore el evento de conversión final. Si, en su lugar, el usuario visitó el sitio web desde un vínculo de correo electrónico con UTM, la variable [!DNL Google Analytics] La cookie diría que la fuente es &quot;correo electrónico&quot;. Por lo tanto, si hay parámetros de UTM existentes en la cookie y el usuario entra mediante un vínculo directo, la variable [!DNL Google Analytics] La cookie muestra los parámetros de UTM en lugar de &quot;directos&quot;.

>[!NOTE]
>
>El nombre de un usuario específico [!DNL Google Analytics] Los parámetros de cookies se borran al configurar la cookie [caduca](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)o cuando un usuario borra sus cookies en el explorador.*

### Atribución del primer clic

Algunas herramientas de atribución de pago le permiten capturar &quot;la pila de tortitas&quot; de fuentes en la ruta de un usuario. En ese caso, en el ejemplo anterior, la atribución del primer clic nos diría que la búsqueda de pago. Como alternativa, algunos sitios web implementan sus propias cookies que capturan una pila de panqueques y almacenan la primera fuente en su base de datos.

## ¿Cómo analizar la atribución?

[!DNL Google Analytics] tiene una funcionalidad sólida en su interfaz web que le permite realizar cuatro modelos de atribución diferentes:

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

* [Rastrear origen de referencia de pedido mediante [!DNL Google Analytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../analysis/google-track-user-acq.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../analysis/roi-ad-camp.md)
* [Cinco prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
