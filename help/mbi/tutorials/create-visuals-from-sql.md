---
title: Creación de visualizaciones a partir de consultas SQL
description: Aprenda a familiarizarse con la terminología utilizada en el Report Builder SQL y le proporcione una base sólida para crear visualizaciones SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Creación de visualizaciones a partir de consultas SQL

El objetivo de este tutorial es familiarizarle con la terminología utilizada en la `SQL Report Builder` y le proporcionan una base sólida para crear `SQL visualizations`.

La variable [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) es un creador de informes con opciones: puede ejecutar una consulta con el único propósito de recuperar una tabla de datos o puede convertir esos resultados en un informe. Este tutorial explica cómo crear una visualización a partir de una consulta SQL.

## Terminología

Antes de comenzar este tutorial, consulte la siguiente terminología utilizada en la `SQL Report Builder`.

- `Series`: La columna que desea medir se denomina Serie en el Report Builder SQL. Los ejemplos comunes son `revenue`, `items sold`y `marketing spend`. Se debe configurar al menos una columna como `Series` para crear una visualización.

- `Category`: La columna que desea utilizar para segmentar los datos se denomina `Category` Esto es igual que el `Group By` en la función [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Por ejemplo, si desea segmentar los ingresos de por vida de los clientes según su fuente de adquisición, la columna que contiene la fuente de adquisición se especificaría como `Category`. Se puede configurar más de una columna como `Category`.

>[!NOTE]
>
>Las fechas y marcas de hora también se pueden usar como `Categories`. Son simplemente otra columna de datos en la consulta y deben tener formato y orden según sus preferencias en la propia consulta.

- `Labels`: Se aplican como etiquetas de eje x. Al analizar las tendencias de datos a lo largo del tiempo, las columnas de año y mes generalmente se especifican como etiquetas. Se puede configurar más de una columna como Label.

## Paso 1: Escribir la consulta

Tenga en cuenta lo siguiente:

- La variable `SQL Report Builder` uses [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Si está creando un informe con una serie temporal, asegúrese de `ORDER BY` las columnas de marca de tiempo. Esto garantizará que las marcas de tiempo se trazen en el orden correcto en el informe.

- La variable `EXTRACT` es buena de usar para analizar el día, la semana, el mes o el año de la marca de tiempo. Esto resulta útil cuando la variable `time interval` desea utilizar en el informe es `daily`, `weekly`, `monthly`o `yearly`.

Para empezar, abra el `SQL Report Builder` haciendo clic en **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Por ejemplo, considere esta consulta que devuelve el número total mensual de artículos vendidos para cada producto:

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Esta consulta devuelve esta tabla de resultados:

![](../assets/SQL_results_table.png)

## Paso 2: Creación de la visualización

Con estos resultados, *¿cómo se crea la visualización?* Para empezar, haga clic en la **[!UICONTROL Chart]** en la ficha `Results` panel. Se mostrará la variable `Chart settings` pestaña .

Cuando se ejecuta una consulta por primera vez, el informe puede verse incrutable porque todas las columnas de la consulta están trazadas como una serie:

![](../assets/SQL_initial_report_results.png)

Para este ejemplo, queremos que este sea un gráfico de líneas que evolucione con el tiempo. Para crearlo, utilice esta configuración:

- `Series`: Seleccione el `Items sold` como el `Series` ya que queremos medirlo. Después de definir una `Series` , verá una sola línea trazada en el informe.

- `Category`: Para este ejemplo, queremos ver cada producto como una línea diferente en el informe. Para ello, configuramos `Product name` como el `Category`.

- `Labels`: Uso de las columnas `year` y `month` como etiquetas en el eje x para poder ver `Items Sold` como tendencias a lo largo del tiempo.

>[!NOTE]
>
>La consulta debe contener un `ORDER BY` en las etiquetas si `date`/`time` columnas.

A continuación se muestra un breve vistazo a cómo hemos creado esta visualización, desde la ejecución de la consulta hasta la configuración del informe:

![](../assets/SQL_report_settings.gif)

## Paso 3: Seleccione un `Chart Type`

Este ejemplo utiliza la variable `Line` tipo de gráfico. Para usar un `chart type`, haga clic en los iconos situados encima de la sección de opciones del gráfico para cambiarlo:

![](../assets/Chart_types.png)

## Paso 4: Guardar la visualización

Si desea volver a utilizar este informe, asigne un nombre al informe y haga clic en **[!UICONTROL Save]** en la esquina superior derecha.

En la lista desplegable , seleccione `Chart` como el `Type` y, a continuación, un tablero en el que guardar el informe.

## ¡Felicidades! Has terminado.

¿Quiere ir un paso más allá? Consulte la [prácticas recomendadas de optimización de consultas](../best-practices/optimizing-your-sql-queries.md).
