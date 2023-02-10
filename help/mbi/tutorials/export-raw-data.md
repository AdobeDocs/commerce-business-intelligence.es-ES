---
title: Exportar datos sin procesar
description: Aprenda a exportar registros de su [!DNL MBI] Data Warehouse para obtener una visión más detallada de lo que alimenta su tablero.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Exportar datos sin procesar

Con las exportaciones de datos sin procesar, puede exportar registros desde [!DNL MBI] Data Warehouse para obtener una visión más detallada de lo que alimenta su tablero. Además, las exportaciones de datos sin procesar pueden ayudarle [detectar discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en).

Las exportaciones de datos sin procesar proporcionan acceso a columnas y dimensiones adicionales generadas mediante la desnormalización y la preagregación de métricas relevantes. Por ejemplo, `User's first order date` es una dimensión que puede exportar para cada usuario de [!DNL MBI], aunque es posible que no esté disponible en la base de datos.

Este tutorial trata lo siguiente:

* [Selección de datos para exportar](#select)
* [Descarga de la exportación (](#download)
* [Acceso a exportaciones históricas](#historical)

## Paso 1: Selección de datos para exportar {#select}

Existen dos maneras de exportar datos sin procesar en [!DNL MBI]: en el nivel de gráfico o en el nivel de tabla.

### Exportación en el nivel de tabla de su `Manage Data` Tabulación

Si desea exportar la tabla desde `Manage Data` , necesitará [Administrador](../administrator/user-management/user-management.md) permisos.

1. Haga clic en **[!UICONTROL Manage Data** > ** Exportar datos **> **Exportación de datos sin procesar]** para empezar.
1. Verá un `Export List` de las exportaciones de datos creadas recientemente, si las hay. Haga clic en **[!UICONTROL Add Export]** para crear una nueva exportación.
1. La variable `New Raw Data Export` se mostrará el cuadro de diálogo. Aquí puede personalizar la exportación seleccionando o anulando la selección de columnas y filtros:

   * `Table` - El `Table` selecciona la tabla desde la que se exportarán los datos. De forma predeterminada, se mostrará la tabla en la que navegó.
   * `Export Name` : En este campo, introduzca el nombre de la exportación. Por ejemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Este campo enumera las columnas (dimensiones) de la base de datos que están disponibles para su inclusión en la exportación. Para agregar una columna, haga clic en su nombre.
   * `Selected Columns` : este campo enumera las columnas (dimensiones) incluidas actualmente en la exportación. Para quitar una columna, haga clic en su nombre.
   * `Filter` : Esta sección enumera los filtros aplicados actualmente a la exportación. Estos filtros se pueden cambiar; también se pueden agregar nuevos filtros para exportar un conjunto de datos en particular.
   * Cuando termine, haga clic en **[!UICONTROL Export Data]**.

### Exportación en el nivel de gráfico desde el panel

1. Haga clic en el icono de engranaje en la esquina superior derecha de cualquier gráfico.
1. Select `Raw Export` en el menú desplegable para mostrar la `Raw Export` diálogo.
1. Personalice la exportación seleccionando la opción `table`, `columns`y `filters` para incluir o excluir. Consulte la sección anterior para obtener información más detallada sobre los campos de este módulo.
   >[!NOTE]
   >
   >La tabla que se muestra en la variable `Table` es, de forma predeterminada, la tabla que alimenta el gráfico.

1. Cuando termine, haga clic en **[!UICONTROL Export Data]**.

Echemos un vistazo a todo el proceso a nivel de gráfico.

![](../assets/Chart-level_export.gif)

## Paso 2: Descarga de la exportación {#download}

La exportación empezará a procesarse inmediatamente después de completar las selecciones en el `Raw Data Export` diálogo. Como algunas exportaciones pueden tener un tamaño grande, están limitadas a 10 millones de filas y pueden tardar algún tiempo en ejecutarse.

Para comprobar si la exportación está lista, haga clic en **[!UICONTROL Raw Data Exports]** en la esquina superior derecha de la pantalla. Haga clic en **[!UICONTROL Download]** para descargar un zip `.csv` del archivo de exportación.

![](../assets/Downloading_export.gif)

## Paso 3: Acceso a exportaciones históricas {#historical}

Para ver las exportaciones anteriores, haga clic en **[!UICONTROL Raw Data Export]** en la esquina superior derecha de la pantalla. Se puede acceder a los informes pendientes y completados durante un máximo de siete días.

¡Felicidades! Has terminado.
