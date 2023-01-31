---
title: Columna calculada de comparación secuencial
description: Conozca el propósito y los usos de la columna calculada Comparación secuencial .
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Columna calculada de comparación secuencial

Este tema describe el propósito y los usos del `Sequential Comparison` la columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

La variable `Sequential Comparison` tipo de columna: encuentra la diferencia entre eventos consecutivos. El tipo más común de `Sequential Comparison` es la `Seconds since previous order` para abrir el Navegador. Se necesitan tres entradas para esta columna:

1. `Event Owner`: Esta entrada determina la entidad para la que se agrupan las filas. Por ejemplo, en la `Seconds since previous order` , el propietario del evento es el cliente, ya que queremos encontrar el número de segundos desde el pedido anterior del mismo cliente.
1. `Event Date`: Esta entrada fuerza la secuencia de eventos. En el caso de `Seconds since previous order`, la columna que contiene la marca de tiempo del pedido debe ser `Event Date`. Esta entrada es siempre una marca de tiempo.
1. `Value to Compare`: Esta entrada es el valor real que se va a comparar. Resta el valor de la fila anterior del valor de la fila actual. Por lo tanto, se llama a una columna que encuentra la diferencia horaria entre pedidos sucesivos de un cliente `Seconds since previous order`. Esta entrada no tiene que ser una marca de tiempo. Un ejemplo sin marca de hora es encontrar la diferencia en el valor de pedido entre pedidos sucesivos de un cliente.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 01-01-2015:00:00 | NULL |
| **`2`** | B | 01-01-2015:30:00 | NULL |
| **`3`** | A | 01-01-2015:00:00 | 7200 |
| **`4`** | A | 2015-01-02 14:00:00 | 126000 |
| **`5`** | B | 2015-01-03 14:00:00 | 217800 |

En el ejemplo anterior, `Seconds since owner's previous event` es la variable `Sequential Comparison` columna calculada. Para la variable `owner_id = A`, primero identifica una secuencia basada en la variable `timestamp` y, a continuación, resta el valor de `timestamp` desde la marca de tiempo del evento actual. En la tercera fila de la tabla: la segunda fila de `owner_id A` - el valor de `Seconds since owner's previous event` es el número de segundos entre &quot;2015-01-01 02:00&quot; y &quot;2015-01-01 00:00:00&quot;. Esta diferencia es igual a 2 horas = 7200 segundos.

Para este tipo de columna calculada, la fila correspondiente al primer evento del propietario tiene un `NULL` valor.

**Mecánicos**

Para crear un **Número de evento** columna:

1. Vaya a la **[!DNL Manage Data** > **Data Warehouse]** página.
1. Desplácese a la tabla en la que desea crear esta columna.
1. Haga clic en **[!UICONTROL Create New Column]** en la parte superior derecha de la pantalla.
1. Select `Same Table` como el `Definition Type` (si las columnas que desea comparar no están en la misma tabla, es posible que tenga que reubicarlas).
1. Select `SEQUENTIAL_COMPARISON` como el `Column Definition Equation`.
1. Elija las entradas, como se explica más arriba:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`
1. También se pueden agregar filtros para excluir filas de la posibilidad de que se consideren. Las filas excluidas tendrán un valor NULL para esta columna.
1. Asigne un nombre a la columna de la parte superior de la página y haga clic en **[!UICONTROL Save]**.
1. La columna estará disponible para usar *inmediatamente*.

![SEC](../../assets/SEC_new.png)
