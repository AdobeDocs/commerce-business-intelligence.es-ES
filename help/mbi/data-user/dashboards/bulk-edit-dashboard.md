---
title: Edición masiva de gráficos en paneles
description: Aprenda a utilizar la característica de edición en lotes en  [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 260
ht-degree: 0%

---

# Edición masiva de gráficos en paneles

La función de edición masiva facilita el cambio de nombres y fechas de gráficos en los paneles. Por ejemplo, desea que todos los gráficos de un tablero específico hagan referencia a un único almacén e informe con periodicidad mensual en lugar de trimestral. En lugar de cambiar todo manualmente, deje que la característica `bulk-editing` haga el trabajo. En este tema, aprenderá a utilizar lo siguiente:

* [Función  [!DNL Find/Replace] ](#findreplace)

* [Función  [!DNL Prepend Name] ](#prepend)

* [Función  [!DNL Change Dates] ](#dates)

Dicho esto, considere esto - *¿Es necesario que estos cambios sean permanentes?* Si no es así, considere la posibilidad de clonar el tablero y, a continuación, cambiar las fechas en el tablero nuevo. Esto le permite conservar su panel original mientras realiza los cambios que necesita.

>[!NOTE]
>
>Si está cambiando numerosos informes, el proceso de actualización podría tardar un poco.

## Usando [!DNL Find/Replace] {#findreplace}

1. Haga clic en el icono de engranaje (![Icono de engranaje](../../assets/gear-icon.png)) junto al nombre del panel y, a continuación, en la ventana [!UICONTROL Bulk Edit Reports].

1. Haga clic en **[!UICONTROL Chart Title Find and Replace]** en la ventana emergente.

1. En el campo `Chart Title Find`, escriba las palabras o los caracteres que desee buscar.

1. En el campo `Replace With`, escriba las palabras o los caracteres que deben reemplazar lo que se encuentra en el campo `Find`.

1. Haga clic en **[!UICONTROL Update Reports]**.

Ejemplo:

![edición en lotes](../../assets/bulk_edit.gif)

## Anteponiendo `Chart Names` {#prepend}

1. Haga clic en el icono de engranaje (![Icono de engranaje](../../assets/gear-icon.png)) junto al nombre del panel y, a continuación, en la ventana [!UICONTROL Bulk Edit Reports].

1. Haga clic en **[!UICONTROL Prepend Report Names]** en la ventana emergente.

1. Escriba las palabras o los caracteres que desea anteponer a los gráficos.

1. Haga clic en **[!UICONTROL Update Reports]**.

Ejemplo:

![anteponer](../../assets/prepend.gif)

## Cambiando `Dates` {#dates}

1. Haga clic en el icono de engranaje (![Icono de engranaje](../../assets/gear-icon.png)) junto al nombre del panel y, a continuación, seleccione la ventana [!UICONTROL Bulk Edit Reports].

1. Haga clic en **[!UICONTROL Change Dates]** en la ventana emergente.

1. Establecer los nuevos `Start/End Date` y `Time Interval`. También puede dejar estos campos sin cambios.

1. Haga clic en **[!UICONTROL Update Reports]**.

Ejemplo:

![cambiando fechas](../../assets/dates.gif)
