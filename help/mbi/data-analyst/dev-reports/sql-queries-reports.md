---
title: Traducción de consultas SQL a informes de Commerce Intelligence
description: Aprenda cómo se traducen las consultas SQL en las columnas calculadas y las métricas que utiliza en Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# Traducción de consultas SQL en Commerce Intelligence

¿Alguna vez se ha preguntado cómo se traducen las consultas SQL en las [columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md) e [informes](../../tutorials/using-visual-report-builder.md) que usa en [!DNL Commerce Intelligence]? Si usa mucho SQL, comprender cómo se traduce SQL en [!DNL Commerce Intelligence] le permite trabajar de forma más inteligente en [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) y aprovechar al máximo la plataforma [!DNL Commerce Intelligence].

Al final de este tema, se encuentra una **matriz de traducción** para cláusulas de consulta SQL y [!DNL Commerce Intelligence] elementos.

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

Este ejemplo abarca la mayoría de los casos de traducción, pero hay algunas excepciones. Sumérjase en, empezando por cómo se traduce la función `aggregate`.

## Funciones agregadas

Las funciones agregadas (por ejemplo, `count`, `sum`, `average`, `max`, `min`) en las consultas toman la forma de **agregaciones de métricas** o **agregaciones de columnas** en [!DNL Commerce Intelligence]. El factor diferenciador es si se requiere una unión para realizar la agregación.

Observe un ejemplo para cada uno de los elementos anteriores.

## Agregaciones de métricas {#aggregate}

Se requiere una métrica al agregar `within a single table`. Por ejemplo, es muy probable que la función de agregado `SUM(b)` de la consulta anterior esté representada por una métrica que suma la columna `B`. 

Observe un ejemplo específico de cómo se puede definir una métrica de `Total Revenue` en [!DNL Commerce Intelligence]. Observe la consulta siguiente que intenta traducir:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` (y sistema de informes `time range`) |

Vaya al generador de métricas haciendo clic en **[!UICONTROL Manage Data** > ** Métricas **> **Crear nueva métrica]**; primero debe seleccionar la tabla `source` adecuada, que en este caso es la tabla `orders`. A continuación, la métrica se configuraría como se muestra a continuación:

![Agregación de métrica](../../assets/Metric_aggregation.png)

## Agregaciones de columnas

Se requiere una columna calculada al agregar una columna unida desde otra tabla. Por ejemplo, puede tener una columna creada en la tabla `customer` llamada `Customer LTV`, que suma el valor total de todos los pedidos asociados con ese cliente en la tabla `orders`.

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

La configuración de esto en [!DNL Commerce Intelligence] requiere el uso de su administrador de Data Warehouse, donde creará una ruta de acceso entre las tablas `orders` y `customers` y, a continuación, creará una columna denominada `Customer LTV` en la tabla del cliente.

Observe cómo establecer una nueva ruta de acceso entre `customers` y `orders`. El objetivo final es crear una nueva columna agregada en la tabla `customers`, así que primero vaya a la tabla `customers` en su Data Warehouse y, a continuación, haga clic en **[!UICONTROL Create a Column** > ** Seleccionar una definición **> **SUMA]**.

A continuación, debe seleccionar la tabla de origen. Si existe una ruta de acceso a la tabla `orders`, simplemente selecciónela en la lista desplegable. Sin embargo, si está creando una nueva ruta, haga clic en **[!UICONTROL Create new path]** y aparecerá la siguiente pantalla:

![Crear nueva ruta](../../assets/Create_new_path.png)

Aquí debe considerar cuidadosamente la relación entre las dos tablas que está intentando unir. En este caso, hay potencialmente `Many` pedidos asociados con `One` cliente, por lo tanto la tabla `orders` se muestra en el lado `Many`, mientras que la tabla `customers` está seleccionada en el lado `One`.

>[!NOTE]
>
>En [!DNL Commerce Intelligence], un `path` equivale a un `Join` en SQL.

Una vez guardada la ruta, puede crear la columna `Customer LTV`. Consulte lo siguiente:

![Demostración animada del análisis de valor de duración de clientes mediante SQL](../../assets/Customer_LTV.gif)

Ahora que ha creado la nueva columna `Customer LTV` en su tabla `customers`, está listo para crear una [agregación de métrica](#aggregate) con esta columna (por ejemplo, para encontrar el LTV promedio por cliente). También puede `group by` o `filter` por la columna calculada en un informe usando las métricas existentes creadas en la tabla `customers`.

>[!NOTE]
>
>Para esto último, cada vez que genere una nueva columna calculada debe [agregar la dimensión a las métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de que esté disponible como `filter` o `group by`.

Ver [creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) con el administrador de Data Warehouse.

## `Group By` cláusulas

Las funciones de `Group By` en las consultas se representan a menudo en [!DNL Commerce Intelligence] como una columna utilizada para segmentar o filtrar un informe visual. Por ejemplo, vamos a revisar la consulta `Total Revenue` que exploró anteriormente, pero esta vez segmentemos los ingresos por el `coupon\_code` para comprender mejor qué cupones generan la mayor cantidad de ingresos.

Comience con la siguiente consulta:

| | |
|--- |--- |
| `SELECT coupon_code,` | Informe `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` (y sistema de informes `time range`) |
| `GROUP BY coupon_code` | Informe `group by` |

>[!NOTE]
>
>La única diferencia con respecto a la consulta con la que comenzó antes es la adición del &quot;coupon\_code&quot; como agrupado por._

Con la misma métrica `Total Revenue` que creó anteriormente, ya puede crear su informe de ingresos segmentado por código de cupón. Observe el gif que aparece a continuación y que muestra cómo configurar este informe visual con los datos de septiembre a noviembre:

![Ingresos por código de cupón](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

A veces, una consulta puede implicar varias agregaciones para calcular la relación entre columnas independientes. Por ejemplo, puede calcular el valor de pedido promedio en una consulta de una de las dos maneras siguientes:

* `AVG('order\_total')` O
* `SUM('order\_total')/COUNT('order\_id')`

El método anterior implicaría la creación de una nueva métrica que realice un promedio en la columna `order\_total`. Sin embargo, este último método se podría crear directamente en el Report Builder, suponiendo que ya se hayan configurado las métricas para calcular `Total Revenue` y `Number of orders`.

Retroceda un paso y observe la consulta general de `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (columna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (columna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (columna) / Operación de métrica (columna) |
| `FROM orders` | Tabla de métrica `source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Marca de tiempo de las métricas (e intervalo de tiempo de informes) |

Ahora suponga que ya tiene métricas configuradas para calcular `Total Revenue` y `Number of orders`. Dado que estas métricas existen, simplemente puede abrir `Report Builder` y crear un cálculo bajo demanda utilizando la característica `Formula`:

![Fórmula AOV](../../assets/AOV_forumula.gif)

## Ajuste

Si es un usuario de SQL con mucho peso, pensar en cómo se traducen las consultas en [!DNL Commerce Intelligence] le permite generar columnas calculadas, métricas e informes.

Para obtener una referencia rápida, consulte la siguiente matriz. Esto muestra el elemento [!DNL Commerce Intelligence] equivalente de una cláusula SQL y cómo se puede asignar a más de un elemento, dependiendo de cómo se utilice en la consulta.

## Elementos de Commerce Intelligence

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (con elementos de tiempo) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
