---
title: Informes en un calendario minorista
description: Aprenda a configurar la estructura para utilizar un calendario comercial 4-5-4 dentro de su [!DNL MBI] cuenta.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Creación de informes en un calendario comercial

En este artículo, se muestra cómo configurar la estructura para utilizar un [Calendario comercial 4-5-4](https://nrf.com/resources/4-5-4-calendar) dentro de su [!DNL MBI] cuenta. El Creador de informes visuales proporciona intervalos de tiempo, intervalos y configuraciones independientes increíblemente flexibles. Nuestro equipo también puede ayudarle a cambiar el día de inicio de la semana para que se ajuste a sus preferencias comerciales. Sin embargo, todos estos ajustes funcionan con el calendario mensual tradicional establecido.

Debido a que muchos de nuestros clientes modifican su calendario para utilizar fechas de venta minorista o cuentas, los siguientes pasos ilustran cómo trabajar con sus datos y crear informes utilizando fechas de venta minorista. Aunque las instrucciones siguientes hacen referencia al calendario comercial 4-5-4, puede modificarlo para cualquier calendario específico que use su equipo, ya sea financiero o simplemente un intervalo de tiempo personalizado.

Antes de comenzar, debe familiarizarse con [el Cargador de archivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) y asegúrese de que ha alargado el `.csv` para que las fechas abarquen todos los datos históricos, así como para insertar las fechas en el futuro.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introducción

Puede [descargar](../../assets/454-calendar.csv) a `.csv` versión del calendario comercial 4-5-4 para los años minoristas 2014 a 2017. Tenga en cuenta que es posible que tenga que ajustar este archivo según su calendario comercial interno, así como ampliar el intervalo de fechas para admitir su lapso de tiempo histórico y actual. Después de descargar el archivo, use el cargador de archivos para crear una tabla de calendario comercial en su [!DNL MBI] almacén de datos. Si utiliza una versión no modificada del calendario comercial 4-5-4, asegúrese de que la estructura y los tipos de datos de los campos de esta tabla coinciden con los siguientes:

| Nombre de columna | Tipo de datos de columna | Clave principal |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Hasta 255 caracteres) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style=&quot;table-layout:auto&quot;}

## Columnas que crear

* **sales\_order** tabla
   * `INPUT` `created\_at` (aaaa-mm-dd 00:00:00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendario comercial** tabla de carga de archivos
   * **Fecha actual**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL DataType]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >La variable `now()` es específica de PostgreSQL. Aunque la mayoría [!DNL MBI] los almacenes de datos están alojados en PostgreSQL; algunos pueden estar alojados en Redshift. Si el cálculo anterior devuelve un error, es posible que necesite utilizar la función Redshift `getdate()` en lugar de `now()`.
   * **Año minorista actual** (Debe crearlo un analista de asistencia técnica)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **¿Se incluye en el año minorista actual? (Sí/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL DataType]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **¿Incluido en el año anterior de venta al por menor? (Sí/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL DataType]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** tabla
   * **Creado\_at (año minorista)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleccione un [!UICONTROL table]: `Retail Calendar`
      * Seleccione un [!UICONTROL column]: `Year Retail`
   * **Creado\_at (semana de venta minorista)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]:sales\_order.\[INPUT\] creado\_at (aaaa-mm-dd 00:00:00
         * [!UICONTROL One]:Calendario comercial.Retención de fechas
      * Seleccione un [!UICONTROL table]: `Retail Calendar`
      * Seleccione un [!UICONTROL column]: `Week Retail`
   * **Creado\_at (mes de venta minorista)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleccione un [!UICONTROL table]: `Retail Calendar`
      * Seleccione un [!UICONTROL column]: `Month Number Retail`
   * **¿Se incluye en el año minorista anterior? (Sí/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Comercial `Calendar.Date Retail`
      * Seleccione un [!UICONTROL table]: `Retail Calendar`
      * Seleccione un [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **¿Incluir en el año minorista actual? (Sí/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Ruta -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Comercial `Calendar.Date Retail`
      * Seleccione un [!UICONTROL table]: `Retail Calendar`
      * Seleccione un [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Métricas

Nota: No se necesitan métricas nuevas para este análisis. Sin embargo, asegúrese de [añada las nuevas columnas que haya creado en la tabla sales\_order como dimensiones](../data-warehouse-mgr/manage-data-dimensions-metrics.md) para todas las métricas de la tabla sales\_order antes de continuar con los informes.

## Informes

* **Pedidos semanales - calendario minorista (año 2006)**
   * Métrica `A`: `2017`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Creado\_at (año minorista) = 2017
   * Métrica `B`: `2016`
      * [!UICONTROL Metric]: Número de pedidos
      * [!UICONTROL Filter]:
         * Creado\_at (año minorista) = 2016
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

* **Resumen del calendario comercial (año minorista actual por mes)**
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

* **Resumen del calendario comercial (año minorista anterior por mes)**
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

Lo anterior describe cómo configurar un calendario comercial para que sea compatible con cualquier métrica creada en su `sales\_order` (por ejemplo,`Revenue` y `Orders`), pero también puede ampliarlo para que admita el calendario comercial de las métricas creadas en cualquier tabla. El único requisito es que esta tabla tenga un campo de fecha y hora válido que se pueda usar para unirse a la tabla de calendario comercial.

Por ejemplo, para ver las métricas de nivel de cliente en un calendario comercial 4-5-4, cree un nuevo `Same Table` en el `customer\_entity` tabla, similar a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descrito anteriormente. A continuación, puede utilizar esta columna para reproducir todas las `One to Many` Cálculos JOINED\_COLUMN (como `Created_at (retail year)` y `Include in previous retail year? (Yes/No)` uniéndose a la `customer\_entity` a `Retail Calendar` tabla.

No olvide [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.
