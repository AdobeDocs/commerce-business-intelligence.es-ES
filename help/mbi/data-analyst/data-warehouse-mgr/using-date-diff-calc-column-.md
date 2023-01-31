---
title: Uso de la columna Diferencia de fechas calculadas
description: Conozca el propósito y los usos de la columna calculada Diferencia de fechas .
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Columna calculada de diferencia de fechas

Este tema describe el propósito y los usos del `Date Difference` la columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

La variable `Date Difference` tipo de columna: encuentra el tiempo entre dos eventos que pertenecen a un único registro, en función de las marcas de tiempo del evento. El valor sin procesar calculado en esta columna se expresa en segundos, pero se convertirá automáticamente en minutos, horas, días, etc. para mostrarlo en los informes. Sin embargo, cuando se usa como filtro o grupo por, se recomienda utilizar el valor en segundos.

A `date difference` la columna calculada se puede usar para crear una métrica que calcule el tiempo promedio o medio entre dos eventos, como el tiempo promedio entre el registro del cliente y sus primeros pedidos.

**Ejemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 01-01-2015:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 01-01-2015:00:00 | 2015-01-01 11:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


En el ejemplo anterior, la variable `Date Difference` es la `Seconds between timestamp_2 and timestamp_1` para abrir el Navegador. Realiza el cálculo `timestamp_2 minus timestamp_1`.

**Mecánicos**

Los siguientes pasos describen cómo crear una `Date Difference` para abrir el Navegador.

1. Vaya a la **[!DNL Manage Data > Data Warehouse]** página.
1. Desplácese a la tabla en la que desea crear esta columna.
1. Haga clic en **[!UICONTROL Create a Column]** y configure la columna de la siguiente manera:
   * Select `Column Definition Type` > `Same Table`
   * Select `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Select `Ending DATETIME` columna > Elija el campo fecha y hora de finalización, que suele ser el evento que se produce más adelante
   * Select `Starting DATETIME` column** > Elija el campo fecha y hora de inicio, que suele ser el evento que ocurre anteriormente

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.
1. La columna estará disponible para usar *inmediatamente*.

Por ejemplo, se configura el siguiente ejemplo para calcular la variable `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
