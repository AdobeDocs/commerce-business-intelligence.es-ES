---
title: Exportar datos sin procesar
description: Aprenda a exportar registros de su  [!DNL Commerce Intelligence] Data Warehouse para obtener más información sobre lo que alimenta su tablero.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Developer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
TQID: https://experienceleague.adobe.com/8n0DUwkiI1BVF5612vCd4jFWx7jwWlfOHg2K3hgWkco
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
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
source-wordcount: 491
ht-degree: 0%

---

# Exportar datos sin procesar

Con las exportaciones de datos sin procesar, puede exportar registros de su Data Warehouse para obtener una visión más detallada de lo que alimenta su panel. Además, las exportaciones de datos sin procesar pueden ayudarle a [identificar discrepancias en los datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

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

![Demostración animada de la exportación de datos sin procesar de un gráfico](../assets/Chart-level_export.gif)

## Paso 2: Descarga de la exportación {#download}

La exportación empezará a procesarse inmediatamente después de completar las selecciones en el cuadro de diálogo `Raw Data Export`. Como algunas exportaciones pueden ser de gran tamaño, están limitadas a 10 millones de filas y pueden tardar algún tiempo en ejecutarse.

Para comprobar si la exportación está lista, haga clic en **[!UICONTROL Raw Data Exports]**, en la esquina superior derecha de la pantalla. Haga clic en **[!UICONTROL Download]** para descargar un archivo comprimido `.csv` de su exportación.

![Demostración animada de la descarga de un archivo CSV exportado](../assets/Downloading_export.gif)

## Paso 3: Acceso a exportaciones históricas {#historical}

Para ver las exportaciones anteriores, haga clic en **[!UICONTROL Raw Data Export]**, en la esquina superior derecha de la pantalla. Se puede acceder a los informes pendientes y completados durante un máximo de siete días.
