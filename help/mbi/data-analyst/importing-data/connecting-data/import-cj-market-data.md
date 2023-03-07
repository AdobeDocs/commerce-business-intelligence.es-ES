---
title: Importación de datos de marketing de afiliados de CJ (Commission Junction)
description: Obtenga información sobre cómo importar datos de afiliados de CJ (Commission Junction) en [!DNL MBI].L [MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Importar `CJ Affiliate` datos

Para importar `CJ Affiliate` Datos de (Commission Junction) en [!DNL MBI], simplemente siga los pasos a continuación y adjunte el archivo resultante a un ticket de asistencia. El Adobe configurará la tabla de datos de su cuenta y le permitirá continuar cargando datos de forma independiente.

## Exportar `CJ Affiliate` Datos

1. En su `CJ Affiliate` cuenta de, vaya a `Reports` pestaña.

1. En el `Performance` pestaña, seleccione `Report Options`.

1. Establecer `Performance By` igual a `Program`, `Trend` igual a `Daily`, y `Date Range` igual al intervalo de fechas que se está auditando.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleccionar `Run Report`.

1. En el `File Format` menú desplegable, seleccione `CSV`.  Clic **[!UICONTROL Download]**.

   ![exportar datos de afiliados de cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Una vez descargado el archivo, puede [cargar el archivo](../connecting-data/using-file-uploader.md) a su [!DNL MBI] Data Warehouse.

   Esto crea una tabla en su [!DNL MBI] Data Warehouse en la que puede seguir cargando datos nuevos periódicamente. Al cargar el archivo, asegúrese de seguir los requisitos de formato enumerados en [Uso del cargador de archivos](../connecting-data/using-file-uploader.md).
