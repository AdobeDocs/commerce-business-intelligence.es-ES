---
title: Edición masiva de gráficos en paneles
description: Aprenda a utilizar la característica de edición en lotes en [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: 'https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c'
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
  - id: 06e518d4-11ae-5c20-98b0-ce8ab05d7166
    internal-label: Dashboards
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
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%
---
# Edición masiva de gráficos en paneles

La función de edición masiva facilita el cambio de nombres y fechas de gráficos en los paneles. Por ejemplo, desea que todos los gráficos de un tablero específico hagan referencia a un único almacén e informe con periodicidad mensual en lugar de trimestral. En lugar de cambiar todo manualmente, deje que la característica `bulk-editing` haga el trabajo. En este tema, aprenderá a utilizar lo siguiente:

* [Función  [!DNL Find/Replace] &#x200B;](#findreplace)

* [Función  [!DNL Prepend Name] &#x200B;](#prepend)

* [Función  [!DNL Change Dates] &#x200B;](#dates)

Dicho esto, considere esto - *¿Es necesario que estos cambios sean permanentes?* Si no es así, considere la posibilidad de clonar el panel y, a continuación, cambiar las fechas en el nuevo panel. Esto le permite conservar su panel original mientras realiza los cambios que necesita.

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
