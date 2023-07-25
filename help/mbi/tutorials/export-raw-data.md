---
title: Exportar datos sin procesar
description: Obtenga información sobre cómo exportar registros desde [!DNL Commerce Intelligence] Data Warehouse para obtener una visión más detallada de lo que alimenta el panel.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Exportar datos sin procesar

Con las exportaciones de datos sin procesar, puede exportar registros de la Data Warehouse para obtener una visión más detallada de lo que alimenta el panel. Además, las exportaciones de datos sin procesar pueden ayudarle [localizar discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Las exportaciones de datos sin procesar proporcionan acceso a columnas y dimensiones adicionales generadas mediante la desnormalización y la agregación previa de métricas relevantes. Por ejemplo, `User's first order date` es una dimensión que puede exportar para cada usuario en [!DNL Commerce Intelligence], aunque es posible que no esté disponible en la base de datos.

Este tutorial abarca lo siguiente:

* [Selección de datos para exportar](#select)
* [Descarga de la exportación (](#download)
* [Acceso a exportaciones históricas](#historical)

## Paso 1: Selección de datos para exportar {#select}

Existen dos maneras de exportar datos sin procesar en [!DNL Commerce Intelligence]:

1. a nivel de gráfico
1. a nivel de tabla

### Exportación a nivel de tabla en su [!UICONTROL Manage Data] Ficha

Si desea exportar la tabla desde [!UICONTROL Manage Data] pestaña, necesita [Administrador](../administrator/user-management/user-management.md) permisos.

1. Clic **[!UICONTROL Manage Data** > ** Exportar datos **> **Exportación de datos sin procesar]**.
1. Verá un `Export List` de exportaciones de datos creadas recientemente, si las hay. Clic **[!UICONTROL Add Export]** para crear una exportación.
1. El `New Raw Data Export` se muestra. Aquí puede personalizar la exportación seleccionando o anulando la selección de columnas y filtros:

   * `Table` - El `Table` selecciona la tabla desde la que se exportan los datos. De forma predeterminada, esto muestra la tabla a la que se desplazó.
   * `Export Name` : En este campo, introduzca el nombre de la exportación. Por ejemplo: `Philadelphia - Daily Revenue`.
   * `Available Columns` : Este campo enumera las columnas (dimensiones) de la base de datos que están disponibles para su inclusión en la exportación. Para agregar una columna, haga clic en su nombre.
   * `Selected Columns` : Este campo enumera las columnas (dimensiones) incluidas actualmente en la exportación. Para quitar una columna, haga clic en su nombre.
   * `Filter` : Esta sección enumera los filtros aplicados actualmente a la exportación. Estos filtros se pueden cambiar, y también se pueden añadir nuevos filtros para exportar un conjunto de datos concreto.
   * Cuando termine, haga clic en **[!UICONTROL Export Data]**.

### Exportación a nivel de gráfico desde el panel

1. Haga clic en el icono de engranaje en la esquina superior derecha de cualquier gráfico.

1. Seleccionar `Raw Export` en el menú desplegable para mostrar el `Raw Export` diálogo.

1. Personalice la exportación eligiendo la opción `table`, `columns`, y `filters` para incluir o excluir. Consulte la sección anterior para obtener información más detallada sobre los campos de este módulo.

   >[!NOTE]
   >
   >La tabla que se muestra en la `Table` El campo es, de forma predeterminada, la tabla que alimenta el gráfico.

1. Cuando termine, haga clic en **[!UICONTROL Export Data]**.

Observe todo el proceso en el nivel de gráfico.

![](../assets/Chart-level_export.gif)

## Paso 2: Descarga de la exportación {#download}

La exportación comienza a procesarse inmediatamente después de completar las selecciones en la `Raw Data Export` diálogo. Como algunas exportaciones pueden ser de gran tamaño, están limitadas a 10 millones de filas y pueden tardar algún tiempo en ejecutarse.

Para comprobar si la exportación está lista, haga clic en **[!UICONTROL Raw Data Exports]** en la esquina superior derecha de la pantalla. Clic **[!UICONTROL Download]** para descargar un archivo comprimido `.csv` del archivo de exportación.

![](../assets/Downloading_export.gif)

## Paso 3: Acceso a exportaciones históricas {#historical}

Para ver las exportaciones anteriores, haga clic en **[!UICONTROL Raw Data Export]** en la esquina superior derecha de la pantalla. Se puede acceder a los informes pendientes y completados durante un máximo de siete días.
