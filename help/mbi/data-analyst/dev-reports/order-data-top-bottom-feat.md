---
title: Ordenar datos mediante la función Mostrar arriba/abajo
description: Aprenda a ordenar los datos mediante la función Mostrar arriba/abajo.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Solicitud de datos mediante `Show Top/Bottom` característica

Puede hacer más en la `Visual Report Builder` que crear análisis que muestren la tendencia a lo largo del tiempo. Por ejemplo, puede crear un informe para mostrar el valor de sus canales de adquisición y marketing, pero también puede crear un informe que muestre solo los cinco principales ejecutantes. Del mismo modo, puede reenfocar sus esfuerzos de marketing creando un informe que le muestre qué estados generan la mayor cantidad de ingresos.

Este tipo de clasificación y orden de los datos se puede realizar en informes que utilizan un `Group By` y una `Time Interval of None`. Cuando ambos elementos están en un informe, la variable `Show Top/Bottom` Esta función se muestra encima de la previsualización del gráfico. Esta función le permite ver los puntos de datos superiores (de mayor a menor) e inferiores (de menor a mayor) en función de los parámetros configurados.

![Mostrar la función Superior/Inferior en el Report Builder visual.](../../assets/Show_Top_Bottom.png)

## ¿Cómo se usa esto? {#how}

Haga clic en **[!UICONTROL Show Top/Bottom link]** para definir los parámetros de visualización y ordenación. El número del cuadro de texto puede ser un número entero (como `5`) o `ALL`. A continuación, puede elegir ordenar el informe por la métrica O por la agrupación.

Por ejemplo, si desea mostrar las cinco fuentes de referencia que generaron la mayor cantidad de ingresos, así es como lo hace:

1. Añada el `Revenue` al informe.

1. Añadir un `Group By` para segmentar la métrica por fuente de referencia.

1. Establecer `Time Interval` hasta `None`.

1. En el `Show Top/Bottom` configuración, establecer la visualización en `5` por lo tanto, solo se incluyen en el informe las fuentes de referencia con los cinco importes de ingresos totales principales.

>[!NOTE]
>
>Debido a que el informe no tiene un `Time Interval`Sin embargo, los valores (en este caso, las cinco fuentes de referencia principales) pueden cambiar con el tiempo. Si un origen de referencia supera a otro en términos de ingresos, cambia el orden en que se muestran los orígenes.

## ¿Qué sucede si se usan varias métricas? {#multiplemetrics}

El uso de esta función se complica cuando hay más de una métrica en un informe, porque cada métrica solo se puede ordenar por sí misma o por una de las agrupaciones.

Supongamos que ha creado un informe con las dos `Revenue` y `Number of orders` métricas, agrupadas por fuente de referencia. `Revenue` solo se puede ordenar por `Revenue` o fuente de referencia y `Number of orders` solo se puede ordenar por `Number of orders` o fuente de referencia.

Esto significa que, aunque puede mostrar el `Revenue` solo desde la parte superior `5` fuentes de recomendación que generan ingresos, no puede mostrar el número de pedidos también por la parte superior `5` fuentes de referencia generadoras de ingresos. En pocas palabras: cuando hay varias métricas, la mejor opción es ordenar cada métrica por la agrupación.

A continuación se muestra un ejemplo de un gráfico que ordenó la variable `Revenue` métrica por sí sola en lugar de por la agrupación. Como puede ver, al no ordenar la métrica por la agrupación, se creó un informe extraño (y, en última instancia, poco útil):

![Resultados de informes extraños y poco útiles.](../../assets/strange-report-results.png)

Si hubiera ordenado ambas métricas por la agrupación, el gráfico tendría este aspecto:

![Ordenar ambas métricas por la agrupación.](../../assets/sort-metrics-by-grouping.png)

## ¿Cómo se ordenan los valores de forma predeterminada? {#defaultsorting}

Cuando solo se incluye una métrica en un informe con un `Group by` y una `Time Interval` de `None`, el orden predeterminado en la `Visual Report Builder` es mostrar los valores principales en función de la métrica. En este caso, la variable `Show Top/Bottom` Esta función puede no ser necesaria si satisface sus necesidades.

En este ejemplo se muestra cuántas oportunidades han cerrado sus representantes de ventas. Esta tabla se ordena automáticamente de mayor a menor según la métrica, en este caso `Won Opportunities`.

![Ordenación por métrica.](../../assets/Ordered_by_metric.png)

Sin embargo, cuando se agrega una segunda métrica, el valor predeterminado es ordenar la parte superior en función de la agrupación. A medida que se agregan métricas y agrupaciones, la ordenación predeterminada se basa en la primera agrupación, luego la segunda agrupación, etc.

![Ordenación por la agrupación.](../../assets/Ordered_by_grouping.png)

## Ajuste {#wrapup}

Aunque algunas funciones básicas se tratan aquí, esta función tiene muchos usos interesantes.

Piense en el ejemplo anterior del representante de ventas y las oportunidades. Eliminación del `Time Interval`, aplicando un `Group By`, y ordenar los datos en función de la agrupación nos permitió obtener una imagen detallada del número de oportunidades ganadas de cada representante. Además, el uso de `Show Top/Bottom` vamos a descubrir quiénes son los mejores ejecutantes.
