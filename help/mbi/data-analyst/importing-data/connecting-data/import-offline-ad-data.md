---
title: Importar otros datos de gasto en publicidad
description: Obtenga información sobre cómo importar datos de gasto en publicidad o sin conexión a [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importar otros datos de gasto en publicidad

La carga de los datos de gasto en publicidad le permite medir el ROI de la campaña combinando el coste de la publicidad con el cliente `lifetime value (CLV)` de usuarios adquiridos de sus campañas.

## Carga de datos de costes de publicidad

El primer paso para analizar los datos de gasto en publicidad es obtener los datos. Dado que la mayoría de las plataformas de publicidad le permiten exportar informes, Adobe recomienda exportar los datos sin procesar de su plataforma de publicidad y cargarlos directamente en [!DNL MBI] sin ninguna manipulación. Puede realizar operaciones en los datos de la Data Warehouse, por lo que no es necesario duplicar los esfuerzos.

Después de exportar los datos de gasto en publicidad, utilice el [`File Upload` característica](../connecting-data/using-file-uploader.md) para introducir los datos en la Data Warehouse. Puede cargar nuevos datos en el mismo [!DNL MBI] tabla con el tiempo.

## Fuentes sin conexión

Además de sus campañas en línea, es posible que también tenga anuncios sin conexión, como en la radio o en un cartel. Para tener en cuenta estos casos, puede cargar manualmente una hoja de cálculo con los datos de coste a [!DNL MBI].

La estructura de tabla explorada a continuación se recomienda al crear una `.csv` para registrar los datos de gasto del anuncio. También se adjunta un archivo de plantilla al final de este artículo para servir de ejemplo. Las columnas recomendadas son:

* `ID` : es un identificador único para cada fila de datos que la base de datos utiliza como clave principal. Debe ser diferente para cada fila.
* `Date` - Fecha en la que se ejecutó la campaña, en formato aaaa-mm-dd.
* `Amount` - Esta es la cantidad que gastó en la campaña.
* `campaign` - Nombre de la campaña. Si está utilizando [!DNL Google Analytics] para realizar el seguimiento de los demás datos sobre gasto en publicidad, deben coincidir con el nombre utm\_campaign.
* `source` - Este es el nombre de origen. Si está utilizando [!DNL Google Analytics], debe coincidir con el `utm_source` nombre.
* `other` (Opcional): También puede incorporar columnas adicionales que le ayuden a segmentar campañas y costes. También puede ser una forma de resumir varios nombres de campañas de UTM diferentes en una sola campaña coherente con fines de seguimiento. En lugar de configurarlo manualmente, podría ser bueno usar una Búsqueda en V en una segunda hoja para hacer coincidir cada Nombre de campaña con el Otro nombre y crear un informe aquí de forma dinámica.

## Relacionado

* [Connect [!DNL AdWords] datos](../integrations/google-adwords.md)
* [Aumentar el retorno de la inversión en campañas publicitarias](../../analysis/roi-ad-camp.md)
