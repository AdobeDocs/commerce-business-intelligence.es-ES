---
title: Columna calculada de número de evento
description: Conozca el propósito y los usos de la columna calculada Número de evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# Columna calculada de número de evento

En este tema se describen el propósito y los usos del `Event Number` columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

El `Event Number` El tipo de columna identifica la secuencia en la que se produjeron los eventos para un **propietario del evento**, como un `customer` o `user`. Si está familiarizado con SQL, este tipo de columna es idéntico al `RANK` función. Se puede utilizar para observar diferencias de comportamiento entre los eventos de primera vez, los eventos repetidos o los eventos n en los datos.

En caso de empate, esta columna contiene lo mismo **clasificar** para los eventos vinculados y omite los números subsiguientes. Por ejemplo, si se clasificaran los números 5,8,10,10,12, los rangos serían 1,2,3,3,5.

El caso de uso más común de esta columna es analizar los compradores nuevos y los compradores habituales. Identificar a los compradores por primera vez añadiendo un filtro (a una métrica o informe) en `Customer's order number` = 1. `Customer's order number` es una columna del tipo `Event Number`.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

En el ejemplo anterior, la columna `Owner's event number` es un `Event Number` columna. Clasifica los eventos del propietario en el orden en que ocurrieron (según el `timestamp` columna).

Por ejemplo, considere todas las filas donde `owner_id = A`. La primera fila de la tabla es la marca de tiempo más antigua para este propietario, seguida de la tercera fila de la tabla, seguida de la cuarta fila de la tabla.

**Mecánica**

Estas son algunas instrucciones para crear un `Event Number` columna:

1. Vaya a **[!UICONTROL Manage Data > Data Warehouse]** página.

1. Desplácese hasta la tabla en la que desee crear esta columna.

1. Clic **[!UICONTROL Create a Column]** y elija la `EVENT_NUMBER (…)` tipo de columna: en `Same Table` sección.

1. La primera lista desplegable `Event Owner` especifica la entidad para la que se va a determinar la clasificación. En caso de que `Customer's order number`, un identificador de cliente como `customer_id` o `customer_email` sería el `Event Owner`.

1. La segunda lista desplegable `Event Rank` especifica la columna que aplica la secuencia que determina el rango de la fila. En caso de que `Customer's order number`, el `created_at` timestamp sería el `Event Rank`.

1. En el `Options` , puede añadir filtros para excluir las filas de la consideración. Las filas excluidas tienen un `NULL` valor de esta columna.

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.

1. La columna está disponible para usar _inmediatamente._
