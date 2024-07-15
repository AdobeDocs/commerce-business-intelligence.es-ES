---
title: Almacenamiento de datos en Adobe Commerce
description: Descubra cómo se generan los datos, qué hace que se inserte una nueva fila y cómo se registran las acciones en la base de datos de Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Almacenando datos en [!DNL Adobe Commerce]

La plataforma [!DNL Adobe Commerce] registra y organiza una amplia variedad de valiosos datos comerciales en cientos de tablas. En este tema se describe:

* cómo se generan esos datos
* ¿qué hace que se inserte una nueva fila en una de las [tablas principales de Commerce](../data-warehouse-mgr/common-mage-tables.md)?
* cómo se registran acciones como realizar una compra o crear una cuenta en la base de datos [!DNL Adobe Commerce]

Para discutir estos conceptos, consulte el siguiente ejemplo:

`Clothes4U` es un minorista de ropa con presencia tanto en línea como física. Utiliza [!DNL Magento Open Source] detrás de su sitio web para recopilar y organizar los datos.

## `catalog\_product\_entity`

Es 22 de septiembre y `Clothes4U` está desplegando tres nuevos elementos a su línea de otoño: `Throwback Bellbottoms`, `Straight Leg Jeans` y `V-Neck T-Shirts`. Un empleado de `Clothes4U` abre su administrador de Commerce, hace clic en **[!UICONTROL Add Product]** e introduce toda la información de `Throwback Bellbottoms`.

Satisfecho con toda la configuración de `Throwback Bellbottoms`, el empleado hace clic en **[!UICONTROL Save]**, que inserta la primera línea debajo de la tabla `catalog_product_entity`. El empleado repite el proceso, creando otro producto de Commerce para `Straight Leg Jeans` y, a continuación, un tercero para `V-Neck T-Shirt`, insertando la segunda y tercera líneas a continuación en la tabla `catalog_product_entity`:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pantalones10 | 22/09/2016 09:15:43 |
| 206 | 4 | 8 | Pantalones11 | 22/09/2016 09:18:17 |
| 207 | 4 | 12 | Camisas6 | 22/09/2016 09:24:02 |

* `entity_id`: esta es la clave principal de la tabla `catalog_product_entity`, lo que significa que cada fila de la tabla debe tener un `entity_id` diferente. Cada `entity_id` de esta tabla solo puede asociarse con un producto, y cada producto solo puede asociarse con un `entity_id`
   * La línea superior de la tabla anterior, `entity_id` = 205, es la nueva fila creada para &quot;Throwback Bellbottom&quot;. Dondequiera que `entity_id` = 205 aparezca en la plataforma Commerce, se refiere al producto &quot;Throwback Bellbottom&quot;
* `entity_type_id`: Commerce tiene varias categorías de objetos (como clientes, direcciones y productos, por nombrar algunos) y esta columna se utiliza para denotar la categoría a la que pertenece esta fila en particular.
   * Siendo esta la tabla `catalog_product_entity`, cada fila tiene el mismo tipo de entidad: producto. En Adobe Commerce, `entity_type_id` para el producto es 4, por lo que los tres nuevos productos creados devuelven 4 para esta columna.
* `attribute_set_id`: los conjuntos de atributos se utilizan para identificar productos que tienen el mismo tipo de descriptores.
   * Las dos filas superiores de la tabla son los productos `Throwback Bellbottoms` y `Straight Leg Jeans`, los cuales son pantalones. Estos productos tendrían los mismos descriptores (por ejemplo, nombre, ancho, cintura) y, por lo tanto, tendrían los mismos `attribute_set_id`. El tercer elemento, `V-Neck T-Shirt` tiene un `attribute_set_id` diferente porque no tendría los mismos descriptores que los pantalones; las camisas no tienen cinturas ni costuras.
* `sku`: son valores únicos asignados a cada producto por el usuario al crear un producto en Adobe Commerce.
* `created_at` - Esta columna devuelve la marca de tiempo del momento en que se creó cada producto

## `customer\_entity`

