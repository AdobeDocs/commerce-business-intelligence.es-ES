---
title: Duplicación de canales de Google Analytics mediante fuentes de adquisición
description: Obtenga información sobre cómo duplicar canales de Google Analytics mediante fuentes de adquisición.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Google Analytics con fuentes de adquisición

## ¿Qué son los canales? {#channels}

La creación de segmentos personalizados para ver el rendimiento de los distintos flujos de tráfico y observar las tendencias es uno de los usos más potentes de  [!DNL Google Analytics ]. Una clase de segmentos que existen de forma predeterminada en [!DNL Google Analytics ] son `Channels`. Los canales son una agrupación de formas comunes en las que las personas llegan al sitio.  [!DNL Google Analytics ] ordena automáticamente las muchas formas en que adquiere un usuario, ya sean medios sociales, pago por clic, correo electrónico o vínculos de referencia, y los agrupa en un bloque o canal.

## ¿Por qué no veo mi `channels` ¿en MBI? {#nochannels}

`Channels` son bloques de datos simples y acumulados. Para ordenar las adquisiciones en bloques de canales, Google establece distintas reglas y definiciones utilizando parámetros específicos: una combinación de adquisiciones [Origen](https://support.google.com/analytics/answer/1033173?hl=en) (el origen de su tráfico) y adquisición [Mediana](https://support.google.com/analytics/answer/6099206?hl=en) (la categoría general de la fuente).

Aunque tener estos contenedores puede ayudarle a comprender de dónde proviene su tráfico, estos datos no están etiquetados por canal, sino por una combinación de Fuente y Medio. Dado que Google envía la información del canal como dos puntos de datos independientes, las agrupaciones de canales no se muestran automáticamente en [!DNL MBI].

## ¿Cuáles son las agrupaciones de canales predeterminadas? ¿Cómo se crean?

De forma predeterminada, Google le configura con ocho canales diferentes. Observe las reglas que determinan cómo se crean:

| Canal | ¿Qué pasa? | ¿Cómo se crea? |
|---|---|---|
| Directo | Cualquier persona que entre directamente en el sitio. | Origen = `Direct`<br>MEDIO AND = `(not set); OR Medium = (none)` |
| Búsqueda orgánica | Tráfico que se ha clasificado orgánicamente en motores de búsqueda no pagados. | Medio = `organic` |
| Referencia | Tráfico que llega desde un vínculo externo que no es búsqueda orgánica o desde sitios web que no son redes sociales. | Medio = `referral` |
| Búsqueda de pago | Tráfico que tiene un código de seguimiento de UTM en el que el medio es &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; Y es una red de distribución de publicidad que no coincide con &quot;Contenido&quot;. | Medio = `^(cpc|ppc|paidsearch)$`<br>≠ de red de distribución de publicidad AND `Content` |
| Social | Tráfico de referencia proveniente de cualquiera de las siguientes ubicaciones, aproximadamente [400 redes sociales](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) y no están etiquetados como anuncios. | Referencia de origen social = `Yes`<br>O Medio = `^(social|social-network|social-media|sm|social network|social media)$` |
| Correo electrónico | Tráfico de las sesiones etiquetadas con el medio &quot;correo electrónico&quot;. | Código de seguimiento UTM de medio = `email` |
| Mostrar | Tráfico que tiene un código de seguimiento UTM en el que el medio es display o cpm. También incluye la interacción AdWords donde la red de distribución de publicidad coincide con &quot;Contenido&quot; | Medio = `^(display|cpm|banner)$`<br>O Red de distribución de publicidad = `Content`<br>≠ de formato de anuncio AND `Text` |
| Otros | Sesiones de otros canales publicitarios (sin incluir la búsqueda de pago) etiquetados con un medio de &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliate&quot;. | Medio = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## ¿Cómo puedo recrear estas agrupaciones de canales en mi Data Warehouse? {#recreate}

Ahora que sabe que los canales son solo combinaciones de fuentes y medios, es un proceso fácil de 3 pasos recrear estas agrupaciones en su Data Warehouse.

1. **Habilite su[!DNL Google ECommerce]integración**

   [Una vez activado](../importing-data/integrations/google-ecommerce.md), asegúrese de lo siguiente [sincronizar](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) el **mediano** y **origen** campos en la Data Warehouse. Una vez finalizado, los datos de adquisición de medio y origen se incluirán en la Data Warehouse.

1. **Cargar una asignación de las agrupaciones de canales de Google**

   Para ahorrarle tiempo, Commerce ya ha creado una tabla con las agrupaciones predeterminadas asignadas como archivo que puede [descargar](../../assets/ga-channel-mapping.csv).

   Si es un profesional de los Google Analytics y ha creado sus propios canales, debe añadir las reglas específicas a la tabla de asignación antes de cargar el archivo en [!DNL MBI].

   Tráigalo a su Data Warehouse como [Carga de archivos](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Establezca una relación entre[!DNL Google ECommerce]Carga de archivos de asignaciones y**

   Para establecer una relación entre[!DNL Google ECommerce]y la tabla de asignación, [enviar una solicitud de asistencia](../../guide-overview.md) Consulte a su equipo de analistas de datos y consulte este artículo. El analista crea una nueva columna calculada llamada **Canal** en la tabla de ECommerce. **Después de un ciclo de actualización completo**, esta columna está lista para usarla en un filtro o agrupar por.

¡Felicitaciones! Ahora tiene las agrupaciones de canales de Google Analytics en la Data Warehouse, lo que significa que puede analizar los datos desde una nueva perspectiva:

![Segmentación de la métrica Número de pedidos por canal](../../assets/GA_Channel_Gif.gif)

En este ejemplo, ha iniciado simple: segmentar el **Número de pedidos** métrica por **Canal**. Ahora es su turno: pruebe su nueva columna y vea qué tendencias puede identificar en los datos del canal de Google Analytics.

## Documentación relacionada

* [Uso del Report Builder](../../tutorials/using-visual-report-builder.md)
* [Previsto[!DNL Google ECommerce]datos](../importing-data/integrations/google-ecommerce-data.md)
* [Edificio[!DNL Google ECommerce]dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [¿Cuáles son sus fuentes y canales de adquisición más valiosos?](../analysis/most-value-source-channel.md)
