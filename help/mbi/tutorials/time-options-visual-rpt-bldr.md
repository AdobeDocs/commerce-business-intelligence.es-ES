---
title: Usar opciones de tiempo en el Report Builder visual
description: Obtenga información sobre cómo analizar los datos del informe durante un período de tiempo específico.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Uso [!DNL Time] Opciones en [!DNL Visual Report Builder]

Una de las características del [!DNL Visual Report Builder] es el global `Time Range` y `Interval` configuración. Esta configuración le permite analizar los datos del informe durante un período de tiempo específico.

Sin embargo, en algunos análisis puede que sea necesario tener en cuenta intervalos de tiempo o intervalos de tiempo diferentes en el mismo informe. Ahí es donde `Time` Las opciones entran. Para que tenga una mejor idea de cómo usar `Time` en sus informes, este tutorial cubre los siguientes casos de uso:

* [Análisis de métricas sin marcas de tiempo](#notimestamp)
* [Concesión de un intervalo de tiempo independiente a una métrica](#independenttimeinterval)
* [Comparación de la misma métrica en diferentes intervalos de tiempo](#difftimerange)

Si desea seguir junto con algunos de los informes de ejemplo mencionados en este tema, abra el [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) antes de continuar.

## Análisis de métricas sin marcas de tiempo {#notimestamp}

Algunas métricas simplemente no pueden generar tendencias a lo largo del tiempo porque los datos no se recopilan ni almacenan con una marca de tiempo asociada. Por ejemplo, una tabla de inventario a menudo contiene solo una fila para cada SKU. En ese caso, debería [creación de la métrica](../data-user/reports/ess-manage-data-metrics.md) sin especificar una marca de tiempo.

Al utilizar una métrica de este tipo en los informes, observa que al agregar esta métrica a un informe se establece automáticamente una métrica independiente `Time Interval` de `None` y `Time Range` de `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Concesión de un intervalo de tiempo independiente a una métrica {#independenttimeinterval}

`Time` Las opciones le permiten crear gráficos del 100 % basados en el tiempo para identificar qué día, semana, mes o año contribuyó con la mayor cantidad de valor durante un intervalo de tiempo específico. En esta sección, se crea un gráfico que muestra el porcentaje de ingresos generados en cada mes natural de un año.

Este tipo de informe puede resultar útil si desea comparar los ingresos generados año tras año. Por ejemplo, un gráfico para 2015 reveló que enero contribuyó con el 18 por ciento de los ingresos del año y un gráfico para 2016 mostró solo el 8 por ciento. Podrías empezar a investigar lo que podría haber pasado.

1. Añada su `Revenue` al informe.
1. Clic **[!UICONTROL Duplicate]** para realizar una copia de la métrica.
1. Haga clic en el global **[!UICONTROL Time Range]** opción, entonces **[!UICONTROL Moving Time Range]**. Configure esto como `Last Year`.
1. Haga clic en el global **[!UICONTROL Time Interval]** y configúrelo en. `Monthly`.
1. El Report Builder añade automáticamente un segundo eje Y para una segunda métrica. Anule la selección de `Multiple Y-Axes` cuadro.
1. A continuación, se aplica un `Time Interval` a la primera métrica. Clic **[!UICONTROL Time Options]** (icono del reloj) a la derecha del `first Revenue metric`.
1. Clic **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En el menú desplegable, establezca lo siguiente:

   * `Time Interval`: establezca esto en `None`.

   * `Time Range`: establezca esto en `Last Year` haciendo clic primero en **[!UICONTROL Custom]**, entonces **[!UICONTROL Moving Range]** y, finalmente, seleccionando la `Last Year` opción.

   * Clic **[!UICONTROL Apply]** para guardar la configuración de intervalo y rango. Esto crea una métrica que calcula los ingresos totales del año anterior. A continuación, utilice esta métrica como denominador en una fórmula.

   * Para ver el porcentaje de ingresos de cada mes, debe agregar una fórmula al informe. Clic **[!UICONTROL Add Formula]**.

   * Entrar `B/A` en el campo formula y seleccione `% Percent` en el menú desplegable situado junto al campo de texto. Esta fórmula divide la cantidad de ingresos de un mes específico del año pasado por la cantidad total de ingresos del año pasado.

   * Clic **[!UICONTROL Apply Changes]**.

   * Oculte ambas métricas de entrada y cambie el nombre de la fórmula.

Ahora puede ver el impacto que tuvo cada mes el año pasado:

![](../assets/Independent_Time_Int.png)

## Comparación de la misma métrica en diferentes intervalos de tiempo {#difftimerange}

Este ejemplo utiliza una dimensión personalizada llamada `Day number of the month`. Si desea crear este informe y aún no tiene esta dimensión en la Data Warehouse, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obtener asistencia.

Los dos ejemplos más comunes en esta categoría son (1) la comparación de métricas de crecimiento (ingresos año tras año o mes tras mes) y (2) una mejor comprensión de las tendencias recientes de ventas de artículos o inventarios.

Para demostrar este caso de uso, observe los ingresos diarios del mes anterior en comparación con el mismo mes del año anterior. Supongamos que desea ver los ingresos de cada día de enero de 2016 y luego compararlos con los de enero de 2015, enero de 2014 y así sucesivamente. Este informe nos lo mostraría.

1. Añada su `Revenue` al informe.
1. Clic **[!UICONTROL Duplicate]** para realizar una copia de la métrica.
1. Cambie el nombre de la primera métrica a `Items sold last 7 days` y la segunda métrica a `Items sold last 28 days`.
1. Clic **[!UICONTROL Time Range]**, entonces **[!UICONTROL Moving Time Range]**. Configure esto como `Last Month`.
1. Clic **[!UICONTROL Time Interval]** y configúrelo en `None`.
1. Clic **[!UICONTROL Time Options]** (icono del reloj) junto al segundo `Revenue` métrica.
1. Clic **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En el menú desplegable, establezca lo siguiente:

   * `Time Interval`: establezca esto en `None`.

   * `Time Range`: establezca esto en `From 14 Months Ago To 13 Months Ago` haciendo clic primero en **[!UICONTROL Custom]** entonces **[!UICONTROL Moving Range]**. Utilice los campos y los menús desplegables de la parte superior del menú para establecer el intervalo. Esta configuración nos permite ver los ingresos del mes anterior, pero del año anterior.
   No se preocupe si la métrica desaparece del informe: al establecer una opción de tiempo independiente, se oculta automáticamente la métrica del informe. Para volver a mostrarlo, haga clic en **[!UICONTROL Show]** junto a la métrica.

   ![](../assets/Different_Time_Ranges.gif)

   * Clic **[!UICONTROL Apply]** para guardar la configuración de intervalo y rango.

   * A continuación, agregue el personalizado `Day number of the month` dimensión haciendo clic en **[!UICONTROL Group By]** y seleccionando la dimensión. Devolverá el número de día del mes de un pedido; por ejemplo, un pedido realizado el 2 de marzo devolverá `2`.

   * En el `Group By` menú desplegable, seleccione `Show All` y haga clic en **[!UICONTROL Apply]**. Esto crea los valores del eje X para el informe:

   ![](../assets/TO4.png)

   * Cambie el nombre de las métricas. En el ejemplo, la primera métrica es `Revenue - 2015` y la segunda es `Revenue - 2014`.



Otro uso común de la personalización `Time Options` es para determinar semanas de suministro. Especialmente durante la temporada de vacaciones o durante un periodo promocional especial, es posible que desee tener en cuenta los artículos vendidos durante la última semana, el mes y el periodo promocional anterior para tomar decisiones de compra informadas.

Recuerde establecer los intervalos de tiempo según lo que necesite al crear este informe.

1. Añada su `Items Sold` al informe.
1. Clic **[!UICONTROL Duplicate]** para realizar una copia de la métrica.
1. Cambie el nombre de las métricas. Puede usar los mismos nombres o algo que sea similar:
   1. Cambie el nombre de la primera métrica a `Items sold last 7 days`.
   1. Cambie el nombre de la segunda métrica a `Items sold last 28 days`.
1. En el `Items sold last 7 days` métrica, haga clic en el **[!UICONTROL Time Range]** Opción entonces **[!UICONTROL Moving Time Range]**. Para este ejemplo, lo establece en `Last 7 Days`.
1. Clic **[!UICONTROL Time Interval]** y configúrelo en `None`.
1. A continuación, defina la variable `Time Options` para el `Items sold last 28 days` métrica. Clic **[!UICONTROL Time Options]** (icono del reloj) a la derecha del `second Items sold` métrica.
1. Clic **[!UICONTROL Time Options]** en la ventana expandida que se muestra encima del informe.
1. En el menú desplegable, establezca lo siguiente:

   * `Time Interval`: establezca esto en `None`.
   * `Time Range`: establezca esto en `From 29 days to 1 day ago` haciendo clic primero en **[!UICONTROL Custom]**, entonces **[!UICONTROL Moving Range]**. Utilice los campos y los menús desplegables de la parte superior del menú para establecer el intervalo.
   * Clic **[!UICONTROL Apply]** para guardar la configuración de intervalo y rango.
   * Duplique el `Items sold last 28 days` y abra la nueva métrica de `Time Options`. Establezca las opciones en lo siguiente:

      * `Time Interval`: dejar esto como `None`.
      * `Time Range`: cambie esto al intervalo de fechas que se ajuste a la promoción que le interesa haciendo clic en **[!UICONTROL Specific Date Range]** y, a continuación, introducir las fechas adecuadas.
      * Cambiar el nombre de la métrica `Items sold during last promotion` o algo similar.
      * Añada su `Units on hand` métrica.
      * A continuación, debe agregar los cálculos que muestran las semanas disponibles, teniendo en cuenta las tendencias de ventas, para los períodos de tiempo (`last 7 days`, `last 28 days`, y `last promo` punto) que se incluye en el informe. Debe hacerlo una vez por cada período de tiempo.

Para crear las fórmulas, haga clic en **[!UICONTROL Add Formula]**. Introduzca las fórmulas a continuación y haga clic en **[!UICONTROL Apply Changes]** cuando termine. Repita esto para cada uno de los tres períodos de tiempo:

* Para el `last 7 days time period`, introduzca `D / A` en el `Formula` field.
* Para el `last 28 days time period`, introduzca `D / (B/4)` en el `Formula` field.

   >[!NOTE]
   >
   >Es importante normalizar aquí los intervalos de tiempo seleccionados. En este ejemplo, divida 28 días en cuatro semanas. Es posible que tenga que aplicar una lógica diferente a la fórmula.

* Para el `last promo period`, introduzca `D / C` en el `Formula` field.

   ![](../assets/Different_Time_Ranges_2.png)

* Por último, personalice el informe ocultando las métricas y agregando un `SKU` o una dimensión similar al informe como `Group By`.

Este ejemplo demuestra que los niveles de inventario actuales estaban bien situados para una venta de todo un producto de 14 días. Sin embargo, añadir un periodo promocional comparable sugiere que la empresa necesita hacer algunos cambios, ya sea pidiendo más inventario y promocionando solo los artículos con suficientes unidades en stock.

Dado que los clientes se comportan de forma diferente a lo largo del tiempo, es probable que observe variaciones en los datos al realizar los análisis. La configuración de Opciones de tiempo personalizadas le permite crear rápidamente análisis complejos, lo que permite tomar decisiones basadas en datos que tienen en cuenta las tendencias históricas.

