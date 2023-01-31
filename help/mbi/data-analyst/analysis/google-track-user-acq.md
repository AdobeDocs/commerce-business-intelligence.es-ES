---
title: 'Google Analytics: información general sobre el seguimiento de la fuente de datos de adquisición de usuarios'
description: Obtenga información sobre cómo segmentar los datos por fuente de adquisición de usuario.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Segmentación por fuente de adquisición de usuario

>[!NOTE]
>
>El proceso siguiente no es compatible [!DNL GoogleUniversal Analytics].

La capacidad de segmentar los datos por fuente de adquisición de usuarios es fundamental para administrar eficazmente su plan de marketing. Conocer la fuente de adquisición de nuevos usuarios muestra qué canales arrojan los principales retornos y permite que su equipo asigne dólares de marketing con confianza.

Si todavía no está realizando el seguimiento de las fuentes de adquisición de usuarios en la base de datos, [!DNL MBI] puede ayudarle a empezar:

## Seguimiento de la fuente de adquisición de usuario

Recomendamos dos métodos para rastrear los datos de origen de referencia en función de su configuración:

### (Opción 1) Rastrear los datos de origen de la referencia de pedidos a través de [!DNL Google Analytics E-Commerce] (Incluido [!DNL Shopify] Almacenes)

Si aprovecha [!DNL Google Analytics E-Commerce] para realizar un seguimiento de los datos de pedidos y ventas, puede aprovechar nuestra [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) para sincronizar los datos de origen de referencia de cada pedido. Esto le permitirá segmentar los ingresos y los pedidos por fuente de referencia (por ejemplo, `utm_source` o `utm_medium`) y también obtener una idea de las fuentes de adquisición de clientes a través de [!DNL MBI] dimensiones personalizadas como `User's first order source`.

>[!NOTE]
>
>Para usuarios de Shopify**: Activar [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) antes de conectar su [!DNL Google Analytics E-Commerce] cuenta para [!DNL MBI].

### (Opción 2) Guardar [!DNL Google Analytics]&#39; datos de origen de adquisición en la base de datos

En este artículo explicaremos cómo guardar [!DNL Google Analytics] información del canal de adquisición en su propia base de datos, concretamente, la `source`, `medium`, `term`, `content`, `campaign`y `gclid` parámetros que estaban presentes en la primera visita de un usuario al sitio web. Para obtener una explicación de estos parámetros, consulte la [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). A continuación, exploraremos algunos de los poderosos análisis de marketing que se pueden realizar con esta información en [!DNL MBI].

#### ¿Por qué?

Si solo está viendo el valor predeterminado [!DNL Google Analytics] métricas de conversión y adquisición, no obtendrá la imagen completa. Aunque ver el número de conversiones de la búsqueda orgánica frente a la búsqueda paga es interesante, ¿qué se puede hacer con esa información? ¿Deberías gastar más dinero en búsquedas pagadas? Eso depende del valor de los clientes que provienen de ese canal, que no es algo que proporcione el Google Analytics.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) mitiga este problema almacenando datos de transacciones en [!DNL Google Analytics], pero esta solución no funciona para sitios que no sean de comercio electrónico, y algunas herramientas como el análisis de cohorte no son fáciles de hacer en la variable [!DNL Google Analytics] interfaz.

¿Qué sucede si desea enviar por correo electrónico una operación de seguimiento a todos los clientes adquiridos a partir de una campaña de correo electrónico determinada? ¿O integrar los datos de adquisición con su sistema CRM? Esto es imposible en [!DNL Google Analytics] - de hecho, va en contra de las Condiciones de servicio de [!DNL Google Analytics] para almacenar cualquier dato que identifique a un individuo.  Pero eso no significa que usted mismo no pueda almacenar estos datos.

#### El método

[!DNL Google Analytics] almacena la información de referencia de visitantes en una cookie denominada `__utmz`. Después de configurar esta cookie (mediante la variable [!DNL Google Analytics] código de seguimiento), su contenido se enviará con cada solicitud posterior a su dominio desde ese usuario. Así que en PHP, por ejemplo, se puede ver el contenido de `$_COOKIE['__utmz']` y verá una cadena que se parece a esta:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Está claro que hay algunos datos de fuentes de adquisición codificados en la cadena y hemos probado para confirmar que esta es la fuente de adquisición más reciente del visitante y los datos de campaña asociados. Ahora solo necesitamos saber cómo extraer los datos. Afortunadamente, Justin Cutroni ha descrito anteriormente cómo funciona esta codificación y ha compartido código javascript para extraer los bits clave de información.

Tomamos este código y lo traducimos en un [Biblioteca PHP alojada en github](https://github.com/RJMetrics/referral-grabber-php).   Para usar la biblioteca de , `include` una referencia a `ReferralGrabber.php` y luego llama a

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

El `$data` matriz será un mapa de las claves `source`, `medium`, `term`, `content`, `campaign`, `gclid` y sus valores respectivos.

Se recomienda añadir una nueva tabla a la base de datos llamada, por ejemplo, `user_referral`, con columnas como: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Cada vez que un usuario se registre, obtenga la información de referente y guárdela en esta tabla.

#### Cómo utilizar estos datos

Ahora que estamos guardando la fuente de adquisición de usuarios, ¿cómo podemos usarla?

Supongamos que estamos utilizando una base de datos SQL y tenemos una `users` con la siguiente estructura:

| ID | CORREO ELECTRÓNICO | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 24-01-2012 | google | orgánico |
| 2 | jim@abc.com | 24-01-2012 | google | cpc |
| 3 | joe@def.com | 25-01-2012 | direct | - |
| 4 | jess@ghi.com | 26-01-2012 | referente | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | other | orgánico |
| ... | ... | ... | ... | ... |

Para empezar, podemos contar la cantidad de usuarios que provienen de cada canal de referencia ejecutando la siguiente consulta en la base de datos:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

El resultado se parecerá a esto:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direct | 156 |
| referente | 55 |
| other | 16 |

Esto es interesante, pero de uso limitado. Lo que realmente nos gustaría saber es la tasa de crecimiento de estas cifras a lo largo del tiempo, la cantidad de ingresos generados por cada fuente de adquisición, una [análisis de cohorte](http://cohortanalysis.com/) de usuarios que provienen de cada fuente y la probabilidad de que un usuario de uno de estos canales vuelva como cliente en el futuro. Las consultas necesarias para realizar estos análisis son complejas, razón por la que creamos [!DNL MBI]. Con esta información podemos determinar nuestros canales de adquisición más rentables y enfocar nuestro tiempo y dinero de marketing en consecuencia.

### Relacionado

* **[Seguimiento de datos de dispositivos de usuario, exploradores y sistemas operativos en la base de datos](https://support.magento.com/hc/en-us/articles/360016732911)**
* **[Descubra las fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)**
* **[Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumento del ROI en las campañas publicitarias](../analysis/roi-ad-camp.md)**
* **[¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../analysis/utm-attributes.md)**
