---
title: Importación de datos de gasto de Bing Ad
description: Obtenga información sobre cómo importar datos de gasto en publicidad de Bing en [!DNL Commerce Intelligence] para su análisis.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Importar [!DNL Bing] Datos

Para importar [!DNL Bing] datos de gasto en publicidad en [!DNL Adobe Commerce Intelligence] para realizar el análisis, simplemente exporte los datos de [!DNL Bing Ads Editor] en un `.csv` y cargarlo en [!DNL Commerce Intelligence] según los pasos descritos a continuación.

## [!DNL Bing Ads Editor]

Para exportar su [!DNL Bing Ads] datos, debe tener [!DNL Bing Ads Editor] instalado. Puede encontrar una descarga gratuita de [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## [!DNL Bing Ads] Exportación de datos

1. En el `Browser` panel de [!DNL Bing Ads Editor], haga clic con el botón derecho en la campaña o grupo de anuncios que desee exportar y haga clic en **[!UICONTROL Export]**.
1. En el `Export` , haga clic en **[!UICONTROL Export]**.
1. En el `Save As` , haga clic en la carpeta en la que desea guardar el archivo de exportación.
1. En el `File name` , elija un nombre para la exportación de archivos.
1. Haga clic **[!UICONTROL Save]**.
1. Una vez descargado el archivo,  [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para realizar una primera carga en su nombre y configurar las dimensiones back-end necesarias.
