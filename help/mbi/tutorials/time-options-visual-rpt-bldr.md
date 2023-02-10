---
title: Usar opciones de tiempo en el Report Builder visual
description: Aprenda a analizar los datos del informe para un período de tiempo específico.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Uso `Time` Opciones de `Visual Report Builder`

Una de las características de `Visual Report Builder` es global `Time Range` y `Interval` configuración. Esta configuración le permite analizar los datos del informe durante un período de tiempo específico.

Sin embargo, en algunos análisis, es posible que tenga que tener en cuenta diferentes intervalos de tiempo o intervalos de tiempo en el mismo informe. Aquí es donde `Time` Entran las opciones. Para darle una mejor idea de cómo usar `Time` Las opciones de los informes de , este tutorial tratará los siguientes casos de uso:

* [Análisis de métricas sin marcas de hora](#notimestamp)
* [Asignar un intervalo de tiempo independiente a una métrica](#independenttimeinterval)
* [Comparación de la misma métrica en diferentes intervalos de tiempo](#difftimerange)

Si desea seguir con algunos de los informes de muestra que se tratan en este tema, abra la [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) antes de continuar.

## Análisis de métricas sin marcas de hora {#notimestamp}

Algunas métricas simplemente no pueden analizar la tendencia a lo largo del tiempo porque los datos no se recopilan ni se almacenan con una marca de tiempo asociada. Por ejemplo, una tabla de inventario a menudo contendrá solo una fila por cada SKU. En ese caso, debe [crear la métrica](../data-user/reports/ess-manage-data-metrics.md) sin especificar una marca de tiempo.

Al utilizar una métrica de este tipo en los informes, verá que al agregar esta métrica a un informe se establece automáticamente un `Time Interval` de `None` y `Time Range` de `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Asignar un intervalo de tiempo independiente a una métrica {#independenttimeinterval}

`Time` Las opciones le permiten crear gráficos del 100% basados en el tiempo para identificar qué día, semana, mes o año contribuyeron con mayor valor durante un intervalo de tiempo específico. En esta sección, creamos un gráfico que muestra el porcentaje de ingresos generados en cada mes natural de un año.

Este tipo de informe puede resultar útil si desea comparar los ingresos generados año tras año. Por ejemplo, si un gráfico de 2015 revelara que enero aportó el 18% de los ingresos del año y uno para 2016 mostró solo el 8%, podría empezar a investigar lo que podría haber sucedido.

1. Agregue la `Revenue` al informe.
1. Haga clic en **[!UICONTROL Duplicate]** para crear una copia de la métrica.
1. Haga clic en la **[!UICONTROL Time Range]** , luego **[!UICONTROL Moving Time Range]**. Configure esto como `Last Year`.
1. Haga clic en la **[!UICONTROL Time Interval]** y configúrela en `Monthly`.
1. El Report Builder agrega automáticamente un segundo eje Y para una segunda métrica. Anule la selección de `Multiple Y-Axes` en la ventana
1. A continuación, aplicamos un `Time Interval` a la primera métrica. Haga clic en **[!UICONTROL Time Options]** (icono del reloj) a la derecha del `first Revenue metric`.
1. Haga clic en **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En la lista desplegable , configure lo siguiente:

   * `Time Interval`: configure esto como `None`.

   * `Time Range`: configure esto como `Last Year` haciendo clic en **[!UICONTROL Custom]**, luego **[!UICONTROL Moving Range]** y, finalmente, seleccionar la variable `Last Year` .

   * Haga clic en **[!UICONTROL Apply]** para guardar la configuración de intervalo y intervalo. Esto crea una métrica que calcula los ingresos totales del año anterior. A continuación, utilizamos esta métrica como denominador en una fórmula.

   * Para ver el porcentaje de ingresos de cada mes, se debe agregar una fórmula al informe. Haga clic en **[!UICONTROL Add Formula]**.

   * Entrar `B/A` en el campo de fórmula y seleccione `% Percent` en el menú desplegable situado junto al campo de texto. Esta fórmula divide la cantidad de ingresos de un mes específico del año pasado por la cantidad total de ingresos del año pasado.

   * Haga clic en **[!UICONTROL Apply Changes]**.

   * Oculte ambas métricas de entrada y cambie el nombre de la fórmula.

Ahora podemos ver cuán impactante fue cada mes el año pasado:

![](../assets/Independent_Time_Int.png)

## Comparación de la misma métrica en diferentes intervalos de tiempo {#difftimerange}

Este ejemplo utiliza una dimensión personalizada llamada `Day number of the month`. Si desea crear este informe y no tiene ya esta dimensión en la Data Warehouse, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para obtener ayuda.

Los dos ejemplos más comunes de esta categoría son (1) la comparación de métricas de crecimiento (ingresos año tras año o mes tras mes) y (2) una mejor comprensión de las tendencias recientes de ventas de artículos o inventarios.

Para demostrar este caso de uso, vemos los ingresos diarios del mes anterior comparados con los del mismo mes del año anterior. Digamos que queremos ver los ingresos de cada día de enero de 2016 y luego compararlos con enero de 2015, enero de 2014, y así sucesivamente - este informe nos mostraría eso.

1. Agregue la `Revenue` al informe.
1. Haga clic en **[!UICONTROL Duplicate]** para crear una copia de la métrica.
1. Cambie el nombre de la primera métrica a `Items sold last 7 days` y la segunda métrica a `Items sold last 28 days`.
1. Haga clic en **[!UICONTROL Time Range]**, luego **[!UICONTROL Moving Time Range]**. Configure esto como `Last Month`.
1. Haga clic en **[!UICONTROL Time Interval]** y configúrelo en `None`.
1. Haga clic en **[!UICONTROL Time Options]** (icono de reloj) junto al segundo `Revenue` métrica.
1. Haga clic en **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En la lista desplegable , configure lo siguiente:

   * `Time Interval`: configure esto como `None`.

   * `Time Range`: configure esto como `From 14 Months Ago To 13 Months Ago` haciendo clic en **[!UICONTROL Custom]** then **[!UICONTROL Moving Range]**. Utilice los campos y desplegables de la parte superior del menú para establecer el rango. Esta configuración nos permite ver los ingresos del mes anterior, pero del año anterior.
   No se preocupe si la métrica desaparece del informe: al configurar opciones de tiempo independientes, se oculta automáticamente la métrica del informe. Para volver a mostrarlo, haga clic en **[!UICONTROL Show]** junto a la métrica.

   ![](../assets/Different_Time_Ranges.gif)

   * Haga clic en **[!UICONTROL Apply]** para guardar la configuración de intervalo y intervalo.

   * A continuación, agregamos nuestra `Day number of the month` para hacer clic en **[!UICONTROL Group By]** y seleccionar la dimensión. Esto devolverá el número de día del mes de un pedido; por ejemplo, un pedido realizado el 2 de marzo devolverá `2`.

   * En el `Group By` menú desplegable, seleccione `Show All` y haga clic en **[!UICONTROL Apply]**. Esto creará de forma eficaz los valores del eje X para el informe:

   ![](../assets/TO4.png)

   * Cambiar el nombre de las métricas. En nuestro ejemplo, la primera métrica es `Revenue - 2015` y la segunda es `Revenue - 2014`.



Otro uso común de `Time Options` es para determinar semanas de suministro. Especialmente durante la temporada de vacaciones o un período promocional especial, puede que desee considerar artículos vendidos durante la última semana, mes y período promocional anterior para tomar decisiones de compra informadas.

Recuerde establecer usted mismo los intervalos de tiempo en los que necesita para crear este informe.

1. Agregue la `Items Sold` al informe.
1. Haga clic en **[!UICONTROL Duplicate]** para crear una copia de la métrica.
1. Cambiar el nombre de las métricas. Puede usar los mismos nombres que usamos o algo similar:
   1. Cambie el nombre de la primera métrica a `Items sold last 7 days`.
   1. Cambie el nombre de la segunda métrica a `Items sold last 28 days`.
1. En el `Items sold last 7 days` , haga clic en la **[!UICONTROL Time Range]** a continuación **[!UICONTROL Moving Time Range]**. Para este ejemplo, lo establecemos en `Last 7 Days`.
1. Haga clic en **[!UICONTROL Time Interval]** y configúrelo en `None`.
1. A continuación, definimos la variable `Time Options` para el `Items sold last 28 days` métrica. Haga clic en **[!UICONTROL Time Options]** (icono del reloj) a la derecha del `second Items sold` métrica.
1. Haga clic en **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En la lista desplegable , configure lo siguiente:

   * `Time Interval`: configure esto como `None`.
   * `Time Range`: configure esto como `From 29 days to 1 day ago` haciendo clic en **[!UICONTROL Custom]**, luego **[!UICONTROL Moving Range]**. Utilice los campos y desplegables de la parte superior del menú para establecer el rango.
   * Haga clic en **[!UICONTROL Apply]** para guardar la configuración de intervalo y intervalo.
   * Duplique el `Items sold last 28 days` y abra las `Time Options`. Defina las opciones de la siguiente manera:

      * `Time Interval`: deje esto como `None`.
      * `Time Range`: cambie esto al intervalo de fechas que coincida con la promoción que le interese haciendo clic en **[!UICONTROL Specific Date Range]** y, a continuación, introduciendo las fechas adecuadas.
      * Cambiar el nombre de la métrica `Items sold during last promotion` o algo similar.
      * Agregue la `Units on hand` métrica.
      * A continuación, es necesario agregar los cálculos que nos muestran las semanas, teniendo en cuenta las tendencias de ventas, para los períodos de tiempo (`last 7 days`, `last 28 days`y `last promo` período) que incluimos en el informe. Debe hacerlo una vez por cada período de tiempo.

Para crear las fórmulas, haga clic en **[!UICONTROL Add Formula]**. Introduzca las fórmulas siguientes y haga clic en **[!UICONTROL Apply Changes]** cuando termine. Repita esto para cada uno de los tres periodos de tiempo:

* Para la variable `last 7 days time period`, introduzca `D / A` en el `Formula` campo .
* Para la variable `last 28 days time period`, introduzca `D / (B/4)` en el `Formula` campo .

   >[!NOTE]
   >
   >Es importante normalizar los intervalos de tiempo seleccionados aquí. En este ejemplo, se deben desglosar 28 días en cuatro semanas. Es posible que deba aplicar una lógica diferente a la fórmula.

* Para la variable `last promo period`, introduzca `D / C` en el `Formula` campo .

   ![](../assets/Different_Time_Ranges_2.png)

* Por último, personalice el informe ocultando las métricas y agregando un `SKU` o una dimensión similar al informe como un `Group By`.

Este ejemplo demuestra que los niveles de inventario actuales estaban bien situados para una venta de 14 días en todo el producto. Sin embargo, añadir un periodo promocional comparable sugiere que la empresa necesita hacer algunos cambios, ya sea solicitando más inventario y promocionando solamente los artículos con suficientes unidades en existencias.

Como los clientes se comportan de forma diferente a lo largo del tiempo, al realizar análisis puede esperar ver variaciones en los datos. La configuración de opciones de tiempo personalizadas permite crear rápidamente análisis complejos, lo que permite tomar decisiones basadas en datos que influyen en las tendencias históricas.

