---
title: Creación de visualizaciones a partir de consultas SQL
description: Aprenda a familiarizarse con la terminología utilizada en SQL Report Builder y le proporcione una base sólida para crear visualizaciones SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Developer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/xWv7O8UJ6gXxysl6oG1t24ygF-PE4LTanwyrrvoJzQ4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---

# Creación de visualizaciones a partir de consultas SQL

El objetivo de este tutorial es que se familiarice con la terminología usada en [!DNL SQL Report Builder] y proporcionarle una base sólida para crear `SQL visualizations`.

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) es un Report Builder con opciones: puede ejecutar una consulta con el único propósito de recuperar una tabla de datos o puede convertir esos resultados en un informe. Este tutorial explica cómo crear una visualización a partir de una consulta SQL.

## Terminología

Antes de comenzar este tutorial, consulte la siguiente terminología utilizada en `SQL Report Builder`.

- `Series`: La columna que desea medir se denomina Serie en SQL Report Builder. Los ejemplos más comunes son `revenue`, `items sold` y `marketing spend`. Se debe establecer al menos una columna como `Series` para crear una visualización.

- `Category`: la columna que desea usar para segmentar los datos se denomina `Category`. Es igual que la característica `Group By` de [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Por ejemplo, si desea segmentar los ingresos de duración de los clientes por su origen de adquisición, la columna que contiene el origen de adquisición se especificaría como `Category`. Se puede establecer más de una columna como `Category`.

>[!NOTE]
>
>Las fechas y marcas de tiempo también se pueden usar como `Categories`. Son simplemente otra columna de datos de la consulta y deben tener el formato y el orden que desee en la propia consulta.

- `Labels`: se aplican como etiquetas del eje x. Al analizar las tendencias de los datos a lo largo del tiempo, las columnas año y mes se especifican como etiquetas. Se puede configurar más de una columna para que sea Label.

## Paso 1: Escribir la consulta

Tenga en cuenta lo siguiente:

- [!DNL SQL Report Builder] usa [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Si está creando un informe con una serie temporal, asegúrese de `ORDER BY` las columnas de marca de tiempo. Esto garantiza que las marcas de tiempo se trazen en el orden correcto en el informe.

- La función `EXTRACT` es excelente de usar para analizar el día, la semana, el mes o el año de la marca de tiempo. Esto resulta útil cuando el `time interval` que desea usar en el informe es `daily`, `weekly`, `monthly` o `yearly`.

Para empezar, abra [!DNL SQL Report Builder] haciendo clic en **[!UICONTROL Report Builder** > **SQL Report Builder]**.

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

![Tabla que muestra resultados de consultas SQL con elementos vendidos por producto, año y mes](../assets/SQL_results_table.png)

## Paso 2: Crear la visualización

Con estos resultados, *¿cómo se crea la visualización?* Para comenzar, haga clic en la ficha **[!UICONTROL Chart]** en el panel `Results`. Esto muestra la ficha `Chart settings`.

Cuando se ejecuta una consulta por primera vez, el informe puede parecer inescrutable porque todas las columnas de la consulta se trazan como una serie:

![Informe SQL inicial con todas las columnas trazadas como series](../assets/SQL_initial_report_results.png)

Para este ejemplo, desea que sea un gráfico de líneas que siga la tendencia a lo largo del tiempo. Para crearlo, utilice esta configuración:

- `Series`: seleccione la columna `Items sold` como `Series`, ya que desea medirla. Después de definir una columna `Series`, verá una sola línea trazada en el informe.

- `Category`: en este ejemplo, desea ver cada producto como una línea diferente en el informe. Para ello, ha establecido `Product name` como `Category`.

- `Labels`: use las columnas `year` y `month` como etiquetas en el eje x para poder ver `Items Sold` como tendencias a lo largo del tiempo.

>[!NOTE]
>
>La consulta debe contener una cláusula `ORDER BY` en las etiquetas si son `date`/`time` columnas.

A continuación se muestra una breve descripción de cómo creó esta visualización, desde la ejecución de la consulta hasta la configuración del informe:

![Demostración animada de la configuración de visualización de informes SQL](../assets/SQL_report_settings.gif)

## Paso 3: Seleccionar un(a) `Chart Type`

Este ejemplo utiliza el tipo de gráfico `Line`. Para usar un(a) `chart type` diferente(a), haga clic en los iconos de la sección de opciones del gráfico para cambiarlo:

![Iconos de tipo de gráfico disponibles que incluyen línea, barra, área y otras opciones de visualización](../assets/Chart_types.png)

## Paso 4: Guardar la visualización

Si desea volver a utilizar este informe, asígnele un nombre y haga clic en **[!UICONTROL Save]** en la esquina superior derecha.

En el menú desplegable, seleccione `Chart` como `Type` y, a continuación, un tablero en el que guardar el informe.

## Ajuste

¿Quieres ir un paso más allá? Consulte las [prácticas recomendadas de optimización de consultas](../best-practices/optimizing-your-sql-queries.md).
