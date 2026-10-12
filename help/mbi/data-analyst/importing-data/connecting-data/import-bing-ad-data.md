---
title: Importación de datos de gasto de Bing Ad
description: Obtenga información sobre cómo importar datos de gasto en publicidad de Bing en [!DNL Commerce Intelligence] para su análisis.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%
---
# Importar [!DNL Bing] datos

Para importar los datos de gasto en publicidad de [!DNL Bing] en [!DNL Adobe Commerce Intelligence] para su análisis, simplemente exporte los datos de [!DNL Bing Ads Editor] en formato `.csv` y cárguelos en [!DNL Commerce Intelligence] según los pasos descritos a continuación.

## [!DNL Bing Ads Editor]

Para exportar los datos de [!DNL Bing Ads], debe tener [!DNL Bing Ads Editor] instalado. Puedes encontrar una descarga gratuita de [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## Exportación de datos de [!DNL Bing Ads]

1. En el panel `Browser` de [!DNL Bing Ads Editor], haga clic con el botón secundario en la campaña o grupo de anuncios que desee exportar y haga clic en **[!UICONTROL Export]**.
1. En el cuadro de diálogo `Export`, haga clic en **[!UICONTROL Export]**.
1. En el cuadro de diálogo `Save As`, haga clic en la carpeta en la que desea guardar el archivo de exportación.
1. En el cuadro `File name`, elija un nombre para la exportación de archivos.
1. Haga clic en **[!UICONTROL Save]**.
1. Una vez descargado el archivo, [comuníquese con la atención al cliente](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies) para realizar una primera carga en su nombre y configurar las dimensiones de back-end necesarias.
