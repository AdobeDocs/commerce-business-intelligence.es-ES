---
title: Almacenamiento de datos en el comercio
description: Descubra cómo se generan los datos, qué hace que se inserte una nueva fila en una de las tablas de comercio principales y cómo se registran acciones como realizar una compra o crear una cuenta en la base de datos de comercio.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Almacenamiento de datos en [!DNL Magento]

La plataforma Commerce registra y organiza una amplia variedad de datos de comercio valiosos en cientos de tablas. En este tema, aprenderá cómo se generan esos datos, qué hace exactamente que se inserte una nueva fila en una de las [Tablas de comercio principales](../data-warehouse-mgr/common-mage-tables.md), y cómo se registran acciones como realizar una compra o crear una cuenta en la base de datos de Commerce. Para explicar estos conceptos, consulte el siguiente ejemplo:

`Clothes4U` es un comerciante de ropa con presencia en línea, de ladrillo y de mortero. Utiliza un Magento Open Source detrás de su sitio web para recopilar y organizar datos.

## `catalog\_product\_entity`

es el 22 de septiembre y `Clothes4U` está desplegando tres nuevos elementos en su línea de otoño: `Throwback Bellbottoms`, `Straight Leg Jeans`y `V-Neck T-Shirts`. A `Clothes4U` el empleado abre su administrador de comercio con los clics **[!UICONTROL Add Product]** e introduce toda la información de `Throwback Bellbottoms`.

Satisfecho con todos los ajustes de `Throwback Bellbottoms`, el empleado hace clic en **[!UICONTROL Save]**, que inserta la primera línea debajo de en el `catalog_product_entity` tabla. El empleado repite el proceso y crea otro nuevo producto de comercio para `Straight Leg Jeans`y luego un tercio para `V-Neck T-Shirt`, insertando las líneas segunda y tercera debajo en el `catalog_product_entity` tabla:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pantalones10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pantalones11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Camisas6 | 2016/09/22 09:24:02 |

* `entity_id` - Esta es la clave principal del `catalog_product_entity` tabla, lo que significa que cada fila de la tabla debe tener un `entity_id`. Cada `entity_id` en esta tabla solo puede asociarse con un producto, y cada producto solo puede asociarse con uno `entity_id`
   * La línea superior de la tabla anterior, `entity_id` = 205, es la nueva fila creada para &quot;Throwback Bellbotoms&quot;. Donde quiera `entity_id` = 205 aparece en la plataforma de comercio; se referirá al producto &quot;Throwback Bellbotoms&quot;
* `entity_type_id` - Comercio tiene varias categorías de objetos (como clientes, direcciones y productos por nombrar algunos), y esta columna se utiliza para indicar la categoría a la que pertenece esta fila en particular.
   * Esta es la `catalog_product_entity` tabla, cada fila tiene el mismo tipo de entidad: producto. En Magento, la variable `entity_type_id` para el producto es 4, por lo que los tres nuevos productos creados devuelven 4 para esta columna.
* `attribute_set_id` - Los conjuntos de atributos se utilizan para identificar productos que tienen el mismo tipo de descriptores.
   * Las dos filas superiores de la tabla son la `Throwback Bellbottoms` y `Straight Leg Jeans` productos, ambos pantalones. Estos productos tendrían los mismos descriptores (por ejemplo, nombre, nombre, línea de espera) y, por lo tanto, tienen los mismos `attribute_set_id`. El tercer punto, `V-Neck T-Shirt` tiene un `attribute_set_id` porque no tendría los mismos descriptores que los pantalones; las camisas no tienen cintura ni inseams.
* `sku` : son valores únicos asignados a cada producto por el usuario al crear un nuevo producto en el Magento.
* `created_at` - Esta columna devuelve la marca de tiempo de cuando se creó cada producto

## `customer\_entity`

