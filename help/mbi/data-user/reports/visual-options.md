---
title: Opciones de visualización en el Report Builder visual
description: Aprenda a utilizar las opciones de visualización en el Report Builder visual.
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---

# Opciones de visualización

La selección de la visualización correcta para un conjunto de datos determinado es una parte fundamental del proceso analítico. Cada conjunto de datos tiene una historia que contar, pero el efecto de esa historia se destaca por su impacto visual y legibilidad.

La variable [!DNL MBI] `Visual Report Builder` ofrece 12 opciones de visualización diferentes, cada una con sus propias ventajas y casos de uso. Este artículo analiza las distintas opciones de visualización de [!DNL MBI], incluidas las configuraciones de informe necesarias cuando corresponda, así como un ejemplo de caso de uso. Las visualizaciones siguientes están disponibles en MBI:

* `Scalar`
* `Table`
* `Line`
* `Bar`
* `Stacked Bar`
* `Column`
* `Stacked Column`
* `Pie`
* `Area`
* `Funnel`
* `Scatter plot`
* `Bubble`
* `Heatmap`

## `Scalar`

`Scalar` los informes se muestran como un solo valor numérico. La mayoría de las veces, esto se usa para mostrar el valor &quot;todo el tiempo&quot; de una métrica clave, como ingresos o pedidos, o para comparar los ingresos con la fecha y el presupuesto con dos informes escalares independientes. En el siguiente ejemplo, esto simplemente muestra el número total de pedidos para el intervalo de informes dado:

![](../../assets/blobid0.png)

Para guardar un informe como escalar, configure los filtros y la configuración de tiempo y haga clic en **[!UICONTROL Save]** o **[!UICONTROL Update]** en la parte superior derecha del informe. En el `Type` , elija Número: Nombre de la métrica para guardar el informe como el valor que se muestra en la barra lateral izquierda.

![](../../assets/blobid1.png)

**Requisitos**:

* `Time interval`: `None`
* `Group by`: `None`
* Solo una métrica

## `Table`

Como sugiere el nombre, `table` los informes son buenos para mostrar los detalles de las tablas. Cuando es necesario mostrar un gran número de grupos por valores o métricas en un solo informe, una tabla suele ser la mejor manera de hacerlo. Por ejemplo, a continuación se muestra una tabla de &quot;Detalles del cliente&quot; que muestra los pedidos y los ingresos agrupados por correo electrónico del cliente:

![](../../assets/blobid2.png)

Al igual que los informes escalares, puede guardar un informe como una tabla haciendo clic en **[!UICONTROL Save]** o **[!UICONTROL Update]** dentro del creador de informes, seleccione la opción Tabla en la sección `Type` lista desplegable.

![](../../assets/blobid3.png)

**Requisitos:**

* Aunque no hay requisitos de configuración de informes, es importante tener en cuenta que las tablas están limitadas a 3500 filas. Si el conjunto de datos incluye más de 3500 filas, deberá filtrar los resultados para reducir el ámbito o exportar los resultados a `.csv` o `Excel` para ver el conjunto de datos completo.

## `Line`

`Line` los gráficos son la elección perfecta para comparar el rendimiento de cohortes de métricas similares. Por ejemplo, analizar los ingresos de dos regiones durante el mismo período de tiempo o comparar el crecimiento interanual de los pedidos realizados, como se muestra a continuación:

![](../../assets/blobid0.png)

Cada métrica y fórmula agregadas al informe se representa mediante su propia línea. Al comparar métricas con unidades y escalas similares, no olvide marcar la casilla de verificación de `Multiple Y-Axes` para mostrar todas las métricas en la misma escala.

Para guardar un informe como un gráfico de líneas, ajuste el informe `Type` a `Chart`y seleccione la visualización adecuada desde el creador de informes, como se muestra a continuación:

![](../../assets/blobid1.png)

**Requisitos:**

* Ninguna

## `Bar`

`Bar` los gráficos muestran los datos como una serie de barras horizontales y son ideales para mostrar el rendimiento general de un número limitado de métricas o agrupar por valores. Por ejemplo, se podría usar un gráfico de barras para comparar los ingresos por almacén:

![](../../assets/blobid2.png)

Cada combinación de métrica, grupo por e intervalo de tiempo se muestra como su propia barra. Si tiene dos métricas con una `group by`, que contiene tres `group by` , el informe mostrará seis barras independientes.

