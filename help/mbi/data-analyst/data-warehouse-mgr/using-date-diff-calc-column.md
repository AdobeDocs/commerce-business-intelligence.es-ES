---
title: Uso de la columna calculada Diferencia de fechas
description: Conozca el propósito y los usos de la columna calculada Diferencia de fechas.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Columna calculada de diferencia de fecha

Este tema describe el propósito y los usos de la columna calculada `Date Difference` disponible en la página **[!DNL Manage Data > Data Warehouse]**. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

El tipo de columna `Date Difference` calcula el tiempo entre dos eventos que pertenecen a un único registro, basándose en las marcas de tiempo del evento. El valor sin procesar calculado en esta columna se expresa en segundos, pero se convierte automáticamente a minutos, horas, días, etc., para que se muestre en los informes. Sin embargo, cuando se utiliza como filtro/grupo por, desea utilizar el valor en segundos.

Se puede usar una columna calculada `date difference` para crear una métrica que calcule el promedio o la mediana de tiempo entre dos eventos, como el tiempo promedio entre el registro de clientes y sus primeros pedidos.

**Ejemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 00:00:00 del 01-01-2015 | 01-01-2015 12:30:00 | 45000 |
| `B` | 08:00:00 de enero de 2015 | 01-01-2015 10:00:00 | 7200 |

{style="table-layout:auto"}


En el ejemplo anterior, la columna `Date Difference` es la columna `Seconds between timestamp_2 and timestamp_1`. Realiza el cálculo `timestamp_2 minus timestamp_1`.

**Mecánica**

Los pasos siguientes describen cómo crear una columna `Date Difference`.

1. Vaya a la página **[!DNL Manage Data > Data Warehouse]**.
1. Desplácese hasta la tabla en la que desee crear esta columna.
1. Haga clic en **[!UICONTROL Create a Column]** y configure la columna de la siguiente manera:
   * Seleccionar `Column Definition Type` > `Same Table`
   * Seleccionar `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleccione la columna `Ending DATETIME` > Elija el campo de fecha y hora de finalización, que suele ser el evento que se produce más adelante
   * Seleccione la columna `Starting DATETIME`** > Elija el campo de fecha y hora de inicio, que suele ser el evento que se produce antes

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.
1. La columna está disponible para usar *inmediatamente*.

A modo de ejemplo, el siguiente ejemplo está configurado para calcular `Seconds between order date and customer's creation date`:

![Configuración de cálculo de diferencia de fecha que muestra selecciones de columna datetime](../../assets/date_diff.png)