Poco después de la adición de los tres nuevos productos, un nuevo cliente, `Sammy Customer`, visita el sitio web de `Clothes4U` por primera vez. Dado que `Clothes4U` no permite pedidos de invitados, `Sammy Customer` debe crear primero una cuenta en el sitio web. El cliente introduce las credenciales necesarias y hace clic en Enviar, lo que da como resultado la nueva entrada siguiente en [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Al igual que la tabla anterior, `entity_id` es la clave principal de la tabla `customer_entity`.
   * Cuando `Sammy Customer` creó una cuenta y la fila anterior se escribió en la tabla `customer_entity`, se asignó al cliente `entity_id` = 214. En todas las tablas, el cliente identificado como `entity_id` = 214 siempre hace referencia al usuario Sammy Customer
* `entity_type_id`: esta columna identifica qué tipo de entidad se enumera en esta tabla y funciona de la misma manera que en la tabla `catalog_product_entity`
   * Cada fila de la tabla `customer_entity` es un cliente y Commerce define los clientes como `entity_type_id` 1 de forma predeterminada
* `email`: este campo se completa con el correo electrónico que introduce un nuevo cliente al crear su cuenta
* `created_at` - Esta columna devuelve la marca de tiempo del momento en que se unió cada usuario

## `sales\_flat\_order (or Sales\_order` si tiene [!DNL Adobe Commerce 2.x]

Una vez finalizada la creación de la cuenta, `Sammy Customer` está listo para comenzar a realizar una compra. En el sitio web, el cliente agrega dos pares de `Throwback Bellbottoms` y uno `V-Neck T-Shirt` al carro de compras. Satisfecho con las selecciones, el cliente pasa al cierre de compra y envía el pedido, creando la siguiente entrada en la [tabla de pedidos planos de ventas](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 23/09/2016 15:41:39 |

* `entity_id`: esta es la clave principal de la tabla `sales_flat_order`.
   * Cuando el cliente Sammy hizo este pedido y la fila anterior se escribió en la tabla `sales_flat_order`, se asignó el pedido a `entity_id` = 227.
* `customer_id`: esta columna es el identificador único del cliente que realizó este pedido en particular
   * El `customer_id` asociado con este pedido es 214, que es el `entity_id` del cliente Sammy en la tabla `customer_entity`.
* `subtotal`: esta columna es el importe total que se cobra a un cliente por el pedido
   * Los dos pares de &quot;Throwback Bellbottom&quot; y &quot;V-Neck T-Shirt&quot; costaron $94.85 dólares en total
* `created_at` - Esta columna devuelve la marca de tiempo del momento en que se creó cada pedido

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(si tiene Commerce 2.0 o posterior)

Además de la única fila de la tabla `Sales\_flat\_order`, cuando `Sammy Customer` envía el pedido, se inserta una fila para cada elemento único en ese orden en la tabla [`sales\_flat\_order\_item`](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Esta columna es la clave principal de la tabla `sales_flat_order_item`
   * El pedido de `Sammy Customer` ha creado dos líneas en esta tabla porque el pedido contenía dos productos distintos
* `name` - Esta columna es el nombre del producto
* `product_id`: esta columna es el identificador único del producto al que se refiere esta fila
   * La primera fila anterior tiene `product_id` = 205 porque `Throwback Bellbottoms` tiene un `entity_id` de 205 en la tabla `catalog_product_entity`
* `order_id` - Esta columna es el `entity_id` del pedido que contiene estos elementos de pedido en particular
   * Ambas filas tienen `order_id` = 227 porque ambas forman parte del pedido realizado por `Sammy Customer`, que tiene `entity_id` = 227 en la tabla `sales_flat_order`
* `qty_ordered`: esta columna es el número de unidades del producto que se incluyen en este pedido específico
   * El pedido de `Sammy Customer` contenía dos pares de `Throwback Bellbottoms`
* `price` - Esta columna es el precio de una sola unidad del artículo de pedido
   * El pedido de `subtotal` de `Sammy Customer` en la tabla `sales_flat_order` era 94,85, que es la suma de dos pares de `Throwback Bellbottoms` a $39,95 cada uno y 1 `V-Neck T-Shirt` a $14,95.
