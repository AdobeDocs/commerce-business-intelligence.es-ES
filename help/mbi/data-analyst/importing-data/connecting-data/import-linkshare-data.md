---
title: Importación de datos de Linkshare
description: Aprenda a importar datos de Linkshare en [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Importar `Linkshare` data

Para traer su `Linkshare` datos en [!DNL MBI], debe hacer dos cosas:

1. [Exportar los datos de Linkshare en ](#export)
1. [Cargar la hoja de cálculo a [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Exportar datos de Linkshare {#export}

1. En `Linkshare` cuenta, vaya a **[!UICONTROL Reports** > **Run Reports].**

1. En el `Report` menú desplegable, seleccione **[!UICONTROL Sales & Activity Report]**.

1. Deje el resto de opciones desplegables como la selección predeterminada.

1. En el `Date Range` menú desplegable, seleccione cualquier opción (`Sun - Sat`, `Mon - Sun`) coincide con su `Start of Week` configuración de [!DNL MBI].

1. Borre la variable `Compare Year-Over-Year Data` casilla de verificación.

1. En `Data Type`, seleccione `Transaction Date`.

   ![importar\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Haga clic en **[!UICONTROL View Report]**.

1. Haga clic en **[!UICONTROL Download]**.

   En este punto, una `.csv` se creará y descargará.

Una vez descargado el archivo, puede cargarlo en [!DNL MBI] usando la variable [`File Upload` función](../connecting-data/using-file-uploader.md).
