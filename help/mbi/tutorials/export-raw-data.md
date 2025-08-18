---
title: Exportar datos sin procesar
description: Aprenda a exportar registros de su  [!DNL Commerce Intelligence] Data Warehouse para obtener más información sobre lo que alimenta su tablero.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Exportar datos sin procesar

Con las exportaciones de datos sin procesar, puede exportar registros de su Data Warehouse para obtener una visión más detallada de lo que alimenta su panel. Además, las exportaciones de datos sin procesar pueden ayudarle a [identificar discrepancias en los datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=es).

Las exportaciones de datos sin procesar proporcionan acceso a columnas y dimensiones adicionales generadas mediante la desnormalización y la agregación previa de métricas relevantes. Por ejemplo, `User's first order date` es una dimensión que puede exportar para cada usuario en [!DNL Commerce Intelligence], aunque es posible que no esté disponible en la base de datos.

Este tutorial abarca lo siguiente:

* [Selección de datos para exportar](#select)
* [Descarga de la exportación (](#download)
* [Acceso a exportaciones históricas](#historical)

## Paso 1: Selección de datos para exportar {#select}

Existen dos maneras de exportar datos sin procesar en [!DNL Commerce Intelligence]:

1. a nivel de gráfico
1. a nivel de tabla

### Exportación a nivel de tabla en la ficha [!UICONTROL Manage Data]

Si desea exportar la tabla desde la ficha [!UICONTROL Manage Data], necesita los permisos de [Admin](../administrator/user-management/user-management.md).

1. Haga clic en **[!UICONTROL Manage Data** > **&#x200B; Exportar datos &#x200B;**> **Exportación de datos sin procesar]**.
1. Verá un(a) `Export List` de exportaciones de datos creadas recientemente, si las hay. Haga clic en **[!UICONTROL Add Export]** para crear una exportación.
1. Se muestra el cuadro de diálogo `New Raw Data Export`. Aquí puede personalizar la exportación seleccionando o anulando la selección de columnas y filtros:

   * `Table` - El campo `Table` selecciona la tabla desde la que se exportan los datos. De forma predeterminada, esto muestra la tabla a la que se desplazó.
   * `Export Name` - En este campo, escriba el nombre de la exportación. Por ejemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns`: este campo enumera las columnas (dimensiones) de la base de datos que están disponibles para su inclusión en la exportación. Para agregar una columna, haga clic en su nombre.
   * `Selected Columns` - Este campo enumera las columnas (dimensiones) incluidas actualmente en la exportación. Para quitar una columna, haga clic en su nombre.
   * `Filter`: en esta sección se enumeran los filtros aplicados actualmente a la exportación. Estos filtros se pueden cambiar, y también se pueden añadir nuevos filtros para exportar un conjunto de datos concreto.
   * Cuando termine, haga clic en **[!UICONTROL Export Data]**.

### Exportación a nivel de gráfico desde el panel

1. Haga clic en el icono de engranaje en la esquina superior derecha de cualquier gráfico.

1. Seleccione `Raw Export` del menú desplegable para mostrar el cuadro de diálogo `Raw Export`.

1. Personalice la exportación eligiendo `table`, `columns` y `filters` para incluir o excluir. Consulte la sección anterior para obtener información más detallada sobre los campos de este módulo.

   >[!NOTE]
   >
   >La tabla que se muestra en el campo `Table` es, de forma predeterminada, la tabla que alimenta el gráfico.

1. Cuando termine, haga clic en **[!UICONTROL Export Data]**.

Observe todo el proceso en el nivel de gráfico.

![](../assets/Chart-level_export.gif)

## Paso 2: Descarga de la exportación {#download}

La exportación empezará a procesarse inmediatamente después de completar las selecciones en el cuadro de diálogo `Raw Data Export`. Como algunas exportaciones pueden ser de gran tamaño, están limitadas a 10 millones de filas y pueden tardar algún tiempo en ejecutarse.

Para comprobar si la exportación está lista, haga clic en **[!UICONTROL Raw Data Exports]**, en la esquina superior derecha de la pantalla. Haga clic en **[!UICONTROL Download]** para descargar un archivo comprimido `.csv` de su exportación.

![](../assets/Downloading_export.gif)

## Paso 3: Acceso a exportaciones históricas {#historical}

Para ver las exportaciones anteriores, haga clic en **[!UICONTROL Raw Data Export]**, en la esquina superior derecha de la pantalla. Se puede acceder a los informes pendientes y completados durante un máximo de siete días.
