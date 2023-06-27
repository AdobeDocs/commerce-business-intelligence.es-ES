---
title: Traducción de consultas SQL a informes de Commerce Intelligence
description: Descubra cómo se traducen las consultas SQL en las columnas calculadas y las métricas que utiliza en Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: fa65bd909495d4d73cabbc264e9a47b3e0a0da3b
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Traducción de consultas SQL en Commerce Intelligence

Alguna vez se ha preguntado cómo se traducen las consultas SQL en la [columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md), y [informes](../../tutorials/using-visual-report-builder.md) que usa en [!DNL Commerce Intelligence]? Si es un usuario de SQL con muchos recursos, le resultará muy útil entender cómo se traduce SQL en [!DNL Commerce Intelligence] le permite trabajar de forma más inteligente en [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) y sacar el máximo partido a [!DNL Commerce Intelligence] plataforma.

Al final de este tema, encontrará una **matriz de traducción** para cláusulas de consulta SQL y [!DNL Commerce Intelligence] elementos.

Comience por ver una consulta general:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Informe `group by` |
| `SUM(b)` | `Aggregate function` (columna) |
| `FROM c` | `Source` tabla |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Informe `time frame` |
| `GROUP BY a` | Informe `group by` |

Este ejemplo abarca la mayoría de los casos de traducción, pero hay algunas excepciones. Sumergirse, empezando por cómo el `aggregate` función traducida.

## Funciones agregadas

Funciones agregadas (por ejemplo, `count`, `sum`, `average`, `max`, `min`) en las consultas toman la forma de **agregaciones de métricas** o **agregaciones de columnas** in [!DNL Commerce Intelligence]. El factor diferenciador es si se requiere una unión para realizar la agregación.

Observe un ejemplo para cada uno de los elementos anteriores.

## Agregaciones de métricas {#aggregate}

Se requiere una métrica al agregar `within a single table`. Por ejemplo, la variable `SUM(b)` la función de agregado de la consulta anterior probablemente se representaría mediante una métrica que suma una columna `B`. 

