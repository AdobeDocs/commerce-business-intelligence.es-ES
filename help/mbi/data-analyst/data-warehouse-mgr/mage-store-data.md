---
title: Almacenamiento de datos en Adobe Commerce
description: Descubra cómo se generan los datos, qué hace que se inserte una nueva fila y cómo se registran las acciones en la base de datos de Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Almacenamiento de datos en [!DNL Adobe Commerce]

El [!DNL Adobe Commerce] platform registra y organiza una amplia variedad de valiosos datos comerciales en cientos de tablas. En este tema se describe:

* cómo se generan esos datos
* ¿qué hace que se inserte una nueva fila en una de las [Tablas de comercio principales](../data-warehouse-mgr/common-mage-tables.md)
* cómo se registran acciones como realizar una compra o crear una cuenta en la [!DNL Adobe Commerce] database

Para discutir estos conceptos, consulte el siguiente ejemplo:

`Clothes4U` es un minorista de ropa con presencia en línea y de ladrillo y mortero. Utiliza [!DNL Magento Open Source] detrás de su sitio web para recopilar y organizar los datos.

## `catalog\_product\_entity`

Es el 22 de septiembre, y `Clothes4U` está desplegando tres nuevos elementos a su línea de otoño: `Throwback Bellbottoms`, `Straight Leg Jeans`, y `V-Neck T-Shirts`. A `Clothes4U` El empleado abre el administrador de Commerce y hace clic en **[!UICONTROL Add Product]** e introduce toda la información de `Throwback Bellbottoms`.

Satisfecho con todos los ajustes de `Throwback Bellbottoms`, el empleado hace clic en **[!UICONTROL Save]**, que inserta la primera línea debajo de en la `catalog_product_entity` tabla. El empleado repite el proceso y crea otro producto de comercio para `Straight Leg Jeans`y luego un tercero para `V-Neck T-Shirt`, insertando la segunda y tercera líneas debajo en la `catalog_product_entity` tabla:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Esta es la clave principal de `catalog_product_entity` tabla, lo que significa que cada fila de la tabla debe tener un `entity_id`. Cada `entity_id` en esta tabla solo se puede asociar a un producto, y cada producto solo se puede asociar a uno `entity_id`
   * La línea superior de la tabla anterior, `entity_id` = 205, es la nueva fila creada para &quot;Throwback Bellbottom&quot;. Dondequiera `entity_id` = 205 aparece en la plataforma de Commerce, se refiere al producto &quot;Throwback Bellbottom&quot;
* `entity_type_id` : el comercio tiene varias categorías de objetos (como clientes, direcciones y productos, por nombrar algunos) y esta columna se utiliza para denotar la categoría en la que se encuentra esta fila en particular.
   * Siendo este el `catalog_product_entity` , cada fila tiene el mismo tipo de entidad: producto. En Adobe Commerce, la variable `entity_type_id` para el producto es 4, por lo que los tres nuevos productos creados devuelven 4 para esta columna.
* `attribute_set_id` - Los conjuntos de atributos se utilizan para identificar productos que tienen el mismo tipo de descriptores.
   * Las dos filas superiores de la tabla son las siguientes `Throwback Bellbottoms` y `Straight Leg Jeans` productos, ambos de los cuales son pantalones. Estos productos tendrían los mismos descriptores (por ejemplo, nombre, pierna, cintura) y, por lo tanto, tienen el mismo `attribute_set_id`. El tercer elemento, `V-Neck T-Shirt` tiene un diferente `attribute_set_id` porque no tendría los mismos descriptores que los pantalones; las camisas no tienen cinturas ni costuras.
* `sku` - Son valores únicos asignados a cada producto por el usuario al crear un producto en Adobe Commerce.
* `created_at` : Esta columna devuelve la marca de tiempo del momento en el que se creó cada producto

## `customer\_entity`

