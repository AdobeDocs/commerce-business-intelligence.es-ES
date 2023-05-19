---
title: Uso de la columna calculada Diferencia de fechas
description: Conozca el propósito y los usos de la columna calculada Diferencia de fechas.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# Columna calculada de diferencia de fecha

En este tema se describen el propósito y los usos del `Date Difference` columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

El `Date Difference` el tipo de columna calcula el tiempo entre dos eventos que pertenecen a un único registro, basándose en las marcas de tiempo del evento. El valor sin procesar calculado en esta columna se expresa en segundos, pero se convierte automáticamente a minutos, horas, días, etc., para que se muestre en los informes. Sin embargo, cuando se utiliza como filtro/grupo por, desea utilizar el valor en segundos.

A `date difference` la columna calculada se puede utilizar para crear una métrica que calcule el promedio o la mediana de tiempo entre dos eventos, como el tiempo promedio entre el registro de clientes y sus primeros pedidos.

**Ejemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


En el ejemplo anterior, la variable `Date Difference` es la columna `Seconds between timestamp_2 and timestamp_1` columna. Realiza el cálculo `timestamp_2 minus timestamp_1`.

**Mecánica**

Los pasos siguientes describen cómo crear un `Date Difference` columna.

1. Vaya a **[!DNL Manage Data > Data Warehouse]** página.
1. Desplácese hasta la tabla en la que desee crear esta columna.
1. Clic **[!UICONTROL Create a Column]** y configure la columna de la siguiente manera:
   * Seleccionar `Column Definition Type` > `Same Table`
   * Seleccionar `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleccionar `Ending DATETIME` columna > Elija el campo de fecha y hora de finalización, que suele ser el evento que se produce más adelante
   * Seleccionar `Starting DATETIME` column** > Elija el campo de fecha y hora de inicio, que suele ser el evento que se produce antes

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.
1. La columna está disponible para usar *inmediatamente*.

Por ejemplo, el siguiente ejemplo está configurado para calcular la variable `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
