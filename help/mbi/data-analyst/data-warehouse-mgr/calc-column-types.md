---
title: Tipos de columnas calculadas
description: Aprenda a crear columnas para aumentar y optimizar los datos para el análisis.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Tipos de columnas calculadas

* [Mismos cálculos de tabla](#sametable)
* [Uno a varios cálculos](#onetomany)
* [Cálculos de varios a uno](#manytoone)
* [Mapa de referencia útil](#map)
* [Columnas calculadas avanzadas](#advanced)

En el [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md), puede crear columnas para aumentar y optimizar los datos para su análisis. [Se puede acceder a esta funcionalidad](../data-warehouse-mgr/creating-calculated-columns.md) seleccionando cualquier tabla en el Administrador de Datas Warehouse y haciendo clic en **[!UICONTROL Create New Column]**.

En este tema se describen los tipos de columnas que se pueden crear con el Administrador de Datas Warehouse. También cubre la descripción, un recorrido visual de esa columna y un [mapa de referencia](#map) de todas las entradas necesarias para crear una columna. Existen tres formas de crear columnas calculadas:

1. [Mismas columnas calculadas de tabla](#sametable)
1. [Columnas calculadas de uno a varios](#onetomany)
1. [Columnas calculadas varios a uno](#manytoone)

## Mismas columnas calculadas de tabla {#sametable}

Estas columnas se crean utilizando columnas de entrada de la misma tabla.

### Edad {#age}

Una columna calculada de edad devuelve el número de segundos entre la hora actual y algún tiempo de entrada.

El ejemplo siguiente crea `Seconds since customer's most recent order` en la tabla `customers`. Esto se puede usar para construir listas de usuarios de clientes que no han hecho compras (a veces denominadas pérdidas) en `X days`.

![](../../assets/age.gif)

### Conversor de moneda

Una columna calculada de convertidor de moneda convierte la moneda nativa de una columna en una nueva moneda deseada.

El ejemplo siguiente crea `base\_grand\_total In AED`, convirtiendo el `base\_grand\_total` de su moneda original a AED en la tabla `sales\_flat\_order`. Esta columna funciona bien en tiendas con varias monedas que desean generar informes en su moneda local.

Para los clientes de Commerce, el campo `base\_currency\_code` generalmente almacena monedas nativas. El campo `Spot Time` debe coincidir con la fecha utilizada en las métricas.

![](../../assets/currency_converter.png)

## Columnas calculadas de uno a varios {#onetomany}

`One-to-Many` columnas [utilizan una ruta entre dos tablas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Esta ruta siempre implica una tabla única, donde reside un atributo, y una tabla varios, donde ese atributo se &quot;reubica&quot; hasta. La ruta de acceso puede describirse como una relación `foreign key--primary key`.

### Columna combinada {#joined}

Una columna unida reubica un atributo de la tabla *a* la tabla varios. El ejemplo clásico de uno/varios es clientes (uno) y pedidos (varios).

En el ejemplo siguiente, la dimensión `Customer's group\_id` se une en la tabla `orders`.

![](../../assets/joined_column.gif)

## Columnas calculadas varios a uno {#manytoone}

Estas columnas utilizan las mismas rutas que las columnas uno a varios, pero dirigen los datos en la dirección opuesta. La columna se crea en el lado uno de la ruta, en contraposición al lado varios. Debido a esta relación, el valor de la columna debe ser una agregación, es decir, una operación matemática realizada en los puntos de datos del lado varios. Existen muchos casos de uso para esto y algunos se enumeran a continuación.

### Recuento {#count}

Este tipo de columna calculada devuelve el recuento de valores de la tabla de varios *en* la tabla de uno.

En el ejemplo siguiente, la dimensión `Customer's lifetime number of canceled orders` se crea en la tabla `customers` (con un filtro para `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Sum {#sum}

Una columna calculada de suma es la suma de los valores de la tabla `many` en la tabla uno.

Se puede usar para crear dimensiones de nivel de cliente como `Customer's lifetime revenue`.

### Mínimo o máximo {#minmax}

Una columna calculada como mínimo o máximo devuelve el registro más pequeño o más grande que existe en el lado varios.

Se puede usar para crear dimensiones de nivel de cliente como `Customer's first order date`.

### Existe {#exists}

Una columna calculada es una prueba binaria que determina la presencia de un registro en el lado varios. En otras palabras, la nueva columna devuelve un `1` si la ruta de acceso conecta al menos una fila en cada tabla y `0` si no se puede establecer ninguna conexión.

Este tipo de dimensión podría determinar, por ejemplo, si un cliente ha comprado alguna vez un producto en particular. Mediante una combinación entre una tabla `customers` y una tabla `orders`, un filtro para un producto específico, se puede crear una dimensión `Customer has purchased Product X?`.

## Mapa de referencia útil {#map}

Si tiene problemas para recordar cuáles son todas las entradas al crear una columna calculada, tenga a mano este mapa de referencia al crear:

![](../../assets/merged_reference_map.png)

## Columnas calculadas avanzadas {#advanced}

En su búsqueda para analizar y responder preguntas sobre su negocio, puede encontrarse con una situación en la que no puede crear la columna exacta que desea.

Para garantizar un giro rápido, Adobe recomienda revisar la guía [Tipos de columnas calculadas avanzadas](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) para ver qué tipo de columnas puede generar el equipo de soporte de Adobe. Ese tema también cubre la información que necesita de usted para crear la columna: inclúyala en su solicitud.

## Documentación relacionada

* [Creación de columnas calculadas](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Creación/eliminación de rutas para columnas calculadas](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Explicación y evaluación de las relaciones de tabla](../../data-analyst/data-warehouse-mgr/table-relationships.md)
