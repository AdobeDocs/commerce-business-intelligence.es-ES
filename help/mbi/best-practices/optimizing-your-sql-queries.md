---
title: Optimización de las consultas SQL
description: Aprenda a optimizar las consultas SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Optimizar las consultas SQL

El Report Builder SQL permite realizar consultas e iterar en esas consultas en un momento determinado. Esto resulta útil cuando necesita modificar una consulta sin tener que esperar a que finalice un ciclo de actualización antes de darse cuenta de que una columna o informe que ha creado necesita actualizarse.

Antes de ejecutar una consulta, [[!DNL MBI] calcula su coste](https://support.magento.com/hc/en-us/articles/360016730391). El coste tiene en cuenta el tiempo y el número de recursos necesarios para ejecutar una consulta. Si ese coste se considera demasiado alto o si el número de filas devueltas supera nuestros límites, la consulta no se ejecutará. Hemos creado una lista de recomendaciones para consultar el almacén de datos, que le asegurarán que está escribiendo las consultas más optimizadas posibles.

## Uso de SELECT o de la selección de todas las columnas

La selección de todas las columnas no proporciona una consulta oportuna y fácil de ejecutar. Consultas que utilizan `SELECT *` puede tardar bastante tiempo en ejecutarse, especialmente si la tabla tiene un gran número de columnas.

Por este motivo, le recomendamos que evite utilizar `SELECT *` siempre que sea posible e incluya únicamente las columnas que necesite:

| **En lugar de esto...** | **¡Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style=&quot;table-layout:auto&quot;}

## Uso de uniones exteriores completas

Las uniones externas seleccionan la totalidad de ambas tablas que se unen, lo que aumentará el coste de cálculo de la consulta. Esto significa que la consulta tardará más en ejecutarse y que es más probable que falle, ya que puede tardar más de lo previsto en la ejecución en devolver los resultados.

En lugar de utilizar este tipo de unión, considere la posibilidad de utilizar una unión interna o izquierda. Las uniones interiores devuelven solo resultados donde tAquí hay una coincidencia en columnas entre tablas (por ejemplo, `order_id` existe en ambas `customers` y `orders` tabla); las uniones izquierdas devolverán todos los resultados de la tabla izquierda (primero) junto con los resultados coincidentes en la tabla derecha (segundo).

Eche un vistazo a cómo podemos reescribir una consulta FULL OUTER JOIN:

| **En lugar de esto...** | **¡Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style=&quot;table-layout:auto&quot;}

Como puede ver, estas consultas son idénticas de todas las formas excepto por el tipo de JOIN que utilizan.

## Uso de varias uniones

Aunque puede incluir varias uniones en la consulta, recuerde que puede aumentar el coste de la consulta. Para evitar alcanzar el umbral de coste, se recomienda evitar múltiples uniones siempre que sea posible.

## Uso de filtros

Utilice filtros siempre que sea posible. `WHERE` y `HAVING` filtrarán los resultados y le darán únicamente los datos que realmente desea.

## Uso de filtros en cláusulas JOIN

Si utiliza un filtro al realizar una unión, asegúrese de aplicarlo a ambas tablas de la unión. Incluso si es redundante, esto reducirá el coste de cálculo de la consulta y acelerará el tiempo de ejecución.

| **En lugar de esto...** | **¡Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style=&quot;table-layout:auto&quot;}

## Uso de operadores

Al escribir consultas, considere la posibilidad de utilizar los operadores &quot;menos costosos&quot;. Cada consulta tiene un coste de cálculo, que viene determinado por las funciones, operadores y filtros que conforman la consulta. Algunos operadores requieren menos esfuerzo de cálculo, lo que los hace menos costosos que otros operadores.

Los operadores de comparación (>, &lt;, =, etc.) son los menos costosos, seguidos de [COMO. Operadores SIMILARES A y POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html) que son los operadores más caros.

## Uso de EXISTENTES frente a IN

Uso `EXISTS` versus `IN` depende del tipo de resultados que intente devolver. Si solo le interesa un valor único, utilice el `EXISTS` en lugar de `IN`. `IN` se utiliza junto con listas de valores separados por coma, lo que aumenta el coste de cálculo de la consulta.

When `IN` se ejecutan las consultas, el sistema debe procesar primero la subconsulta (la variable `IN` ), luego toda la consulta en función de la relación especificada en la `IN` instrucción. `EXISTS` es mucho más eficiente porque la consulta no tiene que ejecutarse varias veces: se devuelve un valor true/false al comprobar la relación especificada en la consulta.

Dicho simplemente: el sistema no tiene que procesar tanto al utilizar `EXISTS`.

| **En lugar de esto...** | **¡Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style=&quot;table-layout:auto&quot;}

## Uso de ORDER POR

`ORDER BY` es una función costosa en SQL y puede aumentar significativamente el coste de una consulta. Si recibe un mensaje de error que indica que el coste EXPLAIN de la consulta es demasiado elevado, intente eliminar cualquier `ORDER BY`s de la consulta a menos que sea absolutamente necesario.

Esto no significa que `ORDER BY` no se puede usar, solo que debe usarse cuando sea necesario.

## Uso de GRUPO POR y ORDEN POR

Aunque puede haber algunas situaciones en las que este enfoque no se ajusta a lo que está intentando hacer, la regla general es que si utiliza un `GROUP BY` y `ORDER BY`, debe colocar las columnas en ambas cláusulas en el mismo orden. Por ejemplo:

| **En lugar de esto...** | **¡Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style=&quot;table-layout:auto&quot;}

## Ajuste

La mejor manera de aprender a escribir SQL -y hacerlo de manera eficiente- es a través de pruebas y errores. Para encontrar lo que mejor le conviene, intente recrear algunos informes usando solo el editor SQL.
