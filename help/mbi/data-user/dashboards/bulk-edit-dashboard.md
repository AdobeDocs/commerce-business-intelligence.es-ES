---
title: Edición masiva de gráficos en paneles
description: Aprenda a utilizar la función de edición masiva en [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Edición masiva de gráficos en paneles

La función de edición masiva facilita el cambio de nombres y fechas de gráficos en los paneles. Por ejemplo, desea que todos los gráficos de un tablero específico hagan referencia a un único almacén e informe con periodicidad mensual en lugar de trimestral. En lugar de cambiar todo manualmente, deje que la variable `bulk-editing` función para realizar el trabajo. En este tema, aprenderá a utilizar lo siguiente:

* [El [!DNL Find/Replace] Función](#findreplace)

* [El [!DNL Prepend Name] Función](#prepend)

* [El [!DNL Change Dates] Función](#dates)

Dicho esto, considere esto - *¿Es necesario que estos cambios sean permanentes?* Si no es así, considere la posibilidad de clonar el panel y, a continuación, cambiar las fechas en el nuevo panel. Esto le permite conservar su panel original mientras realiza los cambios que necesita.

>[!NOTE]
>
>Si está cambiando numerosos informes, el proceso de actualización podría tardar un poco.

## Uso de [!DNL Find/Replace] {#findreplace}

1. Haga clic en el engranaje (![](../../assets/gear-icon.png)) junto al nombre del tablero y, a continuación, el icono [!UICONTROL Bulk Edit Reports] ventana.

1. Clic **[!UICONTROL Chart Title Find and Replace]** en la ventana emergente.

1. En el `Chart Title Find` , escriba las palabras o caracteres que desee buscar.

1. En el `Replace With` , escriba las palabras o caracteres que deben reemplazar lo que hay en el campo `Find` field.

1. Clic **[!UICONTROL Update Reports]**.

Ejemplo:

![edición masiva](../../assets/bulk_edit.gif)

## Antepuesto `Chart Names` {#prepend}

1. Haga clic en el engranaje (![](../../assets/gear-icon.png)) junto al nombre del tablero y, a continuación, el icono [!UICONTROL Bulk Edit Reports] ventana.

1. Clic **[!UICONTROL Prepend Report Names]** en la ventana emergente.

1. Escriba las palabras o los caracteres que desea anteponer a los gráficos.

1. Clic **[!UICONTROL Update Reports]**.

Ejemplo:

![anteponer](../../assets/prepend.gif)

## Cambio `Dates` {#dates}

1. Haga clic en el engranaje (![](../../assets/gear-icon.png)) junto al nombre del tablero y, a continuación, seleccione el icono [!UICONTROL Bulk Edit Reports] ventana.

1. Clic **[!UICONTROL Change Dates]** en la ventana emergente.

1. Establecer el nuevo `Start/End Date` y `Time Interval`. También puede dejar estos campos sin cambios.

1. Clic **[!UICONTROL Update Reports]**.

Ejemplo:

![cambio de fechas](../../assets/dates.gif)