Para guardar un informe como un gráfico de barras, ajuste el informe `Type` a `Chart` y seleccione `Bar` como se muestra a continuación:

![](../../assets/blobid3.png)

**Requisitos:**

* Ninguna

## `Stacked Bar`

`Stacked bar` los gráficos son similares a los de sus hermanos de gráficos de barras, con la capacidad adicional de mostrar el desglose proporcional de cada barra. Con frecuencia, los gráficos de barras apiladas se configuran con dos o más métricas y con un solo grupo por, de modo que cada barra representa un grupo único por valor que se divide entre sus componentes de métricas.

Por ejemplo, el informe siguiente tiene dos métricas de ingresos idénticas: uno se filtró para pedidos nuevos y el otro para pedidos repetidos. Después de agrupar por tienda, puede ver la contribución de ingresos total para cada tienda (representada por la anchura total de la barra) así como el desglose de ingresos por primera vez frente a repetición para cada tienda:

![](../../assets/blobid4.png)

Asegúrese de que la variable `Multiple Y-Axes` no está marcada al configurar un informe como el anterior.

Para guardar un informe como un gráfico de barras apiladas, ajuste el informe `Type` a `Chart` y seleccione la opción de barra apilada del creador de informes:

![](../../assets/blobid5.png)

**Requisitos:**

* Ninguna

## `Column`

`Column` los gráficos representan cada punto de datos como una columna vertical y, por lo general, son mejores para mostrar los datos de tendencias horarias que la visualización de gráficos de barras horizontales. Dado que cada métrica única y cada grupo por combinación se representan en su propia serie de barras, los informes de columna generalmente son mejores para los informes con tres o menos métricas, o bien para una métrica con un solo grupo que contenga entre 1 y 3 grupos por valores.

En el ejemplo siguiente, se muestran dos métricas de ingresos, una filtrada para los ingresos por primera vez y otra para los ingresos repetidos, con tendencias de un mes a otro:

![](../../assets/blobid6.png)

Los informes de columna se pueden guardar cambiando el informe `Type` a `Chart`y seleccionando la opción de visualización de columna:

![](../../assets/blobid7.png)

**Requisitos:**

* Ninguna

## `Stacked Column`

`Stacked column` los informes son casi idénticos a los gráficos de columnas, excepto que columnas similares se apilan unas encima de otras, de modo que la altura total representa la suma de los valores. Las columnas apiladas se visualizan de nuevo mejor con un número limitado de métricas o grupos individuales.

Uso de la misma configuración de informe que se describe en la sección `Column` sección anterior, un informe con dos métricas de ingresos (filtrados por primera vez y repetidos) tendría el aspecto siguiente con una visualización de columna apilada:

![](../../assets/blobid8.png)

Una vez más, es importante que `Multiple Y-Axes` Cuando se muestran varias métricas con la visualización de columnas apiladas, se borra la casilla de verificación.

Para guardar un informe como una columna apilada, establezca el informe `Type` a `Chart` y seleccione `stacked column` opción:

![](../../assets/blobid9.png)

**Requisitos:**

* Ninguna

## `Pie`

`Pie` los gráficos son mejores para mostrar una única métrica con uno o más grupos de amigos o varias métricas sin grupos de amigos. En cualquier caso, el intervalo de tiempo debe establecerse en ninguno para que se muestren los datos en un gráfico circular. En el siguiente ejemplo, una métrica de pedidos individual se agrupa por nombre de almacén para mostrar el desglose de pedidos por almacén:

![](../../assets/blobid10.png)

Para guardar un informe como gráfico circular, establezca el informe `Type` a `Chart` y seleccione `pie` como se muestra a continuación:

![](../../assets/blobid11.png)

**Requisitos:**

