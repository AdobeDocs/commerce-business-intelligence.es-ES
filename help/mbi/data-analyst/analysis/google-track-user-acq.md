---
title: Google Analytics - Resumen de datos de fuentes de adquisición de usuarios de seguimiento
description: Obtenga información sobre cómo segmentar los datos por fuente de adquisición de usuarios.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: af1e3839839b4c419beabb0cc666c996ea2179d4
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# Segmentación por fuente de adquisición de usuario

>[!NOTE]
>
>El proceso siguiente no es compatible con [!DNL Google Universal Analytics].

La capacidad de segmentar los datos por fuente de adquisición de usuarios es crítica para administrar de forma eficaz el plan de marketing. Conocer la fuente de adquisición de nuevos usuarios muestra qué canales rinden los mayores beneficios y permite a su equipo asignar el dinero de marketing con confianza.

Si aún no está realizando el seguimiento de las fuentes de adquisición de usuarios en la base de datos, [!DNL Adobe Commerce Intelligence] puede ayudarle a empezar:

## Origen de adquisición de usuario de seguimiento

[!DNL Adobe] recomienda dos métodos para rastrear los datos de origen de referencia en función de su configuración:

### (Opción 1) Rastrear datos de origen de referencia de pedidos mediante [!DNL Google Analytics E-Commerce] (Incluyendo [!DNL Shopify] Stores)

Si utiliza [!DNL Google Analytics E-Commerce] para realizar un seguimiento de los datos de pedidos y ventas, puede utilizar la variable [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar los datos de origen de referencia de cada pedido. Esto le permite segmentar los ingresos y pedidos por fuente de referencia (por ejemplo, `utm_source` o `utm_medium`). También puede hacerse una idea de las fuentes de adquisición de clientes a través de [!DNL Commerce Intelligence] dimensiones personalizadas como `User's first order source`.

>[!NOTE]
>
>**Para usuarios de Shopify**: Activar [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) antes de conectar su [!DNL Google Analytics E-Commerce] cuenta a [!DNL Commerce Intelligence].

### (Opción 2) Guardar [!DNL Google Analytics]&#39; datos de origen de adquisición en la base de datos

Este tema explica cómo guardar [!DNL Google Analytics] información del canal de adquisición en su propia base de datos, concretamente, la `source`, `medium`, `term`, `content`, `campaign`, y `gclid` parámetros que estaban presentes en la primera visita de un usuario a su sitio web. Para ver una explicación de estos parámetros, consulte la [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). A continuación, explore algunos de los potentes análisis de marketing que se pueden realizar con esta información en [!DNL Commerce Intelligence].

#### ¿Por qué?

Si solo está viendo el valor predeterminado [!DNL Google Analytics] las métricas de conversión y adquisición, no se obtiene toda la imagen. Aunque ver el número de conversiones de la búsqueda orgánica frente a la búsqueda de pago es interesante, ¿qué puede hacer con esa información? ¿Debería gastar más dinero en búsquedas pagadas? Eso depende del valor de los clientes que provienen de ese canal, que no es algo que proporciona Google Analytics.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) mitiga este problema almacenando datos de transacción en [!DNL Google Analytics], pero esta solución no funciona para sitios que no sean de comercio electrónico. Además, ciertas herramientas como el análisis de cohorte no son fáciles de usar en [!DNL Google Analytics] interfaz.

¿Qué sucede si desea enviar por correo electrónico un acuerdo de seguimiento a todos los clientes adquiridos a partir de una determinada campaña de correo electrónico? ¿O integrar datos de adquisición con su sistema CRM? Esto es imposible en [!DNL Google Analytics] - de hecho, va en contra de los Términos de Servicio para [!DNL Google Analytics] para almacenar cualquier dato que identifique a un individuo. Sin embargo, puede almacenar estos datos usted mismo.

#### El método

[!DNL Google Analytics] almacena información de referencia de visitantes en una cookie llamada `__utmz`. Una vez establecida esta cookie (por el [!DNL Google Analytics] código de seguimiento), su contenido se envía con cada solicitud posterior de ese usuario a su dominio. Así, en PHP, por ejemplo, se puede ver el contenido de `$_COOKIE['__utmz']` y se vería una cadena con este aspecto:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Claramente hay algunos datos de fuente de adquisición codificados en la cadena. Esto se prueba para confirmar que es la última fuente de adquisición del visitante y los datos de campaña asociados. Ahora necesita saber cómo extraer los datos.

Este código se ha traducido en un [Biblioteca PHP alojada en github](https://github.com/RJMetrics/referral-grabber-php). Para utilizar la biblioteca, `include` una referencia a `ReferralGrabber.php` y luego llama a

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

El devuelto `$data` matriz es un mapa de las claves `source`, `medium`, `term`, `content`, `campaign`, `gclid`y sus valores respectivos.

[!DNL Adobe] recomienda agregar una tabla a la base de datos llamada, por ejemplo, `user_referral`, con columnas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Cada vez que un usuario se registre, obtenga la información de referencia y guárdela en esta tabla.

#### Cómo utilizar estos datos

Ahora que está guardando la fuente de adquisición de usuarios, ¿cómo puede utilizarla?

Supongamos que está utilizando una base de datos SQL y tiene un `users` con la siguiente estructura:

| ID | CORREO ELECTRÓNICO | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | orgánico |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | dirigir | - |
| 4 | jess@ghi.com | 2012-01-26 | referencia | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | otro | orgánico |
| ... | ... | ... | ... | ... |

Para empezar, puede contar el número de usuarios procedentes de cada canal de referencia ejecutando la siguiente consulta en la base de datos:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

El resultado tiene un aspecto similar al siguiente:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| dirigir | 156 |
| referencia | 55 |
| otro | 16 |

Esto es interesante, pero de uso limitado. Lo que realmente le gustaría saber es:

* la tasa de crecimiento de estas cifras con el tiempo
* el importe de los ingresos generados por cada fuente de adquisición
* a [análisis de cohorte](https://en.wikipedia.org/wiki/Cohort_analysis) de usuarios procedentes de cada origen
* la probabilidad de que un usuario de uno de estos canales vuelva como cliente en el futuro.

Las consultas necesarias para realizar estos análisis son complejas. Con esta información, puede determinar sus canales de adquisición más rentables y enfocar el tiempo y el dinero de marketing en consecuencia.

### Relacionado

* **[Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)**
* **[Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumente el retorno de la inversión en sus campañas publicitarias](../analysis/roi-ad-camp.md)**
* **[¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../analysis/utm-attributes.md)**
