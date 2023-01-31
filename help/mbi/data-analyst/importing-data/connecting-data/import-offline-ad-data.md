---
title: Importar otros datos de gastos de publicidad
description: Aprenda a importar datos de gasto de publicidad sin conexión u otro tipo a [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importar otros datos de gastos de publicidad

La carga de los datos de gasto en publicidad le permitirá medir el ROI de la campaña al casar su coste publicitario con el cliente `lifetime value (CLV)` de usuarios adquiridos en sus campañas.

## Carga de datos de costes de publicidad

El primer paso para analizar los datos del gasto en publicidad es obtener los datos. Dado que la mayoría de las plataformas de publicidad le permiten exportar informes, le recomendamos que exporte los datos sin procesar de su plataforma de publicidad y los cargue directamente en [!DNL MBI] sin ninguna manipulación. Puede realizar operaciones con los datos del almacén de datos, por lo que no es necesario duplicar los esfuerzos.

Después de exportar los datos de gasto de publicidad, use la variable [`File Upload` función](../connecting-data/using-file-uploader.md) para introducir los datos en el almacén de datos. Puede cargar nuevos datos en el mismo [!DNL MBI] con el tiempo.

## Fuentes sin conexión

Además de sus campañas en línea, también puede tener anuncios sin conexión, como por ejemplo en la radio o un anuncio. Para tener en cuenta estos casos, puede cargar manualmente una hoja de cálculo con los datos de coste en [!DNL MBI].

Se recomienda la siguiente estructura de tabla al crear un `.csv` para registrar los datos de gastos de publicidad. En la parte inferior de este artículo también se adjunta un archivo de plantilla que sirve de ejemplo. Las columnas recomendadas son:

* `ID` : es un identificador único para cada fila de datos que utiliza la base de datos como clave principal. Debe ser diferente para cada fila.
* `Date` - Esta es la fecha de ejecución de la campaña, en formato aaaa-mm-dd.
* `Amount` - Esta es la cantidad que gastó en la campaña.
* `campaign` - Este es el nombre de la campaña. Si está utilizando [!DNL Google Analytics] para realizar un seguimiento de los demás datos de gastos de publicidad, deben coincidir con el nombre utm\_campaign.
* `source` - Este es el nombre de la fuente. Si está utilizando [!DNL Google Analytics], debe coincidir con la variable `utm_source` nombre.
* `other` (Opcional) : también puede incorporar columnas adicionales que le ayudarán a segmentar las campañas y los costes. También puede ser una forma de resumir varios nombres de campaña diferentes de UTM en una sola campaña coherente para fines de seguimiento. En lugar de configurarlo manualmente, puede que sea bueno usar una búsqueda de V en una segunda hoja para hacer coincidir cada Nombre de campaña con el Otro nombre y crear un informe aquí de forma dinámica.

## Relacionado

* [Connect [!DNL AdWords] data](../integrations/google-adwords.md)
* [Aumento del ROI en las campañas publicitarias](../../analysis/roi-ad-camp.md)
