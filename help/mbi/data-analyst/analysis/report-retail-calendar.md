---
title: Creación de informes en un calendario comercial
description: Aprenda a configurar la estructura para utilizar un calendario de ventas minoristas 4-5-4 dentro de su [!DNL MBI] cuenta.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Creación de informes en un calendario comercial

Este artículo muestra cómo configurar la estructura para utilizar una [Calendario comercial 4-5-4](https://nrf.com/resources/4-5-4-calendar) dentro de su [!DNL MBI] cuenta. El Report Builder visual proporciona intervalos de tiempo, intervalos y configuraciones independientes increíblemente flexibles. Sin embargo, todos estos ajustes funcionan con el calendario mensual tradicional establecido.

Dado que muchos clientes modifican su calendario para utilizar fechas de venta minorista o contables, los pasos siguientes ilustran cómo trabajar con los datos y crear informes utilizando fechas de venta minorista. Aunque las siguientes instrucciones hacen referencia al calendario comercial 4-5-4, puede modificarlas para cualquier calendario específico que utilice su equipo, ya sea financiero o simplemente personalizado.

Antes de empezar, debe familiarizarse con [el Cargador de archivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) y asegúrese de que ha alargado el `.csv` archivo. Esto garantiza que las fechas cubran todos los datos históricos y las inserten en el futuro.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Primeros pasos

Puede [descargar](../../assets/454-calendar.csv) a `.csv` versión del calendario comercial 4-5-4 para los años de venta al por menor de 2014 a 2017. Es posible que tenga que ajustar este archivo según su calendario comercial interno y ampliar el intervalo de fechas para que sea compatible con el lapso de tiempo histórico y actual. Después de descargar el archivo, use el Cargador de archivos para crear una tabla de Calendario comercial en su [!DNL MBI] Data Warehouse. Si utiliza una versión sin modificar del calendario comercial 4-5-4, asegúrese de que la estructura y los tipos de datos de los campos de esta tabla coinciden con los siguientes:

| Nombre de columna | Tipo de datos de columna | Clave principal |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Hasta 255 caracteres) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Columnas para crear

* **sales\_order** tabla
   * `INPUT` `created\_at` (aaaa-mm-dd 00):00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendario comercial** tabla de carga de archivos
   * **Fecha actual**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL Tipo de datos]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >El `now()` La función anterior es específica de PostgreSQL. Aunque la mayoría [!DNL MBI] Los almacenes de datos de están alojados en PostgreSQL, algunos pueden estar alojados en Redshift. Si el cálculo anterior devuelve un error, es posible que tenga que utilizar la función Redshift `getdate()` en lugar de `now()`.
   * **Año minorista actual** (Debe ser creado por el analista de asistencia)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **¿Incluido en el año minorista actual? (Sí/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo de datos]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **¿Incluido en el año comercial anterior? (Sí/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo de datos]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** tabla
   * **Creado\_a las (año comercial)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleccione una [!UICONTROL table]: `Retail Calendar`
      * Seleccione una [!UICONTROL column]: `Year Retail`
   * **Creado\_en (semana de venta minorista)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: ventas\_pedido.\[INPUT\] created\_at (aaaa-mm-dd 00:00:00
         * [!UICONTROL One]: Calendario comercial.Fecha comercial
      * Seleccione una [!UICONTROL table]: `Retail Calendar`
      * Seleccione una [!UICONTROL column]: `Week Retail`
   * **Creado\_en (mes comercial)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleccione una [!UICONTROL table]: `Retail Calendar`
      * Seleccione una [!UICONTROL column]: `Month Number Retail`
   * **¿Incluir en el año comercial anterior? (Sí/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: minorista `Calendar.Date Retail`
      * Seleccione una [!UICONTROL table]: `Retail Calendar`
      * Seleccione una [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **¿Incluir en el año comercial actual? (Sí/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: minorista `Calendar.Date Retail`
      * Seleccione una [!UICONTROL table]: `Retail Calendar`
      * Seleccione una [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Métricas

Nota: No se necesitan métricas nuevas para este análisis. Sin embargo, asegúrese de lo siguiente [añada las nuevas columnas creadas en la tabla sales\_order como dimensiones](../data-warehouse-mgr/manage-data-dimensions-metrics.md) para todas las métricas de la tabla sales\_order antes de continuar con los informes.

## Informes

* **Pedidos semanales: calendario de ventas minoristas (año)**
   * Métrica `A`: `2017`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Creado\_en (año comercial) = 2017
   * Métrica `B`: `2016`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Creado\_en (año comercial) = 2016
   * Métrica `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * Desactivar `multiple Y-axes`

* **Resumen del calendario de ventas minoristas (año de venta minorista actual por mes)**
   * Métrica `A`: `Revenue`
      * 
         [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **Resumen del calendario de ventas minoristas (año de venta minorista anterior por mes)**
   * Métrica `A`: `Revenue`
      * 
         [!UICONTROL Métrica]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `B`: `Orders`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Métrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## Pasos siguientes

Lo anterior describe cómo configurar un calendario comercial para que sea compatible con cualquier métrica creada en su `sales\_order` tabla (como `Revenue` o `Orders`). También puede ampliarlo para que admita el calendario comercial para las métricas creadas en cualquier tabla. El único requisito es que esta tabla tenga un campo de fecha y hora válido que se pueda usar para unirse a la tabla Calendario comercial.

Por ejemplo, para ver las métricas de nivel de cliente en un calendario de venta minorista 4-5-4, cree un `Same Table` cálculo en la `customer\_entity` tabla, similar a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descrito anteriormente. Puede utilizar esta columna para reproducir el `One to Many` Cálculos JOINED\_COLUMN (como `Created_at (retail year)` y `Include in previous retail year? (Yes/No)` al unirse a `customer\_entity` a la tabla `Retail Calendar` tabla.

No se olvide de [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.
