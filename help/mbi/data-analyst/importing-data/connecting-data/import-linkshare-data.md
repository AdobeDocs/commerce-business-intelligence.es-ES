---
title: Importación de datos de Linkshare
description: Obtenga información sobre cómo importar datos de Linkshare en  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importar datos de [!DNL Linkshare]

Para incluir los datos de [!DNL Linkshare] en [!DNL Adobe Commerce Intelligence], debe hacer dos cosas:

1. [Exportación de los datos de Linkshare en ](#export)
1. [Cargar la hoja de cálculo en  [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exportar datos de Linkshare {#export}

1. En su cuenta de [!DNL Linkshare], vaya a **[!UICONTROL Reports** > **Run Reports].**

1. En el menú desplegable `Report`, seleccione **[!UICONTROL Sales & Activity Report]**.

1. Deje todas las demás opciones desplegables como la selección predeterminada.

1. En el menú desplegable `Date Range`, seleccione cualquier opción (`Sun - Sat`, `Mon - Sun`) que coincida con la configuración de `Start of Week` en [!DNL Commerce Intelligence].

1. Desactive la casilla de verificación `Compare Year-Over-Year Data`.

1. En `Data Type`, seleccione `Transaction Date`.

   ![importando\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Haga clic en **[!UICONTROL View Report]**.

1. Haga clic en **[!UICONTROL Download]**.

   En este punto, seleccione un archivo de `.csv` y descárguelo.

Una vez descargado el archivo, puede cargarlo en [!DNL Commerce Intelligence] mediante la característica [`File Upload` ](../connecting-data/using-file-uploader.md).
