---
title: Columna calculada de comparación secuencial
description: Conozca el propósito y los usos de la columna calculada Comparación secuencial.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Columna calculada de comparación secuencial

En este tema se describen el propósito y los usos del `Sequential Comparison` columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo y la mecánica de crearlo.

**Explicación**

El `Sequential Comparison` tipo de columna: encuentra la diferencia entre eventos consecutivos. El tipo más común de `Sequential Comparison` es la columna `Seconds since previous order` columna. Se necesitan tres entradas para esta columna:

1. `Event Owner`: esta entrada determina la entidad para la que se agrupan las filas. Por ejemplo, en la variable `Seconds since previous order` , el propietario del evento es el cliente, ya que desea obtener el número de segundos desde el pedido anterior del mismo cliente.
1. `Event Date`: Esta entrada fuerza la secuencia de eventos. En los casos de `Seconds since previous order`, la columna que contiene la marca de tiempo del pedido debe ser `Event Date`. Esta entrada siempre es una marca de tiempo.
1. `Value to Compare`: esta entrada es el valor real que se va a comparar. Resta el valor de la fila anterior del valor de la fila actual. Por lo tanto, se llama a una columna que encuentra la diferencia horaria entre pedidos sucesivos de un cliente `Seconds since previous order`. Esta entrada no tiene que ser una marca de tiempo. Un ejemplo que no es de marca de hora es buscar la diferencia en el valor de pedido entre pedidos sucesivos de un cliente.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 00-01-2015:00:00 | NULL |
| **`2`** | B | 00-01-2015:30:00 | NULL |
| **`3`** | A | 02-01-2015:00:00 | 7200 |
| **`4`** | A | 02-01-2015 13:00:00 | 126000 |
| **`5`** | B | 03-01-2015 13:00:00 | 217800 |

En el ejemplo anterior, `Seconds since owner's previous event` es el `Sequential Comparison` columna calculada. Para el `owner_id = A`, primero identifica una secuencia basada en la variable `timestamp` y, a continuación, resta el del evento anterior `timestamp` de la marca de tiempo del evento actual. En la tercera fila de la tabla, la segunda fila para `owner_id A` - el valor de `Seconds since owner's previous event` es el número de segundos entre &quot;2015-01-01 02:00&quot; y &quot;2015-01-01 00:00:00&#39;. Esta diferencia es igual a dos horas = 7200 segundos.

Para este tipo de columna calculada, la fila correspondiente al primer evento del propietario tiene un `NULL` valor.

**Mecánica**

Para crear un **Número de evento** columna:

1. Vaya a **[!DNL Manage Data > Data Warehouse]** página.

1. Desplácese hasta la tabla en la que desee crear esta columna.

1. Clic **[!UICONTROL Create New Column]** en la esquina superior derecha.

1. Seleccionar `Same Table` como el `Definition Type` (si las columnas que desea comparar no están en la misma tabla, es posible que tenga que reubicarlas).

1. Seleccionar `SEQUENTIAL_COMPARISON` como el `Column Definition Equation`.

1. Elija las entradas, tal como se explica más arriba:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. También se pueden añadir filtros para excluir filas de la consideración. Las filas excluidas tienen un `NULL` valor de esta columna.

1. Proporcione un nombre a la columna en la parte superior de la página y haga clic en **[!UICONTROL Save]**.

1. La columna está disponible para usar *inmediatamente*.

![SEC](../../assets/SEC_new.png)
