---
title: Importar datos de MailChimp
description: Aprenda a importar datos de MailChimp en  [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y
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
source-wordcount: 274
ht-degree: 0%

---

# Importar datos de [!DNL Mailchimp]

Para obtener una imagen completa de sus campañas, puede importar los datos de su campaña de correo electrónico [!DNL Mailchimp] en [!DNL Commerce Intelligence]. Para completar la importación, debe hacer lo siguiente para cada campaña de [!DNL Mailchimp] que tenga:

## Exportar Datos de aperturas {#opens}

1. Después de iniciar sesión en [!DNL Mailchimp], vaya a la ficha `Campaigns`.

   ![importar mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Haga clic en **[!UICONTROL View Report]**, junto al nombre de la campaña.

   ![importar mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Haga clic en el número **[!UICONTROL Opened]**.

   ![importar mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el archivo `.csv`.

   Debe agregar `primary key`, `date (mm/dd/yyyy)` y `campaign name` columnas a este archivo. Asegúrese de que `primary keys` sean únicos para cada fila.

   ![importar mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportar datos de clics {#clicks}

1. Vuelva a la pantalla `View Report` de la campaña.

1. Haga clic en el número que `Clicked`.

   ![importar mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Haga clic en el número de la columna `Total Clicks` O `Unique Clicks`.

   ![importar mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el archivo `.csv`.

   Debe agregar `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` y `URL` columnas a este archivo. No es necesario que añada la dirección URL completa, sino que es algo que le permite saber en qué se hizo clic.

   ![importar mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Repita los pasos 3 y 4 para cada URL donde hizo clic en el correo electrónico, combinando todos los datos en el mismo archivo de `.csv` cuando termine.

## Exportar datos enviados {#sent}

1. Vaya a la ficha `Campaigns` de [!DNL Mailchimp].

1. Haga clic en **[!UICONTROL View Report]** junto al nombre de la campaña.

1. Haga clic en el número que aparece junto a `Recipients`.

   ![importar mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el archivo `.csv`.

   Debe agregar `Primary Key`, `date (mm/dd/yyyy)` y `campaign name` columnas a este archivo.

   ![importar mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparar archivos para cargar en [!DNL Commerce Intelligence] {#upload}

Cada archivo - `Opens`, `Clicks` y `Sent` - debe cargarse en [!DNL Commerce Intelligence] como un archivo independiente. Adobe recomienda asignar un nombre a los archivos con esta convención de nombres: `MailChimp\_ACTION\_DATE`. Reemplazar `ACTION` por `Open`, `Click` o `Sent`, y reemplazar `DATE` con la fecha de exportación.

Cuando esté listo para cargar los archivos, use la característica [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md) para llevar los datos a su Data Warehouse.
