---
title: Columna calculada del número de evento
description: Conozca el propósito y los usos de la columna calculada Número de evento .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Columna calculada del número de evento

Este tema describe el propósito y los usos del `Event Number` la columna calculada disponible en la **[!DNL Manage Data > Data Warehouse]** página. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

La variable `Event Number` tipo de columna: identifica la secuencia en la que se produjeron eventos para un **propietario del evento**, como un `customer` o `user`. Si está familiarizado con SQL, este tipo de columna es idéntico al del `RANK` función. Se puede usar para observar diferencias de comportamiento entre eventos nuevos, eventos repetidos o eventos nth en los datos.

En el caso de los vínculos, esta columna contiene lo mismo **rank** para los eventos vinculados y omite los números siguientes. Por ejemplo, si clasificara los números 5,8,10,10,12, los rangos serían 1,2,3,3,5.

El caso de uso más común de esta columna es el análisis de compradores nuevos y compradores repetitivos. La primera vez que se identifican los compradores añadiendo un filtro (a una métrica o a un informe) en `Customer's order number` = 1. `Customer's order number` es una columna del tipo `Event Number`.

**Ejemplo**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

En el ejemplo anterior, la columna `Owner's event number` es un `Event Number` para abrir el Navegador. Clasifica los eventos del propietario en el orden en que se produjeron (según la variable `timestamp` ).

Por ejemplo, considere todas las filas donde `owner_id = A`. La primera fila de la tabla es la marca de tiempo más temprana para este propietario, seguida de la tercera fila de la tabla, seguida de la cuarta fila de la tabla.

**Mecánicos**

Estas son algunas instrucciones para crear una `Event Number` columna:

1. Vaya a la **[!UICONTROL Manage Data > Data Warehouse]** página.
1. Desplácese a la tabla en la que desea crear esta columna.
1. Haga clic en **[!UICONTROL Create a Column]** y seleccione `EVENT_NUMBER (…)` tipo de columna: en el `Same Table` para obtener más información.
1. Primer menú desplegable `Event Owner` especifica la entidad para la que se va a determinar la clasificación. En el caso de `Customer's order number`, un identificador de cliente como `customer_id` o `customer_email` sería el `Event Owner`.
1. La segunda lista desplegable `Event Rank` especifica la columna que aplica la secuencia que determina la clasificación de la fila. En el caso de `Customer's order number`, el `created_at` la marca de tiempo sería `Event Rank`.
1. En el `Options` , puede agregar filtros para excluir filas de la posibilidad de que se consideren. Las filas excluidas tendrán un `NULL` para esta columna.
1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.
1. La columna estará disponible para usar _inmediatamente._
