---
title: Importar otros datos de gasto en publicidad
description: Aprenda a importar datos de gasto en publicidad sin conexión o de otro tipo en  [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Importar otros datos de gasto en publicidad

La carga de los datos de gasto en publicidad le permite medir el retorno de la inversión de la campaña combinando el costo de la publicidad con el `customer lifetime value (CLV)` de usuarios adquiridos de las campañas.

## Carga de datos de costes de publicidad

El primer paso para analizar los datos de gasto en publicidad es obtener los datos. Dado que la mayoría de las plataformas de publicidad le permiten exportar informes, Adobe recomienda exportar los datos sin procesar de su plataforma de publicidad y cargarlos directamente en [!DNL Commerce Intelligence] sin ninguna manipulación. Puede realizar operaciones en los datos de su Data Warehouse, por lo que no es necesario duplicar los esfuerzos.

Después de haber exportado los datos de gasto en publicidad, use la característica [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md) para llevar los datos a Data Warehouse. Con el tiempo, puede cargar nuevos datos en la misma tabla [!DNL Commerce Intelligence].

## Fuentes sin conexión

Además de sus campañas en línea, es posible que también tenga anuncios sin conexión, como en la radio o en un cartel. Para tener en cuenta estos casos, puede cargar manualmente una hoja de cálculo con los datos de costo en [!DNL Commerce Intelligence].

La estructura de tabla que se explora a continuación se recomienda al crear un archivo de `.csv` para registrar y gastar datos. También se adjunta un archivo de plantilla al final de este tema para que sirva de ejemplo. Las columnas recomendadas son:

* `ID`: es un identificador único para cada fila de datos que la base de datos utiliza como clave principal. Debe ser diferente para cada fila.
* `Date`: fecha en la que se ejecutó la campaña, en formato aaaa-mm-dd.
* `Amount` - Esta es la cantidad que gastó en la campaña.
* `campaign`: nombre de la campaña. Si usa [!DNL Google Analytics] para hacer un seguimiento de los demás datos de gasto en publicidad, debe coincidir con el nombre utm\_campaign.
* `source`: este es el nombre de origen. Si usa [!DNL Google Analytics], debe coincidir con el nombre de `utm_source`.
* `other` (opcional): también puede incorporar columnas adicionales que le ayuden a segmentar campañas y costos. También puede ser una forma de resumir varios nombres de campañas de UTM diferentes en una sola campaña coherente con fines de seguimiento. En lugar de configurarlo manualmente, podría ser bueno usar una Búsqueda en V en una segunda hoja para hacer coincidir cada Nombre de campaña con el Otro nombre y crear un informe aquí de forma dinámica.

## Relacionado

* [Conectar  [!DNL AdWords] datos](../integrations/google-adwords.md)
* [Aumentar el retorno de la inversión en campañas publicitarias](../../analysis/roi-ad-camp.md)
