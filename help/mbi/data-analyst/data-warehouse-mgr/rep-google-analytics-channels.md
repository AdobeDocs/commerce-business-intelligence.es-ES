---
title: Duplicación de canales de Google Analytics mediante fuentes de adquisición
description: Obtenga información sobre cómo duplicar canales de Google Analytics mediante fuentes de adquisición.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# [!DNL Google Analytics] mediante fuentes de adquisición

## ¿Qué son los canales? {#channels}

La creación de segmentos personalizados para ver el rendimiento del tráfico y las tendencias es uno de los usos más eficaces de [!DNL Google Analytics]. Una clase de segmentos que existe de forma predeterminada en [!DNL Google Analytics] es `Channels`. Los canales son una agrupación de formas comunes en las que las personas llegan al sitio.  [!DNL Google Analytics] ordena automáticamente las muchas formas en que adquiere a un usuario, ya sean los medios sociales, los vínculos de pago por clic, el correo electrónico o los vínculos de referencia, y los agrupa en un bloque o canal.

## ¿Por qué no veo mi `channels` en Commerce Intelligence? {#nochannels}

`Channels` son bloques simples y acumulados de datos. Para ordenar las adquisiciones en bloques de canales, [!DNL Google] establece distintas reglas y definiciones con parámetros específicos: una combinación de adquisición [Source](https://support.google.com/analytics/answer/1033173?hl=en) (el origen del tráfico) y adquisición [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (la categoría general del origen).

Aunque tener estos contenedores puede ayudarle a comprender de dónde proviene su tráfico, estos datos no están etiquetados por canal, sino por una combinación de Source y Medium. Dado que [!DNL Google] envía información de canal como dos puntos de datos independientes, las agrupaciones de canales no se muestran automáticamente en [!DNL Commerce Intelligence].

## ¿Cuáles son las agrupaciones de canales predeterminadas? ¿Cómo se crean?

De manera predeterminada, [!DNL Google] configura ocho canales diferentes. Las reglas que determinan cómo se crean los canales se describen a continuación.

| **Canal** | **¿Qué es?** | **¿Cómo se crea?** |
|---|---|---|
| Directo | Cualquier persona que entre directamente en el sitio. | Source = `Direct`<br> Y Medium = `(not set); OR Medium = (none)` |
| Búsqueda orgánica | Tráfico que se ha clasificado orgánicamente en motores de búsqueda no pagados. | Medium = `organic` |
| Referencia | Tráfico que llega desde un vínculo externo que no es búsqueda orgánica o desde sitios web que no son redes sociales. | Medium = `referral` |
| Búsqueda de pago | Tráfico que tiene un código de seguimiento de UTM en el que el medio es &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; Y es una red de distribución de publicidad que no coincide con &quot;Contenido&quot;. | Medium = `^(cpc|ppc|paidsearch)$`<br>Y red de distribución de anuncios ≠ `Content` |
| Social | Tráfico de referencia que proviene de cualquiera de las aproximadamente 400 redes sociales y no está etiquetado como anuncios. | Referente de Social Source = `Yes`<br>O Medium = `^(social|social-network|social-media|sm|social network|social media)$` |
| Correo electrónico | Tráfico de las sesiones etiquetadas con el medio &quot;correo electrónico&quot;. | Código de seguimiento de UTM de Medium = `email` |
| Mostrar | Tráfico que tiene un código de seguimiento UTM en el que el medio es display o cpm. También incluye la interacción AdWords donde la red de distribución de publicidad coincide con &quot;Contenido&quot; | Medium = `^(display|cpm|banner)$`<br>O Red De Distribución De Anuncios = `Content`<br>Y Formato De Anuncio ≠ `Text` |
| Otros | Sesiones de otros canales publicitarios (sin incluir la búsqueda de pago) etiquetados con un medio de &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;afiliate&quot;. | Medium = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## ¿Cómo puedo recrear estas agrupaciones de canales en mi Data Warehouse? {#recreate}

Ahora que sabe que los canales son solo combinaciones de fuentes y medios, es un proceso fácil de 3 pasos recrear estas agrupaciones en su Data Warehouse.

1. **Habilitar su[!DNL Google ECommerce]integración**

   [Cuando esté habilitado](../importing-data/integrations/google-ecommerce.md), asegúrate de [sincronizar](tour-dwm.md#syncing) los campos **medio** y **origen** de tu Data Warehouse. Una vez finalizado, los datos de adquisición de medio y origen se incluirán en el Data Warehouse.

1. **Cargar una asignación de agrupaciones de canales de Google**

   Adobe Commerce crea una tabla con las agrupaciones predeterminadas asignadas como un archivo que puede [descargar](../../assets/ga-channel-mapping.csv).

   Si es un profesional de [!DNL Google Analytics] y ha creado sus propios canales, quiere agregar las reglas específicas a la tabla de asignación antes de cargar el archivo en [!DNL Commerce Intelligence].

   Llévelo a su Data Warehouse como [carga de archivo](../importing-data/connecting-data/using-file-uploader.md).

   ![Interfaz de Data Warehouse Manager que muestra la configuración de clave principal](../../assets/Setting_Primary_Keys.png)

1. **Establezca una relación entre[!DNL Google ECommerce]y la carga de archivos de asignaciones**

   Para establecer una relación entre [!DNL Google ECommerce] y la tabla de asignación, [envíe una solicitud de soporte técnico](../../guide-overview.md#Submitting-a-Support-Ticket) a su equipo de analista de datos y haga referencia a este tema. El analista crea una nueva columna calculada llamada **Canal** en la tabla de comercio electrónico. **Después de un ciclo de actualización completo**, esta columna estará lista para usar en un `Filter` o `Group by`.

Ahora tiene [!DNL Google Analytics Channel] agrupaciones en su Data Warehouse, lo que significa que puede analizar los datos desde una nueva perspectiva:

![Segmentación de la métrica Número de pedidos por canal](../../assets/GA_Channel_Gif.gif)

En este ejemplo, ha comenzado de forma sencilla segmentando la métrica **Número de pedidos** por **Canal**. Pruebe su nueva columna y vea qué tendencias puede identificar en sus datos de [!DNL Google Analytics Channel].

## Documentación relacionada

* [Uso de Report Builder](../../tutorials/using-visual-report-builder.md)
* [Se esperaban [!DNL Google ECommerce]datos](../importing-data/integrations/google-ecommerce-data.md)
* [Creando [!DNL Google ECommerce]dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [¿Cuáles son sus fuentes y canales de adquisición más valiosos?](../analysis/most-value-source-channel.md)
