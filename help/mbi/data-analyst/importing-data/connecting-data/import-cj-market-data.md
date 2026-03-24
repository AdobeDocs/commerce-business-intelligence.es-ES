---
title: Importación de datos de marketing de afiliados de CJ (Commission Junction)
description: Obtenga información sobre cómo importar datos de afiliados de CJ (Commission Junction) en  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;.
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# Importar datos de [!DNL CJ Affiliate]

Para importar datos de [!DNL CJ Affiliate (Commission Junction)] en [!DNL Adobe Commerce Intelligence], simplemente siga los pasos a continuación y adjunte el archivo resultante a un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es). Adobe configurará la tabla de datos en su cuenta y le permitirá continuar cargando datos de forma independiente.

## Exportar [!DNL CJ Affiliate] datos

1. En su cuenta de [!DNL CJ Affiliate], vaya a la pestaña `Reports`.

1. En la ficha `Performance`, seleccione `Report Options`.

1. Establezca `Performance By` igual a `Program`, `Trend` igual a `Daily` y `Date Range` igual al intervalo de fechas que se está auditando.

   ![export-cj-afiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleccione `Run Report`.

1. En el menú desplegable `File Format`, seleccione `CSV`.  Haga clic en **[!UICONTROL Download]**.

   ![exportar datos de afiliados de cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Una vez que hayas descargado el archivo, puedes [cargar el archivo](../connecting-data/using-file-uploader.md) en tu Data Warehouse [!DNL Commerce Intelligence].

   Esto crea una tabla en su Data Warehouse [!DNL Commerce Intelligence] en la cual puede continuar cargando datos nuevos periódicamente. Al cargar el archivo, siga los requisitos de formato enumerados en [Uso del cargador de archivos](../connecting-data/using-file-uploader.md).
