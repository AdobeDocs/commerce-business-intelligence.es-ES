---
title: Tipos de columnas calculadas
description: Aprenda a crear columnas para aumentar y optimizar los datos para su análisis.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Tipos de columnas calculadas

* [Mismos cálculos de tabla](#sametable)
* [Uno a muchos cálculos](#onetomany)
* [Varios a uno cálculos](#manytoone)
* [Mapa de referencia práctico](#map)
* [Columnas calculadas avanzadas](#advanced)

Dentro de [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md), puede crear columnas para aumentar y optimizar los datos para su análisis. [Esta funcionalidad](../data-warehouse-mgr/creating-calculated-columns.md) se puede acceder seleccionando cualquier tabla en el Administrador de Datas Warehouse y haciendo clic en **[!UICONTROL Create New Column]**.

En este artículo se describen los tipos de columnas que se pueden crear con el Administrador de Datas Warehouse, así como una descripción, un recorrido visual por esa columna y una [mapa de referencia](#map) de todas las entradas necesarias para crear una columna. Existen tres formas de crear columnas calculadas:

* [Misma tabla de columnas calculadas](#sametable)
* [Columnas calculadas de uno a varios](#onetomany)
* [Columnas calculadas &quot;varios a uno&quot;](#manytoone)

## Misma tabla de columnas calculadas {#sametable}

Estas columnas se crean utilizando columnas de entrada de la misma tabla.

### Edad {#age}

Una columna calculada de edad devuelve el número de segundos entre la hora actual y algún tiempo de entrada.

En el ejemplo siguiente, creamos `Seconds since customer's most recent order` en el `customers` tabla. Esto se puede aprovechar para construir listas de usuarios de clientes que no han realizado compras (a veces denominadas &quot;pérdida&quot;) dentro de `X days`.

![](../../assets/age.gif)

### Conversor de moneda

Una columna calculada del conversor de moneda convierte la moneda nativa de una columna a la nueva moneda deseada.

En el ejemplo siguiente, creamos `base\_grand\_total In AED`, convirtiendo el `base\_grand\_total` de que es moneda nativa a AED en la variable `sales\_flat\_order` tabla. Esta columna funciona bien para las tiendas con varias monedas que desean registrar en su moneda local.

Para los clientes de Commerce, la variable `base\_currency\_code` normalmente almacena monedas nativas. La variable `Spot Time` debe coincidir con la fecha utilizada en las métricas.

![](../../assets/currency_converter.png)

## Columnas calculadas de uno a varios {#onetomany}

`One-to-Many` columnas [utilizar una ruta entre dos tablas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Esta ruta siempre implica una tabla única, donde reside un atributo, y una tabla múltiple, donde ese atributo se &quot;reubica&quot; a. La ruta se puede describir como una `foreign key--primary key` relación.

### Columna unida {#joined}

Una columna unida reubica un atributo en una tabla *a* la tabla de muchas. El ejemplo clásico de uno o varios es clientes (uno) y pedidos (muchos).

En el ejemplo siguiente, la variable `Customer's group\_id` la dimensión se une a `orders` tabla.

![](../../assets/joined_column.gif)

## Columnas calculadas &quot;varios a uno&quot; {#manytoone}

Estas columnas utilizan las mismas rutas que las columnas de uno a muchos, pero dirigen los datos en la dirección opuesta. La columna se crea en un lado de la ruta, en lugar de en el otro. Debido a esta relación, el valor de la columna debe ser una agregación, es decir, una operación matemática realizada en los puntos de datos en el lado varios. Hay muchos casos de uso para esto y algunos se enumeran a continuación.

### Recuento {#count}

Este tipo de columna calculada devuelve el recuento de valores en la tabla de varios *onto* la única mesa.

En el ejemplo siguiente, la dimensión `Customer's lifetime number of canceled orders` se crea en la variable `customers` (con un filtro para `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Sum {#sum}

Una columna calculada de suma es la suma de valores de la variable `many` en la única mesa.

Esto se puede utilizar para crear dimensiones de nivel de cliente como `Customer's lifetime revenue`.

### Min o Max {#minmax}

Una columna calculada como mínimo o máximo devuelve el registro más pequeño o el más grande que existe en el lado múltiple.

Esto se puede utilizar para crear dimensiones de nivel de cliente como `Customer's first order date`.

### Existe {#exists}

Una columna calculada existe es una prueba binaria que determina la presencia de un registro en el lado múltiple. En otras palabras, la nueva columna devolverá un valor `1` si la ruta conecta al menos una fila en cada tabla, y `0` si no se puede realizar ninguna conexión.

Este tipo de dimensión puede determinar, por ejemplo, si un cliente ha comprado un producto en particular alguna vez. Uso de una unión entre `customers` tabla y `orders` tabla, filtro para un producto específico, dimensión `Customer has purchased Product X?` se puede crear.

## Mapa de referencia práctico {#map}

Si tiene problemas para recordar cuáles son todas las entradas al crear una columna calculada, intente mantener este mapa de referencia a mano cuando esté creando:

![](../../assets/merged_reference_map.png)

## Columnas calculadas avanzadas {#advanced}

En su búsqueda de analizar y responder preguntas sobre su negocio, puede encontrarse con una situación en la que no puede crear la columna exacta que desee. En estos casos, ¡te hemos cubierto!

Para garantizar un giro rápido, le recomendamos que compruebe el [Tipos de columnas calculadas avanzadas](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) guía para ver qué tipo de columnas puede crear nuestro equipo de asistencia. En ese artículo, también cubrimos la información que necesitaremos de usted para crear la columna - por favor, inclúyala con su solicitud.

## Documentación relacionada

* [Creación de columnas calculadas](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Creación/eliminación de rutas para columnas calculadas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Explicación y evaluación de las relaciones de tabla](../../data-analyst/data-warehouse-mgr/table-relationships.md)
