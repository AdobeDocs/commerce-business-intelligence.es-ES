---
title: Usar el Report Builder visual
description: Obtenga información sobre cómo analizar los datos del informe durante un período de tiempo específico.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Utilice el [!DNL Visual Report Builder]

El [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) le permite explorar visualmente sus datos para obtener perspectivas y ayudar a impulsar las decisiones comerciales. Este tutorial lo acompañará durante el proceso de creación de un informe básico.

>[!NOTE]
>
>Para agregar un informe a un panel, necesita lo siguiente `Standard` [permisos de usuario](../administrator/user-management/user-management.md) y `Edit` acceso al tablero.

## Paso 1: Creación de un informe

Para empezar a crear un informe, haga clic en **[!UICONTROL Report Builder]** en la barra lateral o **[!UICONTROL Add Report]** en la parte superior de cualquier tablero. Si la variable `Report Builder` página, haga clic en el **[!UICONTROL Visual Report Builder]** opción.

Para editar un informe creado en [!DNL Visual Report Builder], haga clic en el icono de engranaje (Opciones) en la esquina superior derecha de cualquier gráfico y, a continuación, haga clic en **[!UICONTROL Edit]**.

## Paso 2: Añadir métricas

El primer paso para crear un análisis es seleccionar [la métrica](../data-user/reports/ess-manage-data-metrics.md) para analizar. Aunque las métricas se enumeran alfabéticamente de forma predeterminada, también puede agruparlas por la tabla que alimenta la métrica.

Puede agregar métricas adicionales después de seleccionar la métrica inicial y superponer todas las métricas en un solo informe, o realizar cálculos de varias métricas agregando fórmulas.

## Paso 3: Añadir `Formulas`

`Formulas` se añaden a los informes haciendo clic en **[!UICONTROL Add Formula]**, situado justo encima de la lista de métricas del informe. En el [editor de fórmulas](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), cualquiera de las métricas incluidas en el informe puede utilizarse como entradas. Los operadores matemáticos básicos se utilizan para manipular las distintas métricas.

Supongamos que desea crear un informe que muestre los ingresos medios por pedido. En este caso, debe dividir la variable `Revenue` métrica por el `Number of orders` métrica.

![](../assets/ave-rev-per-order.png)

## Paso 4: Configuración de `Time Period` y `Interval of Analysis` {#time}

Para centrarse en un periodo de tiempo determinado, se puede definir el periodo de tiempo del análisis. También puede elegir intervalos de tiempo para segmentar los datos (por ejemplo, por año, trimestre o mes). Utilice los menús de la esquina superior derecha del gráfico para establecer el período de tiempo y el intervalo.

![](../assets/Time_Options_Report_Builder.png)

Al establecer un intervalo de fechas específico para el período de tiempo, asegúrese de que la fecha de inicio sea al principio del intervalo y la fecha de finalización al final del intervalo.

Por ejemplo, configurar un periodo de tiempo desde `January 1st` hasta `March 1st` y elegir una `monthly` programas de intervalos `March` como punto de datos, pero ignorar todos los días en `March` excepto `March 1`. En ese caso, debe hacer su `Time Period` de `January 1 to March 31`.

## Paso 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Para segmentar las métricas por una dimensión de datos](../best-practices/segment-filter.md), haga clic en **[!UICONTROL Group by]** en la parte superior izquierda del gráfico. Esto revela un menú desplegable que incluye todas las dimensiones disponibles de la primera métrica incluida en la lista.

Puede elegir `None` para evitar que una métrica se segmente. Por ejemplo, es posible que desee una métrica que devuelva los ingresos totales sin estar segmentada, mientras que otra métrica de ingresos esté segmentada por región.

Vuelva al ejemplo de ingresos promedio por pedido y establezca Agrupar por en el código de promoción. Esto muestra el promedio de ingresos por pedido para pedidos con y sin código de promoción.

![](../assets/Group_By_Report_Builder.png)

Si las métricas incluidas en el análisis se crean en distintas tablas de datos, una ventana emergente le permite seleccionar la dimensión de datos coincidente en cada tabla. El objetivo aquí es encontrar dimensiones que compartan un tipo de valores para la segmentación:

![](../assets/Dimension_Editor.png)

## Paso 6: Configuración `Metric Filters`, `Perspective`, y `Time Interval` {#metric-specific}

Para cada métrica añadida al análisis, puede añadir filtros, seleccionar la perspectiva de datos relevante y definir `time interval` opciones. Para acceder a estas funciones, haga clic en el canal (`Filter`), ojo (`Perspective`) y el reloj (`Time`) iconos ubicados junto a las métricas incluidas en el informe.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limite el conjunto de datos incluido en el análisis. Los filtros son útiles, por ejemplo, para evaluar canales de adquisición individuales y eliminar periféricos.

