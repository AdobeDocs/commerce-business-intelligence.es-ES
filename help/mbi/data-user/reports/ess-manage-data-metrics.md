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
>Requiere [permisos de administrador](../../administrator/user-management/user-management.md).

Una métrica es una medida. En las estructuras SQL y de base de datos, una métrica es como una consulta almacenada durante un período de variable.

En [!DNL Commerce Intelligence], puede usar métricas para [crear gráficos](../../data-user/reports/ess-rpt-build-visual.md). Por ejemplo, la métrica `revenue` es el número total de pedidos. La métrica `average customer revenue per order` es lo que el cliente promedio gasta por pedido.

Cuando se usan en los informes, las métricas se pueden analizar en un período de tiempo especificado y [filtrar o segmentar](../../best-practices/segment-filter.md) por categorías diferentes. Considere la posibilidad de analizar los ingresos promedio de los clientes agrupados por sexo: en este caso, `average customer revenue per order` es la métrica y género es la agrupación.

## Definición de la métrica {#define}

1. Para crear una métrica, haga clic en **[!UICONTROL Data** > **Metrics]**.

1. Haga clic en **[!UICONTROL Create New Metric]**.

1. En el menú desplegable, haga clic en la tabla que incluye la columna nativa o calculada que desee utilizar para la métrica.

1. Asigne un nombre a la métrica.

   Adobe recomienda un nombre que, de un vistazo, le indique cuál es la métrica. Por ejemplo: `Average Order Revenue`.

1. El siguiente paso es definir lo que hace la métrica. Mediante los menús desplegables, defina la operación de la métrica, la columna `operation` y una dimensión `date`:

   * Seleccione una operación:
      * `Count`: esta operación cuenta el número de filas de una tabla de datos
      * `Max` - Máximo devuelve el valor máximo de una columna de datos específica
      * `Min` - Mínimo devuelve el valor mínimo de una columna de datos específica
      * `Sum`: esta operación suma los valores de una columna de datos específica
      * `Average`: esta operación calcula el promedio de los valores de la columna de datos
      * `Count Distinct Value`: esto cuenta el número único de valores en una columna de datos específica
      * `Median`: esta operación calcula la mediana de los valores de la columna de datos
      * `First and Third Quartiles`: estas operaciones calculan los percentiles 25 y 75 de los valores de la columna de datos, respectivamente
      * `Tenth and Ninetieth Percentiles`: estas operaciones calculan los percentiles 10 y 90 de los valores de la columna de datos, respectivamente

   * Seleccione una columna en la que realizar la operación. Por ejemplo, si desea encontrar los ingresos totales, debe realizar una operación de suma en la columna `order total`.

     Si está editando una métrica existente, también puede [cambiar la tabla operativa de la métrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) en esta sección.

   * Elija una dimensión de fecha que se pueda usar para analizar la tendencia de la métrica. Por ejemplo, `order date`.

## Adición de filtros {#filters}

La sección `Filter` le permite crear un filtro o aplicar un [conjunto de filtros guardado](../../data-user/reports/ess-manage-data-filters.md) a su métrica.

Para la métrica `average order revenue`, no desea incluir ningún pedido de prueba que se pueda haber realizado al configurar su tienda, lo que nos daría un resultado impreciso. Puede aplicar un conjunto de filtros para eliminar esos pedidos del conjunto de datos. Una vez creado el filtro, se aplicará a todos los gráficos creados con esta métrica.

En la sección `Filter Logic` puede definir más detalladamente cómo debe comportarse una métrica.

* &quot;\[`A`\] o \[`B`\]&quot; permite cualquier dato que cumpla los filtros \[`A`\] O \[`B`\]
* &quot;\[`A`\] y \[`B`\]&quot; solo permiten datos que cumplan los filtros \[`A`\] y \[`B`\]
* &quot;(\[`A`\] y \[`B`\]) O \[`C`\]&quot; solo permite datos que cumplan los filtros \[`A`\] y \[`B`\], o que satisfagan el filtro \[`C`\] solo

## Adición de dimensiones {#dimensions}

La sección [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) muestra todas las dimensiones de datos disponibles para filtrar o agrupar; de forma predeterminada, todas las columnas de datos disponibles se muestran como dimensiones. Continuando con el ejemplo, si desea segmentar los ingresos por fuente de referencia, puede hacerlo aquí.

Además de enumerar todas las columnas de datos disponibles como dimensiones, [!DNL Commerce Intelligence] adivina qué columnas se pueden agrupar. *Para segmentar o agrupar datos en informes*, las columnas deben marcarse como agrupables.

## Finalizando {#finish}

Además de definir el comportamiento de la métrica, también puede establecer los niveles de permisos en la sección `User Rights`. Aunque los usuarios de `Admin` tienen acceso a todas las métricas, debe indicar los usuarios que pueden usar esta métrica marcando la casilla junto al grupo correspondiente.

Si está editando una métrica existente, puede ver una lista de los gráficos (y a quién pertenecen) que utilizan esta métrica en la sección `Dependent Charts`.

Los cambios se guardan automáticamente y la métrica ya está lista.
