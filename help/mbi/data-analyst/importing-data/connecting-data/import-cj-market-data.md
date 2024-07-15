---
title: Importación de datos de marketing de afiliados de CJ (Commission Junction)
description: Obtenga información sobre cómo importar datos de afiliados de CJ (Commission Junction) en  [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Importar datos de [!DNL CJ Affiliate]

Para importar datos de [!DNL CJ Affiliate (Commission Junction)] en [!DNL Adobe Commerce Intelligence], simplemente siga los pasos a continuación y adjunte el archivo resultante a un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). El Adobe configurará la tabla de datos de su cuenta y le permitirá continuar cargando datos de forma independiente.

## Exportar [!DNL CJ Affiliate] datos

1. En su cuenta de [!DNL CJ Affiliate], vaya a la pestaña `Reports`.

1. En la ficha `Performance`, seleccione `Report Options`.

1. Establezca `Performance By` igual a `Program`, `Trend` igual a `Daily` y `Date Range` igual al intervalo de fechas que se está auditando.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleccione `Run Report`.

1. En el menú desplegable `File Format`, seleccione `CSV`.  Haga clic en **[!UICONTROL Download]**.

   ![exportar datos de afiliados de cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Una vez que hayas descargado el archivo, puedes [cargar el archivo](../connecting-data/using-file-uploader.md) en tu Data Warehouse de [!DNL Commerce Intelligence].

   Esto crea una tabla en su Data Warehouse [!DNL Commerce Intelligence] en la cual puede continuar cargando datos nuevos periódicamente. Al cargar el archivo, siga los requisitos de formato enumerados en [Uso del cargador de archivos](../connecting-data/using-file-uploader.md).
