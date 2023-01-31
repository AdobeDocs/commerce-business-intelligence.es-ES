---
title: Traducción de consultas SQL en [!DNL MBI] informes
description: Descubra cómo se traducen las consultas SQL en las columnas calculadas y las métricas que utiliza en [!DNL MBI].
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Traducir consultas SQL en MBI

Nunca se ha preguntado cómo se traducen las consultas SQL en la variable [columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md), [métricas](../../data-user/reports/ess-manage-data-metrics.md)y [informes](../../tutorials/using-visual-report-builder.md) utiliza en [!DNL MBI]? Si es un usuario SQL pesado, comprenda cómo se traduce SQL en [!DNL MBI] le permitirá trabajar de forma más inteligente en el [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) y aproveche al máximo las [!DNL MBI] plataforma.

Al final de este artículo, hemos incluido un **matriz de traducción** para cláusulas de consulta SQL y [!DNL MBI] elementos.

Empezamos mirando una consulta general:

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | Informe `group by` |
| `SUM(b)` | `Aggregate function` (columna) |
| `FROM c` | `Source` tabla |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Informe `time frame` |
| `GROUP BY a` | Informe `group by` |

Este ejemplo cubre la mayoría de los casos de traducción, pero hay algunas excepciones. Hagamos una inmersión, empezando por cómo `aggregate` está traducida.

## Funciones agregadas

Funciones agregadas (por ejemplo, `count`, `sum`, `average`, `max`, `min`) en consultas que toman la forma de **agregaciones de métricas** o **agregaciones de columnas** en [!DNL MBI]. El factor de diferenciación es si se requiere o no una unión para realizar la agregación.

Veamos un ejemplo de cada uno de los anteriores.

## Acumulaciones de métricas {#aggregate}

Se requiere una métrica al agregar `within a single table`. Por ejemplo, la variable `SUM(b)` la función de agregado de la consulta anterior probablemente estaría representada por una métrica que suma una columna `B`. 

Veamos un ejemplo específico de cómo `Total Revenue` puede definirse en [!DNL MBI]. Eche un vistazo a la siguiente consulta que intentaremos traducir:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Métrica `timestamp` (y `time range`) |

Vaya al creador de métricas haciendo clic en **[!UICONTROL Manage Data** > ** Métricas **> **Crear nueva métrica]**, primero debe seleccionar el `source` que, en este caso, es la `orders` tabla. A continuación, la métrica se configuraría como se muestra a continuación:

![Agregación de métricas](../../assets/Metric_aggregation.png)

## Agregaciones de columnas

Se requiere una columna calculada al agregar una columna que se une desde otra tabla. Por ejemplo, puede tener una columna integrada en su `customer` tabla denominada `Customer LTV`, que suma el valor total de todos los pedidos asociados con ese cliente en la variable `orders` tabla.

La consulta para esta agregación puede tener un aspecto similar al siguiente:

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | Propietario agregado |
| `SUM(o.order_total) as "Customer LTV"` | Operación agregada (columna) |
| `FROM customers c` | Agregar tabla de propietario |
| `JOIN orders o` | Tabla de origen de agregación |
| `ON c.customer_id = o.customer_id` | Ruta |
| `WHERE o.status = 'success'` | Filtro agregado |

Configurar esto en [!DNL MBI] requiere el uso del administrador de Datas Warehouse, donde creará una ruta entre `orders` y `customers` a continuación, cree una nueva columna llamada `Customer LTV` en la tabla del cliente.

En primer lugar, veamos cómo establecer un nuevo camino entre `customers` y `orders`. Nuestro objetivo final es crear una nueva columna agregada en la variable `customers` , por lo que en primer lugar vaya a la tabla `customers` en la Data Warehouse y, a continuación, haga clic en **[!UICONTROL Create a Column** > ** Seleccionar una definición **> **SUMA]**.

A continuación, debe seleccionar la tabla de origen. Si ya existe una ruta de acceso a su `orders` , simplemente selecciónela en la lista desplegable. Sin embargo, si está creando una ruta nueva, haga clic en **[!UICONTROL Create new path]** y se le presentará la siguiente pantalla:

![Crear nueva ruta](../../assets/Create_new_path.png)

