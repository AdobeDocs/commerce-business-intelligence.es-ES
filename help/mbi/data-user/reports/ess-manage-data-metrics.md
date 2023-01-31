---
title: Crear métricas
description: Aprenda a utilizar las métricas para crear gráficos.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Crear métricas

>[!NOTE]
>
>Requiere [Permisos de administrador](../../administrator/user-management/user-management.md).

En pocas palabras, una métrica es una medición. En las estructuras SQL y de base de datos, una métrica es como una consulta almacenada durante un período de tiempo variable.

En [!DNL MBI], puede usar métricas para [crear gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por ejemplo, la métrica `revenue` es la cantidad total de pedidos. La métrica `average customer revenue per order` es lo que el cliente promedio gasta por pedido.

Cuando se usan en los informes, las métricas se pueden analizar en un período de tiempo especificado y [filtrados o segmentados](../../best-practices/segment-filter.md) por categorías diferentes. Considere analizar los ingresos promedio de los clientes agrupados por sexo (en este caso, `average customer revenue per order` es la métrica y el género es la agrupación.

## Definición de la métrica {#define}

1. Para crear una métrica nueva, haga clic en **[!UICONTROL Data** > **Metrics]**.

1. Haga clic en **[!UICONTROL Create New Metric]**.

1. En el menú desplegable, haga clic en la tabla que incluye la columna nativa o calculada que desee usar para la métrica.

1. Asigne un nombre a la métrica.

   Recomendamos un nombre que, de un vistazo, le indique cuál es la métrica. Por ejemplo: `Average Order Revenue`.

1. El siguiente paso es definir lo que hace la métrica. En los menús desplegables, defina la operación de la métrica y la variable `operation` y `date` dimensión:

   * Elija una operación:
      * `Count` - Esta operación cuenta el número de filas de una tabla de datos
      * `Max` - Max devuelve el valor máximo de una columna de datos específica
      * `Min` - Min devuelve el valor mínimo de una columna de datos específica
      * `Sum` - Esta operación resume los valores de una columna de datos específica
      * `Average` - Esta operación calcula el promedio de los valores de la columna de datos
      * `Count Distinct Value` - Cuenta el número único de valores en una columna de datos específica
      * `Median` - Esta operación calcula la mediana de los valores de la columna de datos
      * `First and Third Quartiles` - Estas operaciones calculan los percentiles 25 y 75 de los valores de la columna de datos, respectivamente.
      * `Tenth and Ninetieth Percentiles` - Estas operaciones calculan los percentiles 10 y 90 de los valores de la columna de datos, respectivamente.
   * Elija una columna en la que realizar la operación. Por ejemplo, si desea encontrar los ingresos totales, debe realizar una operación de suma en la variable `order total` para abrir el Navegador.

      Si está editando una métrica existente, también puede [cambiar la tabla operativa de la métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) en esta sección.

   * Elija una dimensión de fecha que se pueda usar para analizar la tendencia de la métrica. Por ejemplo, `order date`.


## Adición de filtros {#filters}

La variable `Filter` permite crear un nuevo filtro o aplicar un [conjunto de filtros guardados](../../data-user/reports/ess-manage-data-filters.md) a su métrica.

Para nuestra `average order revenue` , no queremos incluir ningún pedido de prueba que se haya podido realizar al configurar nuestra tienda, lo que nos daría un resultado inexacto. Podemos aplicar un conjunto de filtros para eliminar esos pedidos del conjunto de datos. Una vez creado el filtro, se aplicará a todos los gráficos creados con esta métrica.

La variable `Filter Logic` es donde puede definir aún más el comportamiento de una métrica.

* &quot;\[`A`\] o \[`B`\]&quot; permitirá cualquier dato que cumpla los filtros \[`A`\] O \[`B`\]
* &quot;\[`A`\] y \[`B`\]&quot; solo permitirá datos que cumplan ambos filtros \[`A`\] y \[`B`\]
* &quot;(\[`A`\] y \[`B`\]) O \[`C`\]&quot; solo permite datos que satisfacen ambos filtros \[`A`\] y \[`B`\] o cumple el filtro \[`C`\] solo

## Adición de Dimension {#dimensions}

La variable [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) muestra todas las dimensiones de datos disponibles para su filtrado o agrupación; de forma predeterminada, todas las columnas de datos disponibles aparecen como dimensiones. Siguiendo con nuestro ejemplo, si quisiéramos segmentar nuestros ingresos por fuente de referencia, podríamos hacerlo aquí.

Además de enumerar todas las columnas de datos disponibles como dimensiones, [!DNL MBI] también tomará una suposición sobre qué columnas se pueden agrupar. *Para segmentar o agrupar datos en informes*, las columnas deben marcarse como agrupables.

## Finalizando {#finish}

Además de definir el comportamiento de la métrica, también puede establecer niveles de permiso en la variable `User Rights` para obtener más información. While `Admin` Los usuarios tienen acceso a todas las métricas, debe indicar los usuarios que pueden usar esta métrica marcando la casilla junto al grupo correspondiente.

Si está editando una métrica existente, puede ver una lista de gráficos (y a quién pertenece) que utilizan esta métrica en la `Dependent Charts` para obtener más información.

Los cambios se guardan automáticamente y la métrica ya está lista.
