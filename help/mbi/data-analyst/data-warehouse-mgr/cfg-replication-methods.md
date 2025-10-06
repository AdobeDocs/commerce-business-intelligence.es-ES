---
title: Configuración de métodos de replicación
description: Conozca cómo se organizan las tablas y cómo se comportan los datos de la tabla para poder elegir el mejor método de replicación para sus tablas.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# Configuración de métodos de replicación

Se utilizan `Replication` métodos y [comprobaciones nuevas](../data-warehouse-mgr/cfg-data-rechecks.md) para identificar datos nuevos o actualizados en las tablas de la base de datos. Configurarlos correctamente es crucial para garantizar tanto la precisión de los datos como los tiempos de actualización optimizados. Este tema se centra en los métodos de replicación.

Cuando se sincronizan nuevas tablas en [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), se elige automáticamente un método de replicación para la tabla. Conocer los distintos métodos de replicación, cómo se organizan las tablas y cómo se comportan los datos de la tabla le permite elegir el mejor método de replicación para sus tablas.

## ¿Cuáles son los métodos de replicación?

Los métodos de `Replication` se dividen en tres grupos: `Incremental`, `Full Table` y `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa que [!DNL Commerce Intelligence] replica solamente datos nuevos o actualizados en cada intento de replicación. Como estos métodos reducen en gran medida la latencia, Adobe recomienda utilizarla siempre que sea posible.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa que [!DNL Commerce Intelligence] replica todo el contenido de una tabla en cada intento de replicación. Debido a la gran cantidad de datos que pueden replicarse, estos métodos pueden aumentar la latencia y los tiempos de actualización. Si una tabla contiene columnas con marca de hora o fecha y hora, Adobe recomienda utilizar un método Incremental en su lugar.

**[!UICONTROL Paused]** indica que la replicación de la tabla se ha detenido o pausado. [!DNL Commerce Intelligence] no comprueba si hay datos nuevos o actualizados durante un ciclo de actualización; esto significa que no se replican datos de una tabla que tenga este método de replicación.

## Métodos de replicación incremental {#incremental}

### Modificado en (lo más ideal)

El método de replicación `Modified At` usa una columna datetime (que se rellena cuando se crea una fila y se actualiza cuando cambian los datos) para buscar los datos que se van a replicar. Este método está diseñado para trabajar con tablas que cumplan los siguientes criterios:

* contiene una columna `datetime` que se rellena inicialmente cuando se crea una fila y se actualiza cada vez que se modifica la fila;
* la columna `datetime` nunca es nula;
* las filas no se eliminan de la tabla

Además de esos criterios, Adobe recomienda **indexar** la columna `datetime` utilizada para la replicación `Modified At`, ya que esto ayuda a optimizar la velocidad de replicación.

Cuando se ejecuta la actualización, los datos nuevos o modificados se identifican buscando filas que tengan un valor en la columna `datetime` que se produjo después de la actualización más reciente. Cuando se detectan nuevas filas, se replican en el Data Warehouse. Si existen filas en [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), se sobrescriben con los valores actuales de la base de datos.

Por ejemplo, una tabla puede tener una columna llamada `modified\_at` que indica la última vez que se cambiaron los datos. Si la actualización más reciente se ejecutó el martes a mediodía, la actualización buscará todas las filas que tengan un valor de `modified\_at` mayor que el martes a mediodía. Las filas detectadas que se hayan creado o modificado desde el mediodía del martes se replican en Data Warehouse.

**¿Lo sabías?**
Aunque su base de datos no admita actualmente un método de replicación de `Incremental`, es posible que pueda [realizar cambios en su base de datos](../../best-practices/mod-db-inc-replication.md) que permitan el uso de `Modified At` o `Single Auto Incrementing PK`.

`Modified At` no solo es el método de replicación más ideal, sino también el más rápido. Este método no solo produce incrementos de velocidad notables con grandes conjuntos de datos, sino que tampoco requiere la configuración de una opción de nueva comprobación. Otros métodos deben iterar a través de una tabla completa para identificar los cambios, incluso si ha cambiado un pequeño subconjunto de datos. `Modified At` se repite solamente en ese pequeño subconjunto.

### Clave principal de incremento automático único

`Auto Incrementing` es un comportamiento que asigna secuencialmente claves principales a las filas. Si una tabla es `Auto Incrementing` y la clave principal más alta de la tabla es 1000, el siguiente valor principal es 1001 o superior. Una tabla que no usa el comportamiento `Auto Incrementing` puede asignar un valor de clave principal inferior a 1000 o saltar a un número mucho mayor, pero no se usa a menudo.

Este método está diseñado para replicar nuevos datos de tablas que cumplan los siguientes criterios:

* `single-column primary key`; y
* `primary key` el tipo de datos es `integer`; y
* `auto incrementing` valores de clave principal.

Cuando una tabla utiliza la replicación `Single Auto Incrementing Primary Key`, se detectan nuevos datos buscando valores de clave principal superiores al valor más alto actual en Data Warehouse. Por ejemplo, si el valor de clave principal más alto de Data Warehouse es 500, cuando se ejecute la siguiente actualización, buscará filas con valores de clave principal 501 o superiores.

### Añadir fecha

El método `Add Date` funciona de manera similar al método `Single Auto Incrementing Primary Key`. En lugar de utilizar un entero para la clave principal de la tabla, este método utiliza una columna `timestamped` para buscar nuevas filas.

Cuando una tabla utiliza la replicación `Add Date`, se detectan nuevos datos al buscar valores con marca de tiempo mayores que la última fecha sincronizada con su Data Warehouse. Por ejemplo, si una actualización se ejecutó por última vez el 20/12/2015 09:00:00, todas las filas con una marca de tiempo mayor que esta se marcarán como datos nuevos y se replicarán.

>[!NOTE]
>
>A diferencia del método `Modified At`, `Add Date` no comprueba las filas existentes para obtener información actualizada, solo espera con interés las filas nuevas.

## Métodos de replicación de tabla completa {#fulltable}

### Tabla completa

La replicación `Full table` actualiza toda la tabla cada vez que se detectan nuevas filas. Este es, con mucho, el método de replicación menos eficaz, ya que todos los datos deben volver a procesarse durante cada actualización, suponiendo que haya filas nuevas.

Las filas nuevas se detectan consultando la base de datos al principio del proceso de sincronización y contando el número de filas. Si la base de datos local contiene más filas que [!DNL Commerce Intelligence], la tabla se actualiza. Si los recuentos de filas son idénticos o si [!DNL Commerce Intelligence] contiene *más* filas que la base de datos local, se omitirá la tabla.

Esto plantea el punto importante de que la replicación de **`Full Table`es incompatible cuando:**

* se eliminan más filas que las creadas en la tabla de base de datos local entre ciclos de actualización subsiguientes, o
* los valores de columna cambian, pero no se crean filas adicionales

En cualquiera de las situaciones anteriores, la replicación de `Full Table` no detecta ningún cambio y los datos quedan obsoletos. Debido a la ineficacia de este método de replicación y a los requisitos mencionados anteriormente, la replicación `Full Table` solo se recomienda como último recurso.

### Lote de clave principal

Cuando una tabla utiliza `Primary Key Batch` (lote PK), se detectan nuevos datos contando las filas dentro de rangos, o lotes, de valores de clave principal. Aunque normalmente piensa que esto se utiliza con números enteros, incluso los valores de texto se pueden ordenar de una manera que permita al sistema definir intervalos constantes.

Por ejemplo, supongamos que se ejecuta una actualización y realiza un recuento de filas para el rango de claves de 1 a 100. En esta actualización, el sistema busca y registra 37 filas. En la siguiente actualización, se vuelve a realizar un recuento de filas en el intervalo 1-100 y se encuentran 41 filas. Dado que existe una diferencia en el número de filas en comparación con la última actualización, el sistema inspecciona ese rango (o lote) con más detalle.

Este método está diseñado para replicar datos de tablas que cumplan los siguientes criterios:

* columna única no entera; o
* claves compuestas (varias columnas que comprenden la clave principal): tenga en cuenta que las columnas utilizadas en una clave principal compuesta nunca pueden tener valores nulos; o
* valores de clave principal de una sola columna, enteros, sin aumento automático.

Este método no es ideal, ya que es increíblemente lento debido a la cantidad de procesamiento que debe ocurrir para examinar los lotes y encontrar cambios. Adobe recomienda no utilizar este método a menos que sea imposible realizar las modificaciones necesarias para admitir los demás métodos de replicación. Espere que los tiempos de actualización aumenten si se debe utilizar este método.

## Estableciendo métodos de replicación

Los métodos de replicación se establecen tabla por tabla. Para establecer un método de replicación para una tabla, necesita [`Admin`](../../administrator/user-management/user-management.md) permisos para poder acceder al Administrador de Data Warehouse.

1. Una vez en el Administrador de Data Warehouse, seleccione la tabla de la lista `Synced Tables` para mostrar el esquema de la tabla.
1. El método de replicación actual aparece debajo del nombre de la tabla. Para cambiarlo, haga clic en el vínculo.
1. En la ventana emergente que se muestra, haga clic en el botón de opción situado junto a `Incremental` o `Full Table` replicación para seleccionar un tipo de replicación.
1. A continuación, haga clic en el menú desplegable **[!UICONTROL Replication Method]** para seleccionar un método. Por ejemplo, `Paused` o `Modified At`.

   >[!NOTE]
   >
   >**Algunos métodos incrementales requieren que establezca un`Replication Key`**. [!DNL Commerce Intelligence] usará esta clave para determinar dónde debe comenzar el siguiente ciclo de actualización.
   >
   >Por ejemplo, si desea utilizar el método `modified at` para la tabla `orders`, debe establecer `date column` como clave de replicación. Pueden existir varias opciones para las claves de replicación, pero usted selecciona `created at` o la hora en que se creó el pedido. Si el último ciclo de actualización se detuvo el 1/12/2015 00:10:00, el siguiente ciclo comenzará a replicar datos con una fecha `created at` mayor que esta.

1. Cuando termine, haga clic en **[!UICONTROL Save]**.

Observe todo el proceso:

![Demostración animada de la configuración de métodos de replicación para tablas de base de datos](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Ajuste

Para terminar, ha creado esta tabla que compara los distintos métodos de replicación. Es increíblemente práctico al seleccionar un método para las tablas de su Data Warehouse.

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
