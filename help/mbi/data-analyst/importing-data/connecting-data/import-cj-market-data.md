---
title: Importación de datos de marketing de afiliados de CJ (Commission Junction)
description: Obtenga información sobre cómo importar datos de afiliados de CJ (Commission Junction) en [!DNL Commerce Intelligence].L Inteligencia comercial].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importar [!DNL CJ Affiliate] datos

Para importar [!DNL CJ Affiliate (Commission Junction)] datos en [!DNL Adobe Commerce Intelligence], simplemente siga los pasos a continuación y adjunte el archivo resultante a una [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). El Adobe configurará la tabla de datos de su cuenta y le permitirá continuar cargando datos de forma independiente.

## Exportar [!DNL CJ Affiliate] Datos

1. En su [!DNL CJ Affiliate] cuenta de, vaya a `Reports` pestaña.

1. En el `Performance` pestaña, seleccione `Report Options`.

1. Establecer `Performance By` igual a `Program`, `Trend` igual a `Daily`, y `Date Range` igual al intervalo de fechas que se está auditando.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleccionar `Run Report`.

1. En el `File Format` menú desplegable, seleccione `CSV`.  Haga clic **[!UICONTROL Download]**.

   ![exportar datos de afiliados de cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Una vez descargado el archivo, puede [cargar el archivo](../connecting-data/using-file-uploader.md) a su [!DNL Commerce Intelligence] Data Warehouse.

   Esto crea una tabla en su [!DNL Commerce Intelligence] Data Warehouse en la que puede seguir cargando datos nuevos periódicamente. Al cargar el archivo, siga los requisitos de formato enumerados en [Uso del cargador de archivos](../connecting-data/using-file-uploader.md).
