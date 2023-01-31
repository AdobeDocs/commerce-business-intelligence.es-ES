---
title: Duplicación de canales de Google Analytics mediante fuentes de adquisición
description: Obtenga información sobre cómo duplicar canales de Google Analytics mediante fuentes de adquisición.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Google Analytics que utilizan fuentes de adquisición

## ¿Qué son los canales? {#channels}

Creación de segmentos personalizados para ver el rendimiento y el comportamiento del tráfico diferente y observar las tendencias (para mejor o peor) es uno de los usos más poderosos para  [!DNL Google Analytics ]. Una clase de segmentos que existen de forma predeterminada en [!DNL Google Analytics ] are `Channels`. Los canales son una agrupación de las formas comunes en que las personas llegan al sitio.  [!DNL Google Analytics ] ordena automáticamente las muchas formas en que adquiere un usuario, ya sea mediante medios sociales, pago por clic, correo electrónico o vínculos de referencia, y los agrupa en un bucket o un canal.

## ¿Por qué no veo mi `channels` en MBI? {#nochannels}

`Channels` son bloques de datos simples y agregados. Para ordenar las adquisiciones en bloques de canales, Google establece reglas y definiciones distintas utilizando parámetros específicos: una combinación de adquisición [Fuente](https://support.google.com/analytics/answer/1033173?hl=en) (el origen del tráfico) y la adquisición [Medio](https://support.google.com/analytics/answer/6099206?hl=en) (la categoría general de la fuente).

Aunque tener estos contenedores puede ayudarle a comprender de dónde proviene el tráfico, estos datos no están etiquetados por canal, sino por una combinación de Fuente y Medio. Como Google envía información de canal como dos puntos de datos independientes, las agrupaciones de canales no se muestran automáticamente en [!DNL MBI].

## ¿Cuáles son las agrupaciones de canales predeterminadas? ¿Cómo se crean?

De forma predeterminada, Google lo configura con 8 canales diferentes. Veamos las reglas que determinan cómo se crean:

| Canal | ¿Qué es? | ¿Cómo se crea? |
|---|---|---|
| Directas | Cualquiera que entre directamente en el sitio. | Origen = `Direct`<br>Y medio = `(not set); OR Medium = (none)` |
| Búsqueda orgánica | Tráfico que se ha clasificado orgánicamente en motores de búsqueda no pagados. | Medio = `organic` |
| Referencia | Tráfico que proviene de un vínculo externo que no es de búsqueda orgánica o de sitios web que no son redes sociales. | Medio = `referral` |
| Búsqueda de pago | Tráfico que tiene un código de seguimiento de UTM donde el medio es &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; Y es una red de distribución de anuncios que no coincide con &quot;Contenido&quot;. | Medio = `^(cpc|ppc|paidsearch)$`<br>AND Red de distribución de anuncios `Content` |
| Social | Tráfico de referencia que proviene de aproximadamente [400 redes sociales](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) y no están etiquetados como anuncios. | Remisión a la fuente social = `Yes`<br>O Medio = `^(social|social-network|social-media|sm|social network|social media)$` |
| Correo electrónico | Tráfico de sesiones etiquetadas con un medio de &quot;correo electrónico&quot;. | Código de seguimiento UTM de Medio = `email` |
| Mostrar | Tráfico que tiene un código de seguimiento de UTM en el que el medio es display o cpm. También incluye la interacción de AdWords en la que la red de distribución de anuncios coincide con &quot;Contenido&quot; | Medio = `^(display|cpm|banner)$`<br>O Red de distribución de anuncios = `Content`<br>Formato de anuncio AND `Text` |
| Otro | Sesiones de otros canales publicitarios, sin incluir Búsqueda paga, que están etiquetadas con un medio de &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliado&quot;. | Medio = `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## ¿Cómo puedo recrear estas agrupaciones de canales en mi Data Warehouse? {#recreate}

Ahora que sabe que los canales son solo combinaciones de fuentes y medios, es un proceso fácil de 3 pasos para recrear estas agrupaciones en su Data Warehouse.

1. **Active su[!DNL Google ECommerce]integración**

   [Una vez activada](../importing-data/integrations/google-ecommerce.md), asegúrese de [sincronizar](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) la **medium** y **source** en la Data Warehouse. Una vez completado este proceso, los datos de adquisición de fuentes y medios se introducirán en la Data Warehouse.

1. **Cargar una asignación de agrupaciones de canales de Google**

   Para ahorrar tiempo, Commerce ya ha creado una tabla con las agrupaciones predeterminadas asignadas como archivo que puede [descargar](../../assets/ga-channel-mapping.csv).

   Si es un profesional de los Google Analytics y ha creado sus propios canales, debe añadir las reglas específicas a la tabla de asignación antes de cargar el archivo en [!DNL MBI].

   Lleve esto a su Data Warehouse como un [Carga de archivo](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Establecer una relación entre[!DNL Google ECommerce]y carga de archivos de asignaciones**

   Para establecer una relación entre[!DNL Google ECommerce]y la tabla de asignación, [enviar una solicitud de asistencia](../../guide-overview.md) consulte nuestro equipo de analistas de datos y consulte este artículo. El analista creará una nueva columna calculada llamada **Canal** en la tabla ECommerce. **Después de un ciclo de actualización completo**, esta columna estará lista para usar en un filtro o en un grupo de por.

¡Felicidades! Ahora tiene agrupaciones de canales de Google Analytics en la Data Warehouse, lo que significa que puede analizar los datos desde una nueva perspectiva:

![Segmentación de la métrica Número de pedidos por canal](../../assets/GA_Channel_Gif.gif)

En este ejemplo, empezamos con la segmentación **Número de pedidos** métrica por **Canal**. Ahora es su turno - pruebe su nueva columna y vea las tendencias que puede identificar en sus datos de canal de Google Analytics!

## Documentación relacionada

* [Uso del Report Builder](../../tutorials/using-visual-report-builder.md)
* [Esperado[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [Creación[!DNL Google ECommerce]dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [¿Cuáles son sus fuentes y canales de adquisición más valiosos?](../analysis/most-value-source-channel.md)
