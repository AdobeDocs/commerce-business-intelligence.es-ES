---
title: Importación de datos de Linkshare
description: Obtenga información sobre cómo importar datos de Linkshare en [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importar `Linkshare` datos

Para traer su `Linkshare` datos en [!DNL MBI], debe hacer dos cosas:

1. [Exportación de los datos de Linkshare en ](#export)
1. [Cargar la hoja de cálculo en [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Exportar datos de Linkshare {#export}

1. En su `Linkshare` cuenta, vaya a **[!UICONTROL Reports** > **Run Reports].**

1. En el `Report` menú desplegable, seleccione **[!UICONTROL Sales & Activity Report]**.

1. Deje todas las demás opciones desplegables como la selección predeterminada.

1. En el `Date Range` , seleccione cualquier opción (`Sun - Sat`, `Mon - Sun`) coincide con su `Start of Week` configuración en [!DNL MBI].

1. Borre la `Compare Year-Over-Year Data` casilla de verificación

1. En `Data Type`, seleccione `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clic **[!UICONTROL View Report]**.

1. Clic **[!UICONTROL Download]**.

   En este punto, una `.csv` y descargado.

Una vez descargado el archivo, puede cargarlo en [!DNL MBI] uso del [`File Upload` característica](../connecting-data/using-file-uploader.md).
