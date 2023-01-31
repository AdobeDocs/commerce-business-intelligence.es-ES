---
title: Usar el Report Builder visual
description: Aprenda a analizar los datos del informe para un período de tiempo específico.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Utilice la variable `Visual Report Builder`

La variable [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) le permite explorar visualmente sus datos para extraer perspectivas y ayudar a tomar decisiones comerciales. Este tutorial lo acompaña durante el proceso de creación de un informe básico.

>[!NOTE]
>
>Para agregar un informe a un tablero, debe `Standard` [permisos de usuario](../administrator/user-management/user-management.md) y `Edit` acceso al tablero.

## Paso 1: Creación de un informe

Para empezar a crear un nuevo informe, haga clic en **[!UICONTROL Report Builder]** en la barra lateral o **[!UICONTROL Add Report]** en la parte superior de cualquier tablero. Cuando la variable `Report Builder` la página de selección que se muestra, haga clic en el botón **[!UICONTROL Visual Report Builder]** .

Para editar un informe creado en la variable `Visual Report Builder`, haga clic en el icono de engranaje (Opciones) en la esquina superior derecha de cualquier gráfico y, a continuación, haga clic en **[!UICONTROL Edit]**.

## Paso 2: Adición de métricas

El primer paso para crear un análisis es seleccionar [la métrica](../data-user/reports/ess-manage-data-metrics.md) para analizar. Aunque las métricas se muestran alfabéticamente de forma predeterminada, también puede agruparlas por la tabla que alimenta la métrica.

Puede agregar métricas adicionales después de seleccionar la métrica inicial y superponer todas las métricas en un solo informe o realizar cálculos multimétricas agregando fórmulas.

## Paso 3: Adición `Formulas`

`Formulas` se añaden a los informes haciendo clic en **[!UICONTROL Add Formula]**, ubicado justo encima de la lista de métricas del informe. En el [editor de fórmulas](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), cualquiera de las métricas incluidas en el informe puede utilizarse como entradas. Los operadores matemáticos básicos se utilizan para manipular las distintas métricas.

Digamos que queríamos crear un informe que nos muestre los ingresos promedio por pedido. En este caso, dividiremos el `Revenue` por `Number of orders` métrica.

![](../assets/ave-rev-per-order.png)

## Paso 4: Configuración de la variable `Time Period` y `Interval of Analysis` {#time}

Para centrarse en un periodo de tiempo determinado, puede establecer el período de tiempo para el análisis. También puede elegir intervalos de tiempo para segmentar los datos (por ejemplo, por año, por trimestre o por mes). Utilice los menús de la esquina superior derecha del gráfico para establecer el intervalo y el período de tiempo.

![](../assets/Time_Options_Report_Builder.png)

Al configurar un intervalo de fechas específico para el período de tiempo, asegúrese de que la fecha de inicio se encuentre al principio del intervalo y que la fecha de finalización se encuentre al final del intervalo.

Por ejemplo, si se configura un periodo de tiempo de `January 1st to March 1st` y elija un `monthly` se mostrará el intervalo `March` como punto de datos, pero ignore todos los días en `March` except `March 1`. En ese caso, debe hacer que su `Time Period` from `January 1 to March 31`.

## Paso 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Para segmentar las métricas por una dimensión de datos](../best-practices/segment-filter.md), haga clic en **[!UICONTROL Group by]** en la parte superior izquierda del gráfico. De este modo se mostrará un menú desplegable que incluye todas las dimensiones disponibles de la primera métrica incluida en la lista.

Puede elegir `None` para evitar que una métrica se segmente. Por ejemplo, es posible que desee una métrica que devuelva los ingresos totales sin estar segmentada, mientras que otra métrica de ingresos se segmenta por región.

Vuelva a los ingresos promedio por ejemplo de pedido y establezca el grupo por en código promocional. Esto nos mostrará el ingreso promedio por pedido para pedidos tanto con como sin un código promocional.

![](../assets/Group_By_Report_Builder.png)

Si las métricas incluidas en el análisis se crean en distintas tablas de datos, una ventana emergente le permitirá seleccionar la dimensión de datos coincidente en cada tabla. El objetivo aquí es encontrar dimensiones que compartan el mismo tipo de valores para la segmentación:

![](../assets/Dimension_Editor.png)

## Paso 6: Configuración `Metric Filters`, `Perspective`y `Time Interval` {#metric-specific}

Para cada métrica agregada al análisis, puede añadir filtros, seleccionar la perspectiva de datos relevante y establecer `time interval` opciones. Para acceder a estas funciones, haga clic en el canal (`Filter`), ojo (`Perspective`) y reloj (`Time`), que se encuentran junto a las métricas incluidas en el informe.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limite el conjunto de datos incluido en el análisis. Los filtros son extremadamente útiles, por ejemplo, al evaluar canales de adquisición individuales y eliminar periféricos.

