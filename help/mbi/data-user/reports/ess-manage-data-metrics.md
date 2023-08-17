---
title: Creación de métricas
description: Aprenda a utilizar las métricas para crear gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Creación de métricas

>[!NOTE]
>
>Requiere [Permisos de administración](../../administrator/user-management/user-management.md).

Una métrica es una medida. En las estructuras SQL y de base de datos, una métrica es como una consulta almacenada durante un período de variable.

Entrada [!DNL Commerce Intelligence], puede utilizar las métricas para [crear gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por ejemplo, la métrica `revenue` es el número total de pedidos. La métrica `average customer revenue per order` es lo que gasta el cliente promedio por pedido.

Cuando se usan en los informes, las métricas se pueden analizar durante un periodo de tiempo especificado y [filtrada o segmentada](../../best-practices/segment-filter.md) por categorías diferentes. Considere la posibilidad de analizar los ingresos medios de los clientes agrupados por sexo, en este caso, `average customer revenue per order` es la métrica y el sexo es la agrupación.

## Definición de la métrica {#define}

1. Para crear una métrica, haga clic en **[!UICONTROL Data** > **Metrics]**.

1. Haga clic **[!UICONTROL Create New Metric]**.

1. En el menú desplegable, haga clic en la tabla que incluye la columna nativa o calculada que desee utilizar para la métrica.

1. Asigne un nombre a la métrica.

   Adobe recomienda un nombre que, de un vistazo, le indique cuál es la métrica. Por ejemplo: `Average Order Revenue`.

1. El siguiente paso es definir lo que hace la métrica. Mediante los menús desplegables, defina el funcionamiento de la métrica, el `operation` y una columna `date` dimensión:

   * Seleccione una operación:
      * `Count` : Esta operación cuenta el número de filas de una tabla de datos
      * `Max` - Max devuelve el valor máximo de una columna de datos específica
      * `Min` - Min devuelve el valor mínimo de una columna de datos específica
      * `Sum` : Esta operación suma los valores de una columna de datos específica
      * `Average` : Esta operación calcula la media de los valores de la columna de datos
      * `Count Distinct Value` : cuenta el número único de valores de una columna de datos específica
      * `Median` : Esta operación calcula la mediana de los valores de la columna de datos
      * `First and Third Quartiles` : Estas operaciones calculan los percentiles 25 y 75 de los valores de la columna de datos, respectivamente
      * `Tenth and Ninetieth Percentiles` : Estas operaciones calculan los percentiles 10 y 90 de los valores de la columna de datos, respectivamente

   * Seleccione una columna en la que realizar la operación. Por ejemplo, si desea encontrar los ingresos totales, debe realizar una operación de suma en la variable `order total` columna.

     Si está editando una métrica existente, también puede [cambiar la tabla operativa de la métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) en esta sección.

   * Elija una dimensión de fecha que se pueda usar para analizar la tendencia de la métrica. Por ejemplo, `order date`.

## Adición de filtros {#filters}

El `Filter` le permite crear un filtro o aplicar una [conjunto de filtros guardado](../../data-user/reports/ess-manage-data-filters.md) a su métrica.

Para el `average order revenue` métrica, no desea incluir ningún pedido de prueba que se haya realizado al configurar su tienda; esto nos daría un resultado impreciso. Puede aplicar un conjunto de filtros para eliminar esos pedidos del conjunto de datos. Una vez creado el filtro, se aplicará a todos los gráficos creados con esta métrica.

El `Filter Logic` es donde puede definir más detalladamente cómo debe comportarse una métrica.

* &quot;\[`A`\] o \[`B`\]&quot; permite cualquier dato que cumpla los filtros \[`A`\] O \[`B`\]
* &quot;\[`A`\] y \[`B`\]&quot; solo permite datos que cumplan ambos filtros \[`A`\] y \[`B`\]
* &quot;(\[`A`\] y \[`B`\]) O \[`C`\]&quot; solo permite datos que cumplan ambos filtros \[`A`\] y \[`B`\] o satisface el filtro \[`C`\] solo

## Añadir Dimension {#dimensions}

El [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) Esta sección muestra todas las dimensiones de datos disponibles para filtrar o agrupar; de forma predeterminada, todas las columnas de datos disponibles se muestran como dimensiones. Continuando con el ejemplo, si desea segmentar los ingresos por fuente de referencia, puede hacerlo aquí.

Además de enumerar todas las columnas de datos disponibles como dimensiones, [!DNL Commerce Intelligence] adivina a qué columnas se pueden agrupar. *Para segmentar o agrupar datos en informes*, las columnas deben marcarse como agrupables.

## Finalizando {#finish}

Además de definir cómo se comporta la métrica, también puede establecer niveles de permisos en la variable `User Rights` sección. While `Admin` Si los usuarios tienen acceso a todas las métricas, debe indicar los usuarios que pueden utilizar esta métrica marcando la casilla junto al grupo correspondiente.

Si está editando una métrica existente, puede ver una lista de gráficos (y a quién pertenecen) que utilizan esta métrica en el `Dependent Charts` sección.

Los cambios se guardan automáticamente y la métrica ya está lista.
