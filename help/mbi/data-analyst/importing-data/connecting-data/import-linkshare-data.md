---
title: Importación de datos de Linkshare
description: Obtenga información sobre cómo importar datos de Linkshare en  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 0%

---

# Importar datos de [!DNL Linkshare]

Para incluir los datos de [!DNL Linkshare] en [!DNL Adobe Commerce Intelligence], debe hacer dos cosas:

1. [Exportación de los datos de Linkshare en &#x200B;](#export)
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

Una vez descargado el archivo, puede cargarlo en [!DNL Commerce Intelligence] mediante la característica [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md).
