---
title: Columna calculada de comparación secuencial
description: Conozca el propósito y los usos de la columna calculada Comparación secuencial.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Columna calculada de comparación secuencial

Este tema describe el propósito y los usos de la columna calculada `Sequential Comparison` disponible en la página **[!DNL Manage Data > Data Warehouse]**. A continuación se explica lo que hace, seguido de un ejemplo y la mecánica de crearlo.

**Explicación**

El tipo de columna `Sequential Comparison`: encuentra la diferencia entre eventos consecutivos. El tipo más común de la columna `Sequential Comparison` es la columna `Seconds since previous order`. Se necesitan tres entradas para esta columna:

1. `Event Owner`: esta entrada determina la entidad para la que se agrupan las filas. Por ejemplo, en la columna `Seconds since previous order`, el propietario del evento es el cliente, ya que desea averiguar la cantidad de segundos transcurridos desde el pedido anterior del mismo cliente.
1. `Event Date`: esta entrada aplica la secuencia de eventos. En los casos de `Seconds since previous order`, la columna que contiene la marca de tiempo del pedido debe ser la `Event Date`. Esta entrada siempre es una marca de tiempo.
1. `Value to Compare`: esta entrada es el valor real que se va a comparar. Resta el valor de la fila anterior del valor de la fila actual. Por lo tanto, una columna que encuentra la diferencia horaria entre pedidos sucesivos de un cliente se llama `Seconds since previous order`. Esta entrada no tiene que ser una marca de tiempo. Un ejemplo que no es de marca de hora es buscar la diferencia en el valor de pedido entre pedidos sucesivos de un cliente.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 00:00:00 del 01-01-2015 | NULL |
| **`2`** | B | 00:30:00 del 01-01-2015 | NULL |
| **`3`** | A | 01-01-2015 02:00:00 | 7200 |
| **`4`** | A | 02-01-2015 13:00:00 | 126000 |
| **`5`** | B | 03-01-2015 13:00:00 | 217800 |

En el ejemplo anterior, `Seconds since owner's previous event` es la columna calculada `Sequential Comparison`. Para `owner_id = A`, primero identifica una secuencia basada en la columna `timestamp` y, a continuación, resta el evento anterior `timestamp` de la marca de tiempo del evento actual. En la tercera fila de la tabla (la segunda fila de `owner_id A`), el valor de `Seconds since owner's previous event` es el número de segundos entre &#39;2015-01-01 02:00&#39; y &#39;2015-01-01 00:00:00&#39;. Esta diferencia es igual a dos horas = 7200 segundos.

Para este tipo de columna calculada, la fila correspondiente al primer evento del propietario tiene un valor `NULL`.

**Mecánica**

Para crear una columna **Número de evento**:

1. Vaya a la página **[!DNL Manage Data > Data Warehouse]**.

1. Desplácese hasta la tabla en la que desee crear esta columna.

1. Haga clic en **[!UICONTROL Create New Column]** en la esquina superior derecha.

1. Seleccione `Same Table` como `Definition Type` (si las columnas que desea comparar no están en la misma tabla, puede que tenga que reubicarlas).

1. Seleccione `SEQUENTIAL_COMPARISON` como `Column Definition Equation`.

1. Elija las entradas, tal como se explica más arriba:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. También se pueden añadir filtros para excluir filas de la consideración. Las filas excluidas tienen un valor `NULL` para esta columna.

1. Proporcione un nombre para la columna en la parte superior de la página y haga clic en **[!UICONTROL Save]**.

1. La columna está disponible para usar *inmediatamente*.

![SEG](../../assets/SEC_new.png)
