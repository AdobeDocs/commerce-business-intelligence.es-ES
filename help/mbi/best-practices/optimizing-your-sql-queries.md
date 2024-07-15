---
title: Optimización de las consultas SQL
description: Aprenda a optimizar las consultas SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Optimización de las consultas SQL

[!DNL SQL Report Builder] le permite consultar e iterar en esas consultas en un momento dado. Esto resulta útil cuando necesita modificar una consulta sin tener que esperar a que finalice un ciclo de actualización antes de darse cuenta de que una columna o informe que ha creado necesita actualizarse.

Antes de ejecutar una consulta, [[!DNL Commerce Intelligence] calcula su costo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html). El coste tiene en cuenta el tiempo y el número de recursos necesarios para ejecutar una consulta. Si se considera que ese costo es demasiado alto o si el número de filas devueltas supera los límites de [!DNL Commerce Intelligence], la consulta falla. Para consultar la [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md), que garantiza que escribirás las consultas más optimizadas posibles, Adobe recomienda lo siguiente.

## Uso de SELECT o Selección de todas las columnas

La selección de todas las columnas no constituye una consulta oportuna y fácil de ejecutar. Las consultas que utilizan `SELECT *` pueden tardar bastante tiempo en ejecutarse, especialmente si la tabla tiene muchas columnas.

Por este motivo, Adobe recomienda evitar el uso de `SELECT *` siempre que sea posible e incluir solo las columnas que necesite:

| **En lugar de esto...** | **Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## Uso de uniones externas completas

Las uniones externas seleccionan la totalidad de ambas tablas que se están uniendo, lo que aumenta el coste de cálculo de la consulta. Esto significa que la consulta tarda más en ejecutarse y es más probable que falle, ya que puede tardar más tiempo que el límite de ejecución en devolver los resultados.

En lugar de utilizar este tipo de combinación, considere la posibilidad de utilizar una combinación interna o izquierda. Las uniones internas devuelven resultados únicamente cuando hay una coincidencia en columnas entre las tablas (por ejemplo, `order_id` existe tanto en una tabla típica de `customers` como en una tabla de `orders`). Las combinaciones de izquierda devuelven todos los resultados de la tabla izquierda (primera) junto con los resultados coincidentes de la tabla derecha (segunda).

Observe cómo puede reescribir una consulta FULL OUTER JOIN:

| **En lugar de esto...** | **Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

Estas consultas son idénticas en todos los sentidos, excepto en el tipo de JOIN que utilizan.

## Uso de varias uniones

Aunque puede incluir varias combinaciones en la consulta, recuerde que puede aumentar el costo de la consulta. Para evitar alcanzar el umbral de coste, Adobe recomienda evitar varias uniones siempre que sea posible.

## Uso de filtros

Utilice filtros siempre que sea posible. Las cláusulas `WHERE` y `HAVING` filtran los resultados y le proporcionan únicamente los datos que realmente desea.

## Uso de filtros en cláusulas JOIN

Si utiliza un filtro al realizar una combinación, asegúrese de aplicarlo a ambas tablas de la combinación. Incluso si es redundante, esto reduce el coste de cálculo de la consulta y el tiempo de ejecución.

| **En lugar de esto...** | **Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## Uso de operadores

Al escribir consultas, considere la posibilidad de utilizar los operadores &quot;menos costosos&quot; posibles. Cada consulta tiene un coste de cálculo, que viene determinado por las funciones, operadores y filtros que conforman la consulta. Algunos operadores requieren menos esfuerzo de cálculo, lo que los hace menos costosos que otros operadores.

Los operadores de comparación (>, &lt;, =, etc.) son los menos costosos, seguidos de [LIKE. Operadores SIMILAR A y POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html), que son los operadores más caros.

## Uso de EXISTS frente a IN

El uso de `EXISTS` frente a `IN` depende del tipo de resultados que esté intentando devolver. Si sólo le interesa un valor único, utilice la cláusula `EXISTS` en lugar de `IN`. `IN` se usa con listas de valores separados por comas, lo que aumenta el costo de cálculo de la consulta.

Cuando se ejecutan `IN` consultas, el sistema debe procesar primero la subconsulta (la instrucción `IN`) y después toda la consulta basada en la relación especificada en la instrucción `IN`. `EXISTS` es mucho más eficaz porque la consulta no tiene que ejecutarse varias veces: se devuelve un valor true/false al comprobar la relación especificada en la consulta.

En pocas palabras: el sistema no tiene que procesar tanto al usar `EXISTS`.

| **En lugar de esto...** | **Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## Uso de ORDER BY

`ORDER BY` es una función costosa en SQL y puede aumentar significativamente el costo de una consulta. Si recibe un mensaje de error que indica que el costo EXPLICAR de la consulta es demasiado alto, intente eliminar `ORDER BY` de la consulta a menos que sea necesario.

Esto no quiere decir que `ORDER BY` no se pueda usar, simplemente que solo se debe usar cuando sea necesario.

## Uso de GROUP BY y ORDER BY

Puede haber algunas situaciones en las que este enfoque no se ajuste a lo que está intentando hacer. La regla general es que si está utilizando `GROUP BY` y `ORDER BY`, debe colocar las columnas en ambas cláusulas en el mismo orden. Por ejemplo:

| **En lugar de esto...** | **Pruebe esto!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## Ajuste

La mejor manera de aprender a escribir SQL -y hacerlo de manera eficiente- es a través de prueba y error. Para encontrar lo que funciona mejor para usted, intente volver a crear algunos informes utilizando solo el editor SQL.
