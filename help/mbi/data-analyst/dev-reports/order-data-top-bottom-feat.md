---
title: Ordenar datos con la función Mostrar arriba/abajo
description: Obtenga información sobre cómo ordenar los datos mediante la función Mostrar arriba/abajo .
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Solicitud de datos mediante `Show Top/Bottom` función

Puede hacer más en la `Visual Report Builder` que crea analiza esa tendencia a lo largo del tiempo. Por ejemplo, puede crear un informe para mostrar el valor que tienen los canales de marketing y adquisición, pero también puede crear un informe que muestre solo los cinco principales. Del mismo modo, puede volver a centrar sus esfuerzos de marketing mediante la creación de un informe que muestre qué estados generan la mayor cantidad de ingresos.

Este tipo de clasificación y ordenación de datos se puede realizar en informes que utilizan un `Group By` y `Time Interval of None`. Cuando ambos elementos están en un informe, la variable `Show Top/Bottom` se mostrará encima de la vista previa del gráfico. Esta función le permite ver los puntos de datos superior (de mayor a menor) y inferior (de menor a mayor) en función de los parámetros que establezca.

![Mostrar la función Superior/Inferior en el Report Builder visual.](../../assets/Show_Top_Bottom.png)

## ¿Cómo utilizo esto? {#how}

Después de hacer clic en el botón **[!UICONTROL Show Top/Bottom link]**, se mostrará una ventana donde puede configurar los parámetros de visualización y clasificación. El número del cuadro de texto puede ser un número entero (como `5`) o `ALL`. A continuación, puede elegir ordenar el informe por métrica O por agrupación.

Por ejemplo, si queremos mostrar las cinco fuentes de referencia que reportaron la mayor cantidad de ingresos, así es como lo hacemos:

1. Agregue la variable `Revenue` al informe.

1. Agregue un `Group By` para segmentar la métrica por fuente de referencia.

1. Establezca `Time Interval` a `None`.

1. En el `Show Top/Bottom` configuración, establezca la visualización en `5` por lo tanto, solo se incluyen en el informe las fuentes de referencia con las cinco principales cantidades totales de ingresos.

>[!NOTE]
>
>Debido a que el informe no tiene un `Time Interval`, los valores -en este caso, las cinco fuentes de referencia principales- pueden cambiar con el tiempo. Si una fuente de referencia supera a otra en términos de ingresos, el orden en que se muestran los orígenes cambiará.

## ¿Qué sucede con el uso de varias métricas? {#multiplemetrics}

El uso de esta función se complica cuando hay más de una métrica en un informe porque cada métrica solo se puede ordenar por sí sola o por una de las agrupaciones.

Digamos que construimos un informe con ambas `Revenue` y `Number of orders` métricas, agrupadas por fuente de referencia. `Revenue` solo se puede ordenar por `Revenue` o la fuente de referencia `Number of orders` solo se puede ordenar por `Number of orders` o fuente de referencia.

Esto significa que, aunque podemos mostrar la variable `Revenue` desde solo la parte superior `5` fuentes de referencia que generan ingresos, no se puede mostrar el número de pedidos también en la parte superior `5` fuentes de referencia que generan ingresos. En pocas palabras: cuando hay varias métricas, lo mejor es ordenar cada métrica por la agrupación.

Este es un ejemplo de un gráfico en el que ordenamos la variable `Revenue` métrica por sí sola en lugar de por la agrupación. Como puede ver, al no ordenar la métrica por la agrupación, se creó un informe extraño (y en última instancia no útil):

![Resultados de informes extraños y poco útiles.](../../assets/strange-report-results.png)

Si se hubieran ordenado ambas métricas por agrupación, el gráfico tendría este aspecto:

![Clasificación de ambas métricas por agrupación.](../../assets/sort-metrics-by-grouping.png)

## ¿Cómo se ordenan los valores de forma predeterminada? {#defaultsorting}

Cuando solo se incluye una métrica en un informe con un `Group by` y `Time Interval` de `None`, el orden predeterminado en la variable `Visual Report Builder` es mostrar los valores principales basados en la métrica. En este caso, la variable `Show Top/Bottom` puede que no sea necesaria si se adapta a sus necesidades.

En este ejemplo, estamos viendo cuántas oportunidades han cerrado nuestros representantes de ventas. Esta tabla se ordena automáticamente de mayor a menor según la métrica, en este caso `Won Opportunities`.

![Pedidos según la métrica.](../../assets/Ordered_by_metric.png)

Sin embargo, cuando se agrega una segunda métrica, el valor predeterminado es ordenar la parte superior en función de la agrupación. A medida que se agregan métricas y agrupaciones, la clasificación predeterminada se basa en la primera agrupación, luego en la segunda agrupación, etc.

![Solicitud por la agrupación.](../../assets/Ordered_by_grouping.png)

## Ajuste {#wrapup}

Lo mencionamos al principio del artículo, pero lo decimos de nuevo: aunque hemos cubierto algunos ejemplos básicos, esta función tiene muchos usos interesantes.

Piense en nuestro representante de ventas anterior y en el ejemplo de oportunidades. Eliminación de `Time Interval`, aplicar un `Group By`, y la clasificación de los datos en función de la agrupación nos permitió obtener una imagen detallada del número de oportunidades obtenidas por cada representante. Además, al usar la variable `Show Top/Bottom` nos permite descubrir quiénes son los mejores.