Aquí debe considerar cuidadosamente la relación entre las dos tablas que está tratando de unir. En este caso, es posible que `Many` pedidos asociados `One` cliente, por lo tanto, la variable `orders` se muestra en la `Many` del lado, mientras que el `customers` tabla seleccionada en el `One` lado.

>[!NOTE]
>
>En [!DNL MBI], *ruta* es equivalente a un `Join` en SQL.

Una vez guardada la ruta, se configurará para crear la nueva `Customer LTV` columna! Eche un vistazo a lo siguiente:

![](../../assets/Customer_LTV.gif)

Ahora que ha creado el nuevo `Customer LTV` en la columna `customers` , está listo para crear un [agregación de métricas](#aggregate) uso de esta columna (por ejemplo, para encontrar el promedio de LTV por cliente), o simplemente `group by` o `filter` por la columna calculada en un informe utilizando métricas existentes basadas en la variable `customers` tabla.

>[!NOTE]
>
>Para este último, cada vez que cree una nueva columna calculada deberá [añadir la dimensión a las métricas existentes](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de que esté disponible como `filter` o `group by`.

Consulte [creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) con su administrador de Datas Warehouse.

## `Group By` cláusulas

`Group By` las funciones en las consultas a menudo se representan en [!DNL MBI] como columna utilizada para segmentar o filtrar un informe visual. Por ejemplo, volvamos a examinar la `Total Revenue` consulta que hemos explorado anteriormente, pero esta vez Vamos a segmentar los ingresos por el `coupon\_code` para comprender mejor qué cupones generan la mayor cantidad de ingresos.

En primer lugar, empezamos con la siguiente consulta:

|  |  |
|--- |--- |
| `SELECT coupon_code,` | Informe `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(columna) |
| `FROM orders` | `Metric source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Métrica `timestamp` (y `time range`) |
| `GROUP BY coupon_code` | Informe `group by` |

>[!NOTE]
>
>La única diferencia con respecto a la consulta con la que empezamos antes es la adición del &quot;coupon\_code&quot; como grupo por._

Usando el mismo `Total Revenue` que hemos creado anteriormente, ¡ya estamos listos para crear nuestro informe de ingresos segmentados por código de cupón! Eche un vistazo a la siguiente gif que muestra cómo configurar este informe visual mirando los datos de septiembre a noviembre:

![Ingresos por código de cupón](../../assets/Revenue_by_coupon_code.gif)

## Fórmulas

En algunos casos, una consulta puede implicar múltiples agregaciones para calcular la relación entre columnas independientes. Por ejemplo, puede calcular el valor de pedido promedio en una consulta de una de las dos maneras siguientes:

* `AVG('order\_total')` O
* `SUM('order\_total')/COUNT('order\_id')`

El método anterior implicaría la creación de una nueva métrica que realiza un promedio en la variable `order\_total` para abrir el Navegador. Sin embargo, este último método se puede crear directamente en el creador de informes, suponiendo que ya tenga métricas configuradas para calcular la variable `Total Revenue` y `Number of orders`.

Retrocedamos un paso y veamos la consulta general de `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Métrica `operation` (columna) |
| `COUNT(order_id) as "Number of orders"` | Métrica `operation` (columna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Métrica `operation` (columna) / Operación de métrica (columna) |
| `FROM orders` | Métrica `source` tabla |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Métrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Marca de tiempo de métrica (e intervalo de tiempo de informes) |

Y supongamos que ya tenemos métricas configuradas para calcular la variable `Total Revenue` y `Number of orders`. Dado que estas métricas ya existen, simplemente podemos abrir el `Report Builder` y crear un cálculo ad hoc utilizando la variable `Formula` función:

![Fórmula AOV](../../assets/AOV_forumula.gif)

## Ajuste

Como mencionamos al principio de este artículo, si es un usuario SQL pesado, piense en cómo se traducen las consultas en [!DNL MBI] le permite crear columnas, métricas e informes calculados.

Para una referencia rápida, consulte la matriz siguiente. Muestra el equivalente de una cláusula SQL [!DNL MBI] y cómo se puede asignar a más de un elemento, según cómo se utilice en la consulta.

## Elementos de MBI

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—|—|—|—|—|—|—| |`SELECT`|X|-|X|-|-|X|-| |`FROM`|-|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-|-| |`WHERE` (con elementos de tiempo)|-|-|-|X|-|-|-| |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|
