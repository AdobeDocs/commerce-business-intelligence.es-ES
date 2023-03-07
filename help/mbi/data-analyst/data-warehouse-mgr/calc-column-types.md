---
title: Tipos de columnas calculadas
description: Aprenda a crear columnas para aumentar y optimizar los datos para el análisis.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Tipos de columnas calculadas

* [Mismos cálculos de tabla](#sametable)
* [Uno a varios cálculos](#onetomany)
* [Cálculos de varios a uno](#manytoone)
* [Mapa de referencia útil](#map)
* [Columnas calculadas avanzadas](#advanced)

Dentro de [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md), puede crear columnas para aumentar y optimizar los datos para el análisis. [Esta funcionalidad](../data-warehouse-mgr/creating-calculated-columns.md) se puede acceder a ella seleccionando cualquier tabla en el Administrador de Datas Warehouse y haciendo clic en **[!UICONTROL Create New Column]**.

En este artículo se describen los tipos de columnas que se pueden crear con el Administrador de Datas Warehouse. También se describe la descripción, se describe visualmente esa columna y se muestra un [mapa de referencia](#map) de todas las entradas necesarias para crear una columna. Existen tres formas de crear columnas calculadas:

* [Mismas columnas calculadas de tabla](#sametable)
* [Columnas calculadas de uno a varios](#onetomany)
* [Columnas calculadas varios a uno](#manytoone)

## Mismas columnas calculadas de tabla {#sametable}

Estas columnas se crean utilizando columnas de entrada de la misma tabla.

### Edad {#age}

Una columna calculada de edad devuelve el número de segundos entre la hora actual y algún tiempo de entrada.

El ejemplo siguiente crea `Seconds since customer's most recent order` en el `customers` tabla. Esto se puede utilizar para construir listas de usuarios de clientes que no han realizado compras (a veces denominadas &quot;pérdidas&quot;) dentro de `X days`.

![](../../assets/age.gif)

### Conversor de moneda

Una columna calculada de convertidor de moneda convierte la moneda nativa de una columna en una nueva moneda deseada.

El ejemplo siguiente crea `base\_grand\_total In AED`, convirtiendo el `base\_grand\_total` de es la moneda nativa a AED en el `sales\_flat\_order` tabla. Esta columna funciona bien en tiendas con varias monedas que desean generar informes en su moneda local.

Para los clientes de Commerce, la variable `base\_currency\_code` Este campo generalmente almacena monedas nativas. El `Spot Time` El campo debe coincidir con la fecha utilizada en las métricas.

![](../../assets/currency_converter.png)

## Columnas calculadas de uno a varios {#onetomany}

`One-to-Many` columnas [utilizar una ruta entre dos tablas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Esta ruta siempre implica una tabla única, donde reside un atributo, y una tabla varios, donde ese atributo se &quot;reubica&quot; hasta. La ruta se puede describir como una `foreign key--primary key` relación.

### Columna combinada {#joined}

Una columna combinada reubica un atributo en la tabla uno *hasta* la tabla de varios. El ejemplo clásico de uno/varios es clientes (uno) y pedidos (varios).

En el ejemplo siguiente, la variable `Customer's group\_id` la dimensión se une hacia abajo en el `orders` tabla.

![](../../assets/joined_column.gif)

## Columnas calculadas varios a uno {#manytoone}

Estas columnas utilizan las mismas rutas que las columnas uno a varios, pero dirigen los datos en la dirección opuesta. La columna se crea en el lado uno de la ruta, en contraposición al lado varios. Debido a esta relación, el valor de la columna debe ser una agregación, es decir, una operación matemática realizada en los puntos de datos del lado varios. Existen muchos casos de uso para esto y algunos se enumeran a continuación.

### Recuento {#count}

Este tipo de columna calculada devuelve el recuento de valores de la tabla varios *en* la de una tabla.

En el ejemplo siguiente, la dimensión `Customer's lifetime number of canceled orders` se crea en la `customers` tabla (con un filtro para `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Sum {#sum}

Una columna calculada de suma es la suma de los valores del `many` sobre la mesa de uno.

Esto se puede utilizar para crear dimensiones de nivel de cliente como `Customer's lifetime revenue`.

### Mínimo o máximo {#minmax}

Una columna calculada como mínimo o máximo devuelve el registro más pequeño o más grande que existe en el lado varios.

Esto se puede utilizar para crear dimensiones de nivel de cliente como `Customer's first order date`.

### Existe {#exists}

Una columna calculada existe es una prueba binaria que determina la presencia de un registro en el lado varios. En otras palabras, la nueva columna devuelve un `1` si la ruta conecta al menos una fila en cada tabla, y `0` si no se puede establecer ninguna conexión.

Este tipo de dimensión podría determinar, por ejemplo, si un cliente ha comprado alguna vez un producto en particular. Uso de una unión entre un `customers` tabla y `orders` una tabla, un filtro para un producto específico, una dimensión `Customer has purchased Product X?` se puede crear.

## Mapa de referencia útil {#map}

Si tiene algún problema para recordar cuáles son todas las entradas al crear una columna calculada, intente mantener este mapa de referencia a mano cuando esté construyendo:

![](../../assets/merged_reference_map.png)

## Columnas calculadas avanzadas {#advanced}

En su búsqueda para analizar y responder preguntas sobre su negocio, puede encontrarse con una situación en la que no puede crear la columna exacta que desea.

Para garantizar un giro rápido, el Adobe recomienda consultar el [Tipos de columnas calculadas avanzadas](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) para ver qué tipo de columnas puede crear el equipo de asistencia de Adobe. Ese artículo también cubre la información que necesita de usted para crear la columna: inclúyala en su solicitud.

## Documentación relacionada

* [Creación de columnas calculadas](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Creación/eliminación de rutas para columnas calculadas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Explicación y evaluación de las relaciones de tabla](../../data-analyst/data-warehouse-mgr/table-relationships.md)