Además de los menús desplegables y el cuadro de texto, también puede utilizar operadores de filtro especiales como `LIKE` o `IN` para crear filtros.

El uso de caracteres comodín (`%` o `_`) con `LIKE` se admite. El `%` el comodín coincide con varios caracteres, mientras que `_` solo coincide con cualquier carácter individual. Por ejemplo:

- `affiliate's name Like B%` solo permite datos de clientes cuyo nombre comience por `B`.

- `affiliate's name Like _ake` solo permite datos de clientes cuyos nombres son similares a `Jake`, `Rake`, o `Bake` pero no `Drake` o `Blake`.

Añadir varios filtros permite un control estricto de los datos del gráfico. De forma predeterminada, todas las condiciones de filtro deben ser verdaderas para que se incluya un fragmento de datos, pero puede crear relaciones O editando el cuadro de texto Reglas de filtro.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Le permite alternar fácilmente entre diferentes vistas de los datos. Observe lo que está disponible:

- `Standard perspective`: la perspectiva estándar muestra el resultado de la fecha coincidente en el eje x (por ejemplo, ingresos en enero). Esta es la perspectiva que utiliza en el ejemplo Ingresos promedio por pedidos.

![](../assets/Standard.png)

- `Amount` O `Percent Change` frente `Previous Period` perspectiva: esta perspectiva muestra la cantidad o el porcentaje de cambio de un intervalo al siguiente y es útil para medir la tasa de cambio en métricas de cambio rápido. También existe una perspectiva para comparar el intervalo con el mismo período de tiempo del año pasado y mostrar el crecimiento interanual.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: La `cumulative perspective` muestra la cantidad de suma continua o acumulativa de la métrica durante el período de tiempo. Esto se utiliza a menudo para analizar el total de clientes y planificar la capacidad futura.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Esta perspectiva muestra los datos como un porcentaje del primer intervalo de tiempo incluido en el análisis. Esto resulta útil para medir la eficacia de acciones específicas en relación con el rendimiento del primer periodo.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: la perspectiva de la ventana promedios móviles muestra el valor promedio móvil de una métrica en el intervalo de tiempo especificado. El intervalo debe ser el mismo que el establecido en el nivel de informe. Por ejemplo, si el informe muestra el último trimestre completo de Ingresos por semana, puede establecer el intervalo de tiempo de la ventana promedio móvil en cuatro semanas. Esto hace que los tres primeros valores sean nulos y el cuarto valor representa el promedio de las primeras cuatro semanas de ingresos. Para una mayor claridad, asegúrese de desactivar el `Multiple Y-Axes` casilla de verificación si está viendo la misma métrica con un promedio móvil, como en el ejemplo siguiente.

![](../assets/rolling_avg_window.png)

### Opciones de tiempo específicas de la métrica

Existen dos opciones para las métricas utilizadas en los informes: pueden generar tendencias en el tiempo según las opciones de tiempo globales o no, lo que las mostrará como un número escalar.

Cambiar un intervalo de tiempo de métrica a `None` devuelve un valor `scalar` número, lo que resulta útil al crear fórmulas que implican la división de una métrica de tendencias temporales por un `scalar` número. Además, también puede cambiar el intervalo de tiempo del `scalar` a un intervalo de tiempo independiente del del informe.

Por ejemplo, supongamos que desea ver los ingresos mensuales de 2019 expresados como un porcentaje de los ingresos generales de 2019. Puede añadir dos `Revenue` métricas de a un informe con un intervalo de tiempo global del 1 de enero de 2019 al 31 de diciembre de 2019, segmentado por intervalo mensual.

>[!NOTE]
>
>Si añade `group by` , elija una nueva visualización o ajuste el intervalo de tiempo y, a continuación, guarde solo el número (`scalar`). Estos ajustes no se conservarán la próxima vez que abra ese informe desde un panel, solo se conservará el intervalo de tiempo.

Para obtener más información sobre el uso de las opciones de tiempo en los informes, consulte lo siguiente [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Paso 7: Guardar el informe

Cuando cree un gráfico, puede guardarlo haciendo clic en **[!UICONTROL Save]** en la esquina superior derecha de la `Visual Report Builder`.

Puede elegir guardar un gráfico, una tabla o un número (`scalar`) usando el `Type` y el tablero en el que se debe guardar el informe usando la variable `Location` desplegable.

A continuación, puede guardar el informe haciendo clic en **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Salidas de informe

Para ayudarle a decidir qué resultado del informe elegir, consulte lo siguiente:

### Gráfico

![](../assets/RB_Chart.png)

### Tabla

![](../assets/RB_Table.png)

### Número (`scalar`)

![](../assets/RB_Scalar.png)

¡Felicidades! Ha terminado.