Observe un ejemplo específico de cómo una `Total Revenue` La métrica de se puede definir en [!DNL Commerce Intelligence]. Observe la consulta siguiente que intenta traducir:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` (y presentación de informes `time range`) |

Vaya al creador de métricas haciendo clic en **[!UICONTROL Manage Data** > ** Métricas **> **Crear nueva métrica]**, primero debe seleccionar la opción `source` , que en este caso es la `orders` tabla. A continuación, la métrica se configuraría como se muestra a continuación:

![Agregación de métricas](../../assets/Metric_aggregation.png)

## Agregaciones de columnas

Se requiere una columna calculada al agregar una columna unida desde otra tabla. Por ejemplo, puede tener una columna creada en su `customer` tabla llamada `Customer LTV`, que suma el valor total de todos los pedidos asociados con ese cliente en el `orders` tabla.

La consulta de esta agregación puede tener un aspecto similar al siguiente:

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Propietario agregado |
| `SUM(o.order_total) as "Customer LTV"` | Operación de agregado (columna) |
| `FROM customers c` | Tabla de propietario agregada |
| `JOIN orders o` | Tabla de origen de agregación |
| `ON c.customer_id = o.customer_id` | Ruta |
| `WHERE o.status = 'success'` | Filtro agregado |

Configuración de esto en [!DNL Commerce Intelligence] requiere el uso del administrador de Datas Warehouse, donde puede crear una ruta entre las `orders` y `customers` luego cree una columna llamada `Customer LTV` en la tabla del cliente.

Observe cómo establecer una nueva ruta entre las variables `customers` y `orders`. El objetivo final es crear una nueva columna agregada en la variable `customers` , así que primero vaya a la `customers` en la Data Warehouse y haga clic en **[!UICONTROL Create a Column** > ** Seleccionar una definición **> **SUM]**.

A continuación, debe seleccionar la tabla de origen. Si existe una ruta a su `orders` , simplemente selecciónelo en la lista desplegable. Sin embargo, si está creando una nueva ruta, haga clic en **[!UICONTROL Create new path]** y se le mostrará la siguiente pantalla:

![Crear nueva ruta](../../assets/Create_new_path.png)

Aquí debe considerar cuidadosamente la relación entre las dos tablas que está intentando unir. En este caso, existen `Many` pedidos asociados a `One` cliente, por lo tanto, `orders` La tabla aparece en la `Many` mientras que el `customers` tabla seleccionada en la `One` lado.

>[!NOTE]
>
>Entrada [!DNL Commerce Intelligence], a `path` es equivalente a `Join` en SQL.

Una vez guardada la ruta, puede crear el `Customer LTV` columna! Consulte lo siguiente:

![](../../assets/Customer_LTV.gif)

Ahora que ha creado el nuevo `Customer LTV` en la columna `customers` , está listo para crear un [agregación de métricas](#aggregate) mediante esta columna (por ejemplo, para buscar el LTV promedio por cliente). También puede `group by` o `filter` por la columna calculada en un informe utilizando métricas existentes creadas en la variable `customers` tabla.

>[!NOTE]
>
>Para esto último, cada vez que cree una nueva columna calculada, debe [añadir la dimensión a las métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de que esté disponible como `filter` o `group by`.

Consulte [creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) con el administrador de Datas Warehouse.

## `Group By` cláusulas

`Group By` Las funciones de las consultas suelen representarse en [!DNL Commerce Intelligence] como una columna utilizada para segmentar o filtrar un informe visual. Por ejemplo, volvamos a visitar la `Total Revenue` consulta que ha explorado anteriormente, pero esta vez segmente los ingresos por `coupon\_code` para comprender mejor qué cupones son los que generan la mayor cantidad de ingresos.

Comience con la siguiente consulta:

| | |
|--- |--- |
| `SELECT coupon_code,` | Informe `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` (y presentación de informes `time range`) |
| `GROUP BY coupon_code` | Informe `group by` |

>[!NOTE]
>
>La única diferencia con respecto a la consulta con la que comenzó antes es la adición del &quot;coupon\_code&quot; como agrupado por._

Usar el mismo `Total Revenue` métrica que ha creado anteriormente, ahora está listo para crear su informe de ingresos segmentado por código de cupón. Observe el gif que aparece a continuación y que muestra cómo configurar este informe visual con los datos de septiembre a noviembre:

![Ingresos por código de cupón](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

A veces, una consulta puede implicar varias agregaciones para calcular la relación entre columnas independientes. Por ejemplo, puede calcular el valor de pedido promedio en una consulta de una de las dos maneras siguientes:

* `AVG('order\_total')` O
* `SUM('order\_total')/COUNT('order\_id')`

El método anterior implicaría la creación de una nueva métrica que realice un promedio en el `order\_total` columna. Sin embargo, este último método se podría crear directamente en el Report Builder, suponiendo que ya se hayan configurado métricas para calcular el `Total Revenue` y `Number of orders`.

Retroceda un paso y observe la consulta general de `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (columna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (columna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (columna) / Operación de métrica (columna) |
| `FROM orders` | Métrica `source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Marca de tiempo de las métricas (e intervalo de tiempo de informes) |

Ahora, supongamos que ya ha configurado métricas para calcular el `Total Revenue` y `Number of orders`. Dado que estas métricas existen, simplemente puede abrir el `Report Builder` y cree un cálculo bajo demanda utilizando `Formula` función:

![Fórmula AOV](../../assets/AOV_forumula.gif)

## Ajuste

Si es un usuario de SQL con muchas tareas, piense en cómo se traducen las consultas en [!DNL Commerce Intelligence] permite crear columnas calculadas, métricas e informes.

Para obtener una referencia rápida, consulte la siguiente matriz. Muestra el equivalente de una cláusula SQL [!DNL Commerce Intelligence] y cómo se puede asignar a más de un elemento, según cómo se utilice en la consulta.

## Commerce Intelligence Elements

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (con elementos de tiempo) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