* `Time interval`: `None`
* Cualquiera de los siguientes:
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area` los gráficos son casi idénticos a los gráficos de columnas apiladas, excepto que las columnas se muestran continuamente. Al igual que las columnas apiladas, los gráficos de áreas se visualizan mejor con un número limitado de grupos o métricas.

Tomar el mismo ejemplo de la variable `stacked column` , el informe siguiente muestra los ingresos por primera vez frente a los ingresos repetidos con la visualización del gráfico de áreas:

![](../../assets/blobid12.png)

Para guardar un informe como un gráfico de áreas, ajuste la variable `Type` a `Chart` y seleccione la opción de área:

![](../../assets/blobid13.png)

**Requisitos:**

* Ninguna

## `Funnel`

`Funnel` los gráficos son perfectos para visualizar la conversión en una secuencia esperada de eventos. Algunos ejemplos incluyen el análisis de los posibles ingresos en el canal de ventas desde posibles clientes hasta contratos cerrados, o la medición de la caída de clientes entre sus primeros y segundos pedidos, segundos y terceros pedidos, etc. A continuación se muestra un ejemplo de esta última:

![](../../assets/blobid4.png)

En un informe de canal, el valor relativo de un paso determinado del canal se refleja en la altura del paso y el orden en que se muestran los pasos se determina mediante la configuración del informe. Existen dos formas de configurar un informe de canal:

* `Single metric with one group by`: - Orden de los pasos determinados por la configuración &quot;Mostrar arriba/abajo&quot; del grupo por. De forma predeterminada, los pasos del canal se muestran en orden desde el valor más grande hasta el más pequeño, pero también puede ordenarlos alfabéticamente por el grupo por nombre.

* `Multiple metrics with no group by`: - Orden de los pasos determinados por el orden en que las métricas se agregan al informe.

Para guardar un informe como un gráfico de canales, ajuste el informe `Type` a `Chart` y seleccione la visualización adecuada desde el creador de informes.

![](../../assets/blobid5.png)

**Requisitos:**

* `Time interval`: `None`
* Cualquiera de los siguientes:
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

A `scatter plot` se utiliza para examinar la relación de una métrica con dos variables diferentes, de modo que pueda identificar fácilmente correlaciones y valores periféricos. Este tipo de visualización es mejor utilizarla solo con dimensiones numéricas; pruébelo con la métrica Pedidos y la variable `Customer's lifetime number of coupons` y `Customer's lifetime revenue` dimensiones para ver cómo se relaciona el uso de cupones con los ingresos. Puede elegir entre un diagrama de puntos con y sin una línea de tendencia:

![](../../assets/scatter-plot-1.png)

![sin línea de tendencia](../../assets/scatter-plot-2.png)

![](../../assets/scatter-plot-3.png)

![Con línea de tendencia](../../assets/scatter-plot-4.png)

**Requisitos:**

Opción 1:

* Two `metrics`
* One `group by`
* `Time interval`: `None`

Opción 2:

* Two `metrics`
* No `group by`
* Establezca `time interval`

## `Bubble` gráfico

A `bubble` El gráfico puede mostrar hasta cuatro dimensiones de datos en las que la variable `X` y `Y` los ejes especifican la ubicación de las burbujas, la variable `Z` eje es el tamaño de las burbujas y, al incluir dos grupos de barras, puede añadir color a las burbujas. Este tipo de visualización es mejor cuando desea trazar varias dimensiones de datos en un único gráfico.

Por ejemplo, en el siguiente gráfico se muestra el número de clientes (tamaño de burbuja) agrupados por una fuente de adquisición específica (color de burbuja) y un estado (varias burbujas de color específico), calculados en función de los ingresos totales y los pedidos de duración promedio.

![](../../assets/bubble-1.png)

En el siguiente gráfico se muestra el número de clientes (tamaño de burbuja) agrupados por fuente de adquisición (color de burbuja) y estado (varias burbujas en color específico), calculados en relación con el valor de duración promedio y los ingresos totales.

![](../../assets/bubble-2.png)

**Requisitos para el gráfico de burbujas de una sola serie:**

Opción 1

* Tres `metrics`
* One `group by`
* `Time interval`: `None`

Opción 2

* Tres `metrics`
* No `group by`
* Establezca `time interval`

**Requisitos para el gráfico de burbujas de varias series:**

* Tres `metrics`
* Two `group by`
* `Time interval`: `None`

## `Heatmap`

Uso `heatmaps` para visualizar las zonas interactivas de los datos. Por ejemplo, un mapa de calor puede indicar dónde se obtiene un volumen mayor de forma rutinaria. La visualización de estos datos puede ayudarle a ajustar los niveles de inventario para asegurarse de satisfacer la demanda durante las ventanas de mayor volumen.

El siguiente mapa de calor muestra los pedidos día a semana por hora del día en conjunto, durante varias semanas.

![](../../assets/heat-map.png)<!--{: width="650"}-->

**Requisitos:**

Opción 1

* One `metric`
* Two `group by`
* `Time interval`: `None`

Opción 2

* One `metric`
* One `group by`
* Establezca `time interval`
