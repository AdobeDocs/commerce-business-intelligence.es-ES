---
title: Comprender y evaluar las relaciones entre tablas
description: Aprenda a comprender cuántas ocurrencias posibles de una tabla podrían pertenecer a una entidad en otra.
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Comprender y evaluar las relaciones entre tablas

Al evaluar la relación entre dos tablas determinadas, debe comprender cuántas ocurrencias posibles de una tabla podrían pertenecer a una entidad en otra y viceversa. Por ejemplo, use una tabla `users` y una tabla `orders`. En este caso, desea saber cuántos **pedidos** ha realizado un **usuario** determinado y a cuántos posibles **usuarios** podría pertenecer un **pedido**.

Entender las relaciones es vital para mantener la integridad de los datos, ya que afecta la precisión de las [columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) y [dimensiones](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Para obtener más información, vea [tipos de relación](#types) y [cómo evaluar las tablas en la Data Warehouse.](#eval)

## Tipos de relaciones {#types}

Existen tres tipos de relaciones que pueden existir entre dos tablas:

1. [&quot;uno a uno&quot;](#onetoone)
1. [&quot;uno a varios&quot;](#onetomany)
1. [&quot;varios a varios&quot;](#manytomany)

### `One-to-One` {#onetoone}

En una relación `one-to-one`, un registro de la tabla `B` pertenece a un único registro de la tabla `A`. Y un registro de la tabla `A` pertenece a un único registro de la tabla `B`.

Por ejemplo, en la relación entre las personas y los números de licencia de conducir, una persona solo puede tener un número de licencia de conducir, y un número de licencia de conducir pertenece a una sola persona.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

En una relación `one-to-many`, un registro de la tabla `A` puede pertenecer potencialmente a varios registros de la tabla `B`. Piense en la relación entre `orders` y `items`: un pedido puede contener muchos elementos, pero un elemento pertenece a un único pedido. En este caso, la tabla `orders` es el lado uno y la tabla `items` es el lado varios.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

En una relación `many-to-many`, un registro de la tabla `B` puede pertenecer potencialmente a varios registros de la tabla `A`. Y viceversa, un registro de la tabla `A` puede pertenecer potencialmente a varios registros de la tabla `B`.

Piense en la relación entre **productos** y **categorías**: un producto puede pertenecer a muchas categorías y una categoría puede contener muchos productos.

![](../../assets/many-to-many.png)

## Evaluación de las tablas {#eval}

Dados los tipos de relaciones que existen entre las tablas, puede aprender a evaluar las tablas en la Data Warehouse. A medida que estas relaciones determinan cómo se definen las columnas calculadas de varias tablas, es importante que entienda cómo identificar las relaciones de tabla y a qué lado - `one` o `many` - pertenece la tabla.

Puede utilizar dos métodos para evaluar las relaciones de un par determinado de tablas dentro de la Data Warehouse. El primer método emplea un [marco conceptual](#concept) que tiene en cuenta cómo interactúan las entidades de la tabla entre sí. El segundo método usa el esquema [table](#schema).

### Uso del marco conceptual {#concept}

Este método utiliza un marco conceptual para describir cómo las entidades de las dos tablas pueden interactuar entre sí. Es importante entender que este marco evalúa lo que es posible, dada la relación.

Por ejemplo, cuando piense en usuarios y pedidos, tenga en cuenta todo lo que es posible en la relación. Un usuario registrado no puede realizar ningún pedido, solo uno o varios pedidos durante su vida útil. Si ha iniciado su negocio y no se han realizado pedidos, es posible que un usuario determinado pueda realizar muchos pedidos durante su vida útil. Las mesas están construidas para acomodar esto.

Para utilizar este método:

1. Identifique la entidad que se describe en cada tabla. **Sugerencia: normalmente es un sustantivo**. Por ejemplo, las tablas `user` y `orders` describen explícitamente usuarios y pedidos.

1. Identifique uno o más verbos que describan cómo interactúan estas entidades. Por ejemplo, al comparar usuarios con pedidos, los usuarios &quot;realizan&quot; pedidos. En la otra dirección, los pedidos &quot;pertenecen&quot; a los usuarios.

Este tipo de marco de trabajo se puede aplicar a cualquier emparejamiento de tablas en la Data Warehouse. Esto le permite identificar fácilmente el tipo de relación y qué tabla es un lado uno y qué tabla es un lado varios.

Una vez identificada la terminología que describe cómo interactúan las dos tablas, enmarque la interacción en ambas direcciones teniendo en cuenta cómo se relaciona una instancia determinada de la primera entidad con la segunda. Estos son algunos ejemplos de cada relación:

### `One-to-One`

Una persona determinada solo puede tener un número de licencia de conducir. Un determinado número de licencia de conducir pertenece a una sola persona.

Se trata de una relación de `one-to-one` en la que cada tabla es un lado uno.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Un pedido determinado puede contener muchos elementos. Un elemento dado pertenece a un único pedido.

Se trata de una relación de `one-to-many` en la que la tabla pedidos es el lado uno y la tabla elementos es el lado varios.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Un producto dado puede pertenecer posiblemente a muchas categorías. Una categoría determinada puede contener muchos productos.

Se trata de una relación de `many-to-many` en la que cada tabla es un lado varios.

![](../../assets/many-to-many3.png)

### Uso del esquema de la tabla {#schema}

El segundo método utiliza el esquema de tabla. El esquema define qué columnas son las claves [`Primary`](https://en.wikipedia.org/wiki/Unique_key) y [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key). Puede utilizar estas claves para vincular tablas y ayudar a determinar los tipos de relación.

Una vez identificadas las columnas que vinculan dos tablas, utilice los tipos de columna para evaluar la relación entre las tablas. Estos son algunos ejemplos:

### `One-to-one`

Si las tablas están vinculadas utilizando el `primary key` de ambas tablas, se describe la misma entidad única en cada tabla y la relación es `one-to-one`.

Por ejemplo, una tabla `users` puede capturar la mayoría de los atributos de usuario (como el nombre) mientras que una tabla `user_source` suplementaria captura los orígenes de registro de usuario. En cada tabla, una fila representa un usuario.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>¿Aceptas órdenes de invitados? Vea [Pedidos de invitado](../data-warehouse-mgr/guest-orders.md) para conocer cómo los pedidos de invitado pueden afectar las relaciones de tabla.

Cuando las tablas se vinculan mediante un `Foreign key` que señala a un `primary key`, esta configuración describe una relación de `one-to-many`. El lado uno es la tabla que contiene `primary key` y el lado varios es la tabla que contiene `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Si alguna de las siguientes opciones es verdadera, la relación es `many-to-many`:

* Se están utilizando `Non-primary key` columnas para vincular dos tablas
  ![](../../assets/many-to-many1.png)
* Parte de un(a) `primary key` compuesto(a) se usa para vincular dos tablas

![](../../assets/many-to-mnay2.png)

## Pasos siguientes

La evaluación correcta de las relaciones de tabla es crucial para modelar los datos con precisión. Ahora que comprende cómo se relacionan las tablas, vea [lo que puede hacer con el Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md).