Además de los menús desplegables y el cuadro de texto, también puede utilizar operadores de filtro especiales, como `LIKE` o `IN` para crear filtros.

El uso de caracteres comodín (`%` o `_`) conjuntamente con `LIKE` es compatible. La variable `%` comodín coincidirá con varios caracteres, mientras que `_` solo coincidirá con cualquier carácter individual. Por ejemplo:

- `affiliate's name Like B%` solo permitirá datos de clientes cuyo nombre comience por `B`.

- `affiliate's name Like _ake` solo permitirá datos de clientes cuyos nombres sean similares a `Jake`, `Rake`o `Bake` pero no `Drake` o `Blake`.

Añadir varios filtros permite un control estricto de los datos del gráfico. De forma predeterminada, todas las condiciones de filtro deben ser verdaderas para que se incluya un fragmento de datos, pero puede crear relaciones O editando el cuadro de texto Reglas de filtro .

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` permite alternar fácilmente entre diferentes vistas de los datos. Echemos un vistazo a lo que está disponible:

- `Standard perspective`: La perspectiva estándar muestra el resultado de la fecha coincidente en el eje x (por ejemplo, ingresos en enero). Esta es la perspectiva que usamos en nuestro ejemplo de Promedio de ingresos por pedidos .

![](../assets/Standard.png)

- `Amount` O `Percent Change` versus `Previous Period` Perspectiva: Esta perspectiva muestra la cantidad o el porcentaje de cambio de un intervalo a otro y resulta útil para medir la tasa de cambio en las métricas que cambian rápidamente. También existe una perspectiva para comparar el intervalo con el mismo período de tiempo del año pasado y mostrar el crecimiento año tras año.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: La variable `cumulative perspective` muestra la cantidad de suma continua o acumulativa de la métrica durante el período de tiempo. Esto se utiliza a menudo para analizar el total de clientes y planificar la capacidad futura.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Esta perspectiva muestra los datos como un porcentaje del primer intervalo de tiempo incluido en el análisis. Esto resulta útil para medir la eficacia de acciones específicas en relación con el rendimiento del primer periodo.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: La perspectiva de la ventana promedios móviles muestra el valor promedio móvil de una métrica en el intervalo de tiempo especificado. El intervalo debe ser el mismo que el establecido en el nivel del informe. Por ejemplo, si el informe muestra el último trimestre completo de Ingresos por semana, puede establecer el intervalo de tiempo promedio móvil en 4 semanas, y los tres primeros valores serán nulos y el cuarto valor representa el promedio de las primeras 4 semanas de Ingresos. Para una mayor claridad, asegúrese de desactivar el `Multiple Y-Axes` si está viendo la misma métrica con un promedio móvil, como en el ejemplo siguiente.

![](../assets/rolling_avg_window.png)

### Opciones de tiempo específicas de métricas

Existen dos opciones para las métricas utilizadas en los informes: pueden analizar la tendencia a lo largo del tiempo según las opciones de tiempo globales, o no, lo que las mostrará como un número escalar.

Cambio de un intervalo de tiempo de métrica a `None` devuelve un valor `scalar` número, lo cual resulta útil al crear fórmulas que impliquen dividir una métrica de tendencias de tiempo por un `scalar` número. Además, también puede cambiar el intervalo de tiempo del `scalar` a un intervalo de tiempo independiente del del informe.

Digamos, por ejemplo, que queríamos ver los ingresos mensuales de 2019 expresados como un porcentaje de los ingresos globales de 2019. Podemos añadir dos `Revenue` métricas a un informe con un intervalo de tiempo global del 1 de enero de 2019 al 31 de diciembre de 2019, segmentadas por intervalo mensual.

>[!NOTE]
>
>Si agrega `group by` , elija una nueva visualización o ajuste el intervalo de tiempo y, a continuación, guarde solo el Número (`scalar`), esos ajustes no se mantendrán la próxima vez que abra ese informe desde un tablero; solo se conservará el intervalo de tiempo.

Para obtener más información sobre el uso de las opciones de tiempo en los informes, consulte esta [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Paso 7: Guardar el informe

Al crear un gráfico nuevo, puede guardarlo haciendo clic en **[!UICONTROL Save]** en la esquina superior derecha del `Visual Report Builder`.

Puede elegir guardar un gráfico, una tabla o un número (`scalar`) utilizando la variable `Type` y el tablero en el que se debe guardar el informe mediante la función `Location` lista desplegable.

A continuación, puede guardar el informe haciendo clic en **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Resultados del informe

Para ayudarle a decidir qué salida de informe elegir, consulte lo siguiente:

### Gráfico

![](../assets/RB_Chart.png)

### Tabla

![](../assets/RB_Table.png)

### Número (`scalar`)

![](../assets/RB_Scalar.png)

¡Felicidades! Has terminado.
