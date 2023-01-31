---
title: Importar datos de MailChimp
description: Aprenda a importar datos de MailChimp en [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Importar `MailChimp` data

Para obtener una imagen completa de los esfuerzos de campaña, puede importar su `MailChimp` enviar datos de campaña de correo electrónico a [!DNL MBI]. Para completar la importación, debe hacer lo siguiente para cada `MailChimp` campaña que tiene:

## Exportar Abrir datos {#opens}

1. Tras iniciar sesión `MailChimp`, vaya a la `Campaigns` pestaña .

   ![importar mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Haga clic en **[!UICONTROL View Report]** junto al nombre de la campaña.

   ![importar mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Haga clic en el **[!UICONTROL Opened]** número.

   ![importar mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el `.csv` archivo.

   Deberá agregar `primary key`, `date (mm/dd/yyyy)`y `campaign name` a este archivo. Asegúrese de que la variable `primary keys` son exclusivos de cada fila.

   ![importar mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportar datos de clics {#clicks}

1. Vuelva a la página `View Report` para la campaña.

1. Haga clic en el número que `Clicked`.

   ![importar mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Haga clic en cualquiera de los números debajo de `Total Clicks` O `Unique Clicks` para abrir el Navegador.

   ![importar mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el `.csv` archivo.

   Deberá agregar `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`y `URL` a este archivo. No es necesario agregar la dirección URL completa, solo es algo que le hará saber en qué se hizo clic.

   ![importar mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Repita los pasos 3 y 4 para cada URL donde se haga clic en el correo electrónico, combinando todos los datos en el mismo `.csv` cuando termine.

## Exportar datos enviados {#sent}

1. Vaya a `Campaigns` de MailChimp.

1. Haga clic en **[!UICONTROL View Report]** junto al nombre de la campaña.

1. Haga clic en el número situado junto a `Recipients`.

   ![importar mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Haga clic en **[!UICONTROL Export]** y guarde el `.csv` archivo.

   Deberá agregar `Primary Key`, `date (mm/dd/yyyy)`y `campaign name` a este archivo.

   ![importar mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparar archivos para la carga en [!DNL MBI] {#upload}

Cada archivo: `Opens`, `Clicks`y `Sent` - debe cargarse en [!DNL MBI] como archivo independiente. También se recomienda asignar un nombre a los archivos mediante esta convención de nombres: `MailChimp\_ACTION\_DATE`. Reemplazar `ACTION` con `Open`, `Click`o `Sent`y reemplace `DATE` con la fecha de exportación.

Cuando esté listo para cargar los archivos, utilice la variable [`File Upload` función](../connecting-data/using-file-uploader.md) para introducir los datos en el almacén de datos.