Poco después de la adición de los tres nuevos productos, un nuevo cliente, `Sammy Customer`, visitas `Clothes4U`por primera vez. Since `Clothes4U` no [permitir pedidos de invitado](https://support.magento.com/hc/en-us/articles/360016729951-Common-Magento-Misconceptions), `Sammy Customer` primero debe crear una cuenta en el sitio web. Ella introduce sus credenciales y hace clic en enviar, lo que resulta en la siguiente nueva entrada en la [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Igual que la tabla anterior, `entity_id` es la clave principal del `customer_entity` tabla.
   * When `Sammy Customer` creó su cuenta y la fila anterior se escribió en la `customer_entity` tabla, se le asignó `entity_id` = 214. En todas las tablas, el cliente identificado como `entity_id` = 214 siempre se referirá al usuario Sammy Customer
* `entity_type_id` - Esta columna identifica qué tipo de entidad se está enumerando en esta tabla y funciona del mismo modo que en la `catalog_product_entity` tabla
   * Cada fila del `customer_entity` La tabla será un cliente y Commerce define a los clientes como `entity_type_id` 1 de forma predeterminada
* `email` : este campo se rellena con el correo electrónico que introduce un nuevo cliente al crear su cuenta
* `created_at` - Esta columna devuelve la marca de tiempo de cada usuario unido

## `sales\_flat\_order (or Sales\_order` si tiene Commerce 2.0 o posterior)

Con la creación de su cuenta finalizada, `Sammy Customer` está lista para empezar a realizar su compra. A medida que navega por el sitio web, agrega dos pares de `Throwback Bellbottoms` y una `V-Neck T-Shirt` a su carrito. Satisfaga con sus selecciones, se desplaza al cierre de compra y envía su pedido, creando la siguiente entrada en el [tabla de pedido plano de ventas](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 23/09/2016 15:41:39 |

* `entity_id` - esta es la clave principal del `sales_flat_order` tabla.
   * Cuando el cliente de Sammy realizó este pedido y la fila anterior se escribió en la variable `sales_flat_order` tabla, orden asignada `entity_id` = 227.
* `customer_id` - Esta columna es el identificador único del cliente que realizó este pedido en particular
   * La variable `customer_id` asociado con este pedido es 214, que es el cliente de Sammy `entity_id` en el `customer_entity` tabla.
* `subtotal` - Esta columna es la cantidad total cobrada a un cliente por el pedido
   * Los dos pares de &quot;Throwback Bellbotoms&quot; y la &quot;V-Neck T-Shirt&quot; costaron $94.85 dólares en total
* `created_at` - Esta columna devuelve la marca de tiempo de la creación de cada pedido

## `sales\_flat\_order\_item ( or Sales\_order\_item` si tiene Commerce 2.0 o posterior)

Además de la fila única en la `Sales\_flat\_order` cuando `Sammy Customer` envía su pedido, se inserta una fila para cada elemento único en ese orden en la variable [`sales\_flat\_order\_item` tabla](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Esta columna es la clave principal del `sales_flat_order_item` tabla
   * `Sammy Customer`El pedido de ha creado dos líneas en esta tabla porque su pedido contenía dos productos distintos
* `name` - Esta columna es el nombre del producto
* `product_id` - Esta columna es el identificador único del producto al que se refiere esta fila
   * La primera fila de arriba tiene `product_id` = 205 porque `Throwback Bellbottoms` tienen un `entity_id` de 205 sobre `catalog_product_entity` tabla
* `order_id` - Esta columna es la `entity_id` del orden que contiene estos elementos de pedido en particular
   * Ambas filas anteriores tienen `order_id` = 227 porque ambas forman parte del pedido realizado por `Sammy Customer`, que `entity_id` = 227 en la variable `sales_flat_order` tabla
* `qty_ordered` - Esta columna es el número de unidades del producto que se incluyen en este pedido específico
   * `Sammy Customer`El orden de contiene 2 pares de `Throwback Bellbottoms`
* `price` - Esta columna es el precio de una sola unidad del artículo de pedido
   * La variable `subtotal` from `Sammy Customer`en el `sales_flat_order` el cuadro era 94,85, que es la suma de 2 pares de `Throwback Bellbottoms` a 39,95 dólares cada uno y 1 `V-Neck T-Shirt` a 14,95 dólares.
