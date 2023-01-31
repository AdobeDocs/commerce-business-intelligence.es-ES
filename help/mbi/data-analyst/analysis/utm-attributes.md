---
title: Atribución de Google Analytics y UTM
description: Obtenga información sobre el proceso de atribución de origen de Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Atribución de Google Analytics y UTM

Es fundamental [seguimiento del origen de adquisición de usuario](../../data-analyst/analysis/google-track-user-acq.md) a [identificar las campañas publicitarias de mejor rendimiento](../../data-analyst/analysis/most-value-source-channel.md). En este tutorial, exploramos el proceso de atribución de origen de Google Analytics. En otras palabras, qué información se registra cuando.

## ¿Qué es la atribución?

`Attribution` se trata de especificar una fuente de referente de una actividad en particular. Estas actividades son normalmente macroconversiones o microconversiones, siendo las macros cosas como **compras**, micro ser cosas como **registro, registro por correo electrónico, comentario de blog,** y así sucesivamente.

Lo ideal es que, cada vez que se produce un evento de conversión, se registre una fuente de referencia. Pero, ¿cómo se determina la fuente?

La realidad es que los usuarios a menudo vienen de muchas fuentes antes de visitar/cometer una microconversión o macro (por ejemplo, pueden llegar al sitio a través de orgánicas, luego irse, luego venir a través de búsquedas pagadas, luego irse, y luego venir directamente al sitio mismo). Esta información de seguimiento de fuentes se suele proporcionar al sitio a través de parámetros UTM, pero también hay sistemas más sofisticados. Para nuestros fines, nos centraremos en [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## ¿Cómo [!DNL Google Analytics] atributos fuentes de referencia a través de parámetros de UTM?

Cuando se especifican los parámetros de la UTM en la dirección URL, estos se analizan y se colocan en una [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Si un sitio web no tiene [!DNL Google Analytics], no tiene sentido tener UTM. [!DNL Google Analytics] tiene reglas sobre cómo trata con un usuario que visita varias URL con UTM durante su vida útil (más información más adelante). Suponiendo que el sitio web esté configurado para capturar parámetros UTM en una base de datos externa, siempre que se produzca una conversión de micro o macro, lo que esté en la variable [!DNL Google Analytics] en el momento de la conversión se replicaría en la base de datos.

## Primer clic frente a último clic

### Atribución de último clic

La atribución de último clic es el modelo de atribución más común empleado por [!DNL Google Analytics]. En este caso, la variable [!DNL Google Analytics] representa los parámetros de la UTM para la última fuente (o la más reciente) anterior al evento de conversión, y esto es lo que [registrado en la base de datos](../../data-analyst/analysis/google-track-user-acq.md). Tenga en cuenta que [!DNL Google Analytics] La cookie solo sobrescribe los parámetros anteriores de la UTM si el usuario hace clic en una nueva URL que contiene un nuevo conjunto de parámetros de la UTM.

Por ejemplo, supongamos que un usuario visita un sitio web por primera vez a través de [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *búsqueda de pago*, devuelve mediante *búsqueda orgánica* y finalmente vuelve al *sitio web directamente* o a través de una *vínculo de correo electrónico* **sin parámetros de UTM** antes del evento de conversión. En este ejemplo, la variable [!DNL Google Analytics] indica que el origen del usuario es orgánico, ya que representa el último origen antes de la conversión. La variable *ruta* del usuario antes de ese evento de conversión final se ignora. Si en su lugar el usuario visitó el sitio web desde un vínculo de correo electrónico con UTM, entonces la variable [!DNL Google Analytics] diría que la fuente es &quot;correo electrónico&quot;. Por lo tanto, si hay parámetros de UTM existentes en la cookie y el usuario ingresa directamente, la variable [!DNL Google Analytics] siempre mostrará los parámetros de la UTM en lugar de &quot;directo&quot;.

>[!NOTE]
>
>El informe de un usuario específico [!DNL Google Analytics] Los parámetros de cookie se borran cuando [caduca](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage), o cuando un usuario borra las cookies en el explorador.*)

### Atribución de primer clic

Algunas herramientas de atribución de pago le permiten capturar &quot;la pila de crepes&quot; de fuentes en la ruta del usuario. En esa situación, en nuestro ejemplo anterior, la atribución de primer clic nos indicaría una búsqueda paga. Alternativamente, una minoría de sitios web implementan sus propias cookies que capturan una pila de panqueques y almacenan la primera fuente en su base de datos.

## ¿Cómo se analiza la atribución?

[!DNL Google Analytics] tiene una funcionalidad más sólida en su interfaz web que permite realizar cuatro modelos de atribución diferentes: primer clic, último clic, lineal (divide los ingresos equitativamente entre todos los orígenes de la ruta) y ponderado (atribución personalizada).

Ahora que comprende cuál es el modelo de atribución para cada microconversión o macro conversión, la pregunta es ¿qué hacer con la totalidad de las conversiones de un usuario?  Por ejemplo, observe los UTM registrados en función de la lógica de último clic de GA:

* Registros de usuarios en el sistema orgánico
* Primera compra del usuario en búsqueda de pago $5.00
* Segunda compra del usuario por correo electrónico $50,00
* Tercera compra del usuario en orgánica $10.00

Aquí es donde se pregunta: ¿Cuántos ingresos obtuve de la búsqueda de pago?  ¿De correo electrónico?  ¿De orgánico?  Se podría decir que las respuestas son 5, 50 y 10 (es decir, cualquiera que sea la última fuente), o también se podría decir que se atribuyen todos los ingresos a la primera fuente (es decir, que los 65 van a lo orgánico). También puede aplicar análisis ponderados o aplicar el modelo lineal (es decir, aproximadamente 22 cada uno).

## Documentación relacionada

* [Rastrear la fuente de referencia de pedidos a través de [!DNL Google Analytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Seguimiento del origen de referencia del usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de datos de dispositivos de usuario, exploradores y sistemas operativos en la base de datos](../analysis/google-track-user-acq.md)
* [Descubra las fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumento del ROI en las campañas publicitarias](../analysis/roi-ad-camp.md)
* [5 prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
