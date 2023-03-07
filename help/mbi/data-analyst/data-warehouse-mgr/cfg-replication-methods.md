---
title: Configuración de métodos de replicación
description: Conozca cómo se organizan las tablas y cómo se comportan los datos de la tabla para poder elegir el mejor método de replicación para sus tablas.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Configuración de métodos de replicación

`Replication` métodos y [nuevas comprobaciones](../data-warehouse-mgr/cfg-data-rechecks.md) se utilizan para identificar datos nuevos o actualizados en las tablas de la base de datos. Configurarlos correctamente es crucial para garantizar tanto la precisión de los datos como los tiempos de actualización optimizados. Este artículo se centra en los métodos de replicación.

Cuando se sincronizan nuevas tablas en el Administrador de Datas Warehouse, se elige automáticamente un método de replicación para la tabla. Conocer los distintos métodos de replicación, cómo se organizan las tablas y cómo se comportan los datos de la tabla le permite elegir el mejor método de replicación para sus tablas.

## ¿Cuáles son los métodos de replicación?

`Replication` Los métodos se dividen en tres grupos: `Incremental`, `Full Table`, y `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa que [!DNL MBI] replica solo los datos nuevos o actualizados en cada intento de replicación. Como estos métodos reducen en gran medida la latencia, Adobe recomienda utilizarla siempre que sea posible.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa que [!DNL MBI] replica todo el contenido de una tabla en cada intento de replicación. Debido a la gran cantidad de datos que pueden replicarse, estos métodos pueden aumentar la latencia y los tiempos de actualización. Si una tabla contiene columnas de fecha y hora o con marca de hora, Adobe recomienda utilizar un método Incremental en su lugar.

**[!UICONTROL Paused]** indica que la replicación de la tabla se ha detenido o pausado. [!DNL MBI] no comprueba la existencia de datos nuevos o actualizados durante un ciclo de actualización; esto significa que no se replican datos de una tabla que tenga este como método de replicación.

## Métodos de replicación incremental {#incremental}

### Modificado en (lo más ideal)

El `Modified At` el método de replicación utiliza una columna datetime, que se rellena cuando se crea una fila y luego se actualiza cuando cambian los datos, para buscar los datos que se van a replicar. Este método está diseñado para trabajar con tablas que cumplan los siguientes criterios:

* contiene un `datetime` columna que se rellena inicialmente cuando se crea una fila y que se actualiza cada vez que se modifica la fila;
* el `datetime` la columna nunca es nula;
* las filas no se eliminan de la tabla

Además de estos criterios, el Adobe recomienda **indexación** el `datetime` columna utilizada para `Modified At` replicación, ya que esto ayuda a optimizar la velocidad de replicación.

Cuando se ejecuta la actualización, los datos nuevos o modificados se identifican buscando filas que tienen un valor en `datetime` columna que se produjo después de la actualización más reciente. Cuando se detectan nuevas filas, se replican en la Data Warehouse. Si existen filas en la Data Warehouse, se sobrescriben con los valores de la base de datos actual.

Por ejemplo, una tabla puede tener una columna llamada `modified\_at` que indica la última vez que se cambiaron los datos. Si la actualización más reciente se ejecutó el martes a mediodía, la actualización busca todas las filas que tengan un `modified\_at` valor bueno que el martes a mediodía. Las filas detectadas que se hayan creado o modificado desde el mediodía del martes se replicarán en la Data Warehouse.

**¿Lo sabías?**
Incluso si la base de datos no admite actualmente un `Incremental` Método de replicación, es posible que [realizar cambios en la base de datos](../../best-practices/mod-db-inc-replication.md) que permitirían el uso de `Modified At` o `Single Auto Incrementing PK`.

`Modified At` no solo es el método de replicación más ideal, sino también el más rápido. Este método no solo produce incrementos de velocidad notables con grandes conjuntos de datos, sino que tampoco requiere la configuración de una opción de nueva comprobación. Otros métodos deben iterar a través de una tabla completa para identificar los cambios, incluso si ha cambiado un pequeño subconjunto de datos. `Modified At` se repite solo en ese pequeño subconjunto.

### Clave principal de incremento automático único

`Auto Incrementing` es un comportamiento que asigna secuencialmente claves principales a las filas. Si una tabla es `Auto Incrementing` y la clave principal más alta de la tabla es 1000, el siguiente valor principal es 1001 o superior. Una tabla que no utiliza `Auto Incrementing` El comportamiento de puede asignar un valor de clave principal inferior a 1000 o saltar a un número mucho mayor, pero esto no se utiliza comúnmente.

Este método está diseñado para replicar nuevos datos de tablas que cumplan los siguientes criterios:

* `single-column primary key`; y
* `primary key` el tipo de datos es `integer`; y
* `auto incrementing` valores de clave principal.

Cuando una tabla utiliza `Single Auto Incrementing Primary Key` replicación, los nuevos datos se detectan buscando valores de clave principal superiores al valor más alto actual en la Data Warehouse. Por ejemplo, si el valor de clave principal más alto de la Data Warehouse es 500, cuando se ejecute la siguiente actualización, buscará filas con valores de clave principal 501 o superiores.

### Añadir fecha

El `Add Date` El método funciona de manera similar a `Single Auto Incrementing Primary Key` método. En lugar de utilizar un entero para la clave principal de la tabla, este método utiliza un `timestamped` columna para buscar nuevas filas.

Cuando una tabla utiliza `Add Date` replicación, los nuevos datos se detectan buscando valores con marca de tiempo buenos a la última fecha de sincronización con la Data Warehouse. Por ejemplo, si una actualización se ejecutó por última vez el 20/12/2015 09:00:00, todas las filas con una marca de tiempo buena a esta se marcarán como datos nuevos y se replicarán.

>[!NOTE]
>
>A diferencia del `Modified At` método, `Add Date` no comprueba las filas existentes para obtener información actualizada; solo espera nuevas filas.

## Métodos de replicación de tabla completa {#fulltable}

### Tabla completa

`Full table` la replicación actualiza toda la tabla cada vez que se detectan nuevas filas. Este es, con mucho, el método de replicación menos eficaz, ya que todos los datos deben volver a procesarse durante cada actualización, suponiendo que haya filas nuevas.

Las filas nuevas se detectan consultando la base de datos al principio del proceso de sincronización y contando el número de filas. Si la base de datos local contiene más filas que [!DNL MBI], la tabla se actualiza. Si los recuentos de filas son idénticos, o si [!DNL MBI] contains *más* filas que no sean de la base de datos local, la tabla se omitirá.

Esto plantea el punto importante de que **`Full Table`la replicación no es compatible cuando:**

* se eliminan más filas que las creadas en la tabla de base de datos local entre ciclos de actualización subsiguientes, o
* los valores de columna cambian, pero no se crean filas adicionales

En cualquiera de los casos anteriores, `Full Table` la replicación no detecta ningún cambio y los datos quedan obsoletos. Debido a la ineficacia de este método de replicación y a los requisitos mencionados anteriormente, `Full Table` la replicación solo se recomienda como último recurso.

### Lote de clave principal

Cuando una tabla utiliza `Primary Key Batch` (Lote FC), los nuevos datos se descubren contando filas dentro de rangos, o lotes, de valores de clave principal. Aunque normalmente piensa que esto se utiliza con números enteros, incluso los valores de texto se pueden ordenar de una manera que permita al sistema definir intervalos constantes.

Por ejemplo, supongamos que se ejecuta una actualización y realiza un recuento de filas para el rango de claves de 1 a 100. En esta actualización, el sistema busca y registra 37 filas. En la siguiente actualización, se vuelve a realizar un recuento de filas en el intervalo 1-100 y se encuentran 41 filas. Dado que existe una diferencia en el número de filas en comparación con la última actualización, el sistema inspecciona ese rango (o lote) con más detalle.

Este método está diseñado para replicar datos de tablas que cumplan los siguientes criterios:

* columna única no entera; o
* claves compuestas (varias columnas que comprenden la clave principal): tenga en cuenta que las columnas utilizadas en una clave principal compuesta nunca pueden tener valores nulos; o
* valores de clave principal de una sola columna, enteros, sin aumento automático.

Este método no es ideal, ya que es increíblemente lento debido a la cantidad de procesamiento que debe ocurrir para examinar los lotes y encontrar cambios. El Adobe recomienda no utilizar este método a menos que sea imposible realizar las modificaciones necesarias para admitir los demás métodos de replicación. Espere que los tiempos de actualización aumenten si se debe utilizar este método.

## Estableciendo métodos de replicación

Los métodos de replicación se establecen tabla por tabla. Para establecer un método de replicación para una tabla, necesita [`Admin`](../../administrator/user-management/user-management.md) para poder acceder al Administrador de Datas Warehouse.

1. Una vez en el Administrador de Datas Warehouse, seleccione la tabla en el `Synced Tables` para mostrar el esquema de la tabla.
1. El método de replicación actual aparece debajo del nombre de la tabla. Para cambiarlo, haga clic en el vínculo.
1. En la ventana emergente que aparece, haga clic en el botón de opción situado junto a `Incremental` o `Full Table` replicación para seleccionar un tipo de replicación.
1. Haga clic en el botón **[!UICONTROL Replication Method]** desplegable para seleccionar un método; por ejemplo, `Paused` o `Modified At`.

   >[!NOTE]
   >
   >**Algunos métodos incrementales requieren que establezca un`Replication Key`**. [!DNL MBI] utilizará esta clave para determinar dónde debe comenzar el siguiente ciclo de actualización.
   >
   >Por ejemplo, si desea utilizar la variable `modified at` método para su `orders` tabla, debe establecer una `date column` como clave de replicación. Pueden existir varias opciones para las claves de replicación, pero seleccione `created at`o la hora en que se creó la solicitud. Si el último ciclo de actualización se detuvo el 1/12/2015 00:10:00, el siguiente ciclo empezaría a replicar datos con una `created at` fecha buena a esta.

1. Cuando termine, haga clic en **[!UICONTROL Save]**.

Observe todo el proceso:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Ajuste

Para terminar, ha creado esta tabla que compara los distintos métodos de replicación. Es increíblemente práctico al seleccionar un método para las tablas de la Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Más rápido | Lento | No | No | No | Sí |
| `Primary Key Batch Monitoring` | Lento | Lento | Sí | Sí | Sí | Sí |
| `Modified At` | Más rápido | Más rápido | Sí | Sí | Sí | No |

{style="table-layout:auto"}

## Documentación relacionada

* [Explicación de las comprobaciones de datos](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modificación de la base de datos para admitir ](../../best-practices/mod-db-inc-replication.md)
* [Optimización de la base de datos para el análisis](../../best-practices/opt-db-analysis.md)
* [Reducción de los tiempos de actualización](../../best-practices/reduce-update-cycle-time.md)
