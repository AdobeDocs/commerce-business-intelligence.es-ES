---
title: Columna calculada de número de evento
description: Conozca el propósito y los usos de la columna calculada Número de evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Columna calculada de número de evento

Este tema describe el propósito y los usos de la columna calculada `Event Number` disponible en la página **[!DNL Manage Data > Data Warehouse]**. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

El tipo de columna `Event Number` identifica la secuencia en la que ocurrieron los eventos para un **propietario de evento** en particular, como un `customer` o `user`. Si está familiarizado con SQL, este tipo de columna es idéntico a la función `RANK`. Se puede utilizar para observar diferencias de comportamiento entre los eventos de primera vez, los eventos repetidos o los eventos n en los datos.

En caso de empate, esta columna contiene el mismo **rango** para los eventos vinculados y omite los números subsiguientes. Por ejemplo, si se clasificaran los números 5,8,10,10,12, los rangos serían 1,2,3,3,5.

El caso de uso más común de esta columna es analizar los compradores nuevos y los compradores habituales. La primera vez que se identifican compradores es agregando un filtro (a una métrica o informe) en `Customer's order number` = 1. `Customer's order number` es una columna de tipo `Event Number`.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 00:00:00 del 01-01-2015 | 1 |
| **2 | B | 00:30:00 del 01-01-2015 | 1 |
| **3 | A | 01-01-2015 02:00:00 | 2 |
| **4 | A | 02-01-2015 13:00:00 | 3 |
| **5 | B | 03-01-2015 13:00:00 | 2 |

En el ejemplo anterior, la columna `Owner's event number` es una columna `Event Number`. Clasifica los eventos del propietario en el orden en que se produjeron (según la columna `timestamp`).

Por ejemplo, considere todas las filas donde `owner_id = A`. La primera fila de la tabla es la marca de tiempo más antigua para este propietario, seguida de la tercera fila de la tabla, seguida de la cuarta fila de la tabla.

**Mecánica**

Estas son algunas instrucciones para crear una columna `Event Number`:

1. Vaya a la página **[!UICONTROL Manage Data > Data Warehouse]**.

1. Desplácese hasta la tabla en la que desee crear esta columna.

1. Haga clic en **[!UICONTROL Create a Column]** y elija el tipo de columna `EVENT_NUMBER (…)`: en la sección `Same Table`.

1. La primera lista desplegable `Event Owner` especifica la entidad para la cual se va a determinar la clasificación. En el caso de `Customer's order number`, un identificador de cliente como `customer_id` o `customer_email` sería `Event Owner`.

1. La segunda lista desplegable `Event Rank` especifica la columna que aplica la secuencia que determina el rango de la fila. En el caso de un `Customer's order number`, la marca de tiempo de `created_at` sería `Event Rank`.

1. En el menú desplegable `Options`, puede agregar filtros para excluir las filas de la consideración. Las filas excluidas tienen un valor `NULL` para esta columna.

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.

1. La columna está disponible para usar _inmediatamente._