Poco después de la adición de los tres nuevos productos, un nuevo cliente, `Sammy Customer`, visitas `Clothes4U`El sitio web de por primera vez. Desde `Clothes4U` no permite pedidos de invitados, `Sammy Customer` primero debe crear una cuenta en el sitio web. El cliente introduce las credenciales necesarias y hace clic en Enviar, lo que da como resultado la nueva entrada siguiente en la [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Igual que la mesa anterior, `entity_id` es la clave principal de `customer_entity` tabla.
   * Cuándo `Sammy Customer` creó una cuenta y la fila anterior se escribió en `customer_entity` tabla, se asignó al cliente `entity_id` = 214. En todas las tablas, el cliente se identificó como `entity_id` = 214 siempre hace referencia al usuario Sammy Customer
* `entity_type_id` : Esta columna identifica qué tipo de entidad se enumera en esta tabla y funciona del mismo modo que en la `catalog_product_entity` tabla
   * Cada fila de la `customer_entity` es un cliente de y Commerce define los clientes como `entity_type_id` 1 de forma predeterminada
* `email` : este campo se rellena mediante el correo electrónico que introduce un nuevo cliente al crear su cuenta
* `created_at` : Esta columna devuelve la marca de tiempo del momento en el que se unió cada usuario

## `sales\_flat\_order (or Sales\_order` si tiene [!DNL Adobe Commerce 2.x]

Una vez finalizada la creación de la cuenta, `Sammy Customer` está listo para empezar a realizar una compra. En el sitio web, el cliente agrega dos pares del `Throwback Bellbottoms` y uno `V-Neck T-Shirt` al carro de compras. Satisfecho con las selecciones, el cliente pasa a la caja y envía el pedido, creando la siguiente entrada en la [tabla de pedido plano de ventas](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - esta es la clave principal del `sales_flat_order` tabla.
   * Cuando el cliente Sammy hizo este pedido y la fila de arriba se escribió en el `sales_flat_order` tabla, se ha asignado el orden `entity_id` = 227.
* `customer_id` : Esta columna es el identificador único del cliente que realizó este pedido en particular
   * El `customer_id` asociado con este pedido es 214, que es de Sammy Cliente `entity_id` en el `customer_entity` tabla.
* `subtotal` : Esta columna es el importe total cargado a un cliente por el pedido
   * Los dos pares de &quot;Throwback Bellbottom&quot; y &quot;V-Neck T-Shirt&quot; costaron $94.85 dólares en total
* `created_at` : Esta columna devuelve la marca de tiempo del momento en el que se creó cada pedido

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(si tiene Commerce 2.0 o posterior)

Además de la única fila de la `Sales\_flat\_order` tabla, cuándo `Sammy Customer` envía el pedido, se inserta una fila para cada elemento único de ese orden en la [`sales\_flat\_order\_item` tabla](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` : esta columna es la clave principal de la variable `sales_flat_order_item` tabla
   * `Sammy Customer`El pedido de ha creado dos líneas en esta tabla porque el pedido contenía dos productos distintos
* `name` - Esta columna es el nombre del producto
* `product_id` : Esta columna es el identificador único del producto al que se refiere esta fila
   * La primera fila de arriba tiene `product_id` = 205 porque `Throwback Bellbottoms` tener un `entity_id` de 205 en el `catalog_product_entity` tabla
* `order_id` - Esta columna es la `entity_id` del pedido que contiene estos elementos de pedido en particular
   * Las dos filas anteriores tienen `order_id` = 227 porque ambos forman parte del pedido realizado por `Sammy Customer`, que tiene `entity_id` = 227 en el `sales_flat_order` tabla
* `qty_ordered` - Esta columna es el número de unidades del producto que se incluyen en este pedido específico
   * `Sammy Customer`El pedido de contenía dos pares de `Throwback Bellbottoms`
* `price` - Esta columna es el precio de una sola unidad del artículo de pedido
   * El `subtotal` de `Sammy Customer`El pedido de en el `sales_flat_order` la tabla era 94,85, que es la suma de dos pares de `Throwback Bellbottoms` a $39.95 cada uno y 1 `V-Neck T-Shirt` a 14,95 dólares.
