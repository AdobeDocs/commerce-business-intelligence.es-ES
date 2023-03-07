---
title: tabla sales_order_item
description: Aprenda a trabajar con la tabla sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# `sales_order_item` Tabla

El `sales_order_item` tabla (`sales_flat_order_item` en M1 1) contiene registros de todos los productos comprados en un pedido. Cada fila representa un único `sku` incluido en un pedido. La cantidad de unidades que se compraron para un `sku` se representa con mayor frecuencia mediante el `qty_ordered` field.

## Tipos de productos

El `sales_order_item` captura detalles en todos los [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) que se compraron. Una práctica común en Commerce es ofrecer productos configurables, o en otras palabras, un producto que se puede personalizar según el tamaño, el color y otros atributos del producto. Aunque un producto configurable tiene su propio `sku`, puede estar relacionado con varios productos simples, donde cada producto simple representa una configuración de producto única. Consulte [configuración de productos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obtener más información.

Por ejemplo, piense en un producto configurable como una camiseta. Cuando un cliente cierra la compra, selecciona opciones para modificar el color y el tamaño. Si el cliente selecciona un color de `blue`y un tamaño de `small`Sin embargo, terminan comprando un producto simple como `t-shirt-blue-small` que se refiere al producto principal de `t-shirt`.

Cuando se incluye un producto configurable en un pedido, se generan dos filas en la `sales_order_item` tabla: uno para [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`y uno para el [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) principal. Estos dos registros en la `sales_order_item` La tabla se puede relacionar entre sí mediante la siguiente combinación:

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Por lo tanto, es posible informar sobre las ventas de productos en el nivel simple o en el nivel configurable. De forma predeterminada, todas las `order-item-level` métricas en [!DNL MBI] están configurados para excluir los productos simples y *solamente* informe sobre las versiones configurables. Esto se logra a través de `Ordered products we count` conjunto de filtros, que filtra la condición donde `parent_item_id` es `NULL`.

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|----|----|
| `base_price` | Precio de una unidad individual de un producto en el momento de la venta después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Esto se representa en la moneda base de la tienda |
| `created_at` | Marca de tiempo de creación del elemento de pedido, almacenada localmente en UTC. Según la configuración en [!DNL MBI], esta marca de tiempo se puede convertir en una zona horaria de informe en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `order_id` | `Foreign key` asociado con el `sales_order` tabla. Unirse a `sales_order.entity_id` para determinar los atributos de pedido asociados al artículo de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Unirse a `sales_order_item.item_id` para determinar los atributos de producto principales asociados a un producto simple. Para los artículos de pedido principales (es decir, paquetes o tipos de producto configurables), la variable `parent_item_id` es `NULL` |
| `product_id` | `Foreign key` asociado con el `catalog_product_entity` tabla. Unirse a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados al artículo de pedido |
| `product_type` | Tipo de producto que se vendió. potencial [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluir: simple, configurable, agrupado, virtual, paquete y descargable |
| `qty_ordered` | Cantidad de unidades incluidas en el carro de compras para el artículo de pedido concreto en el momento de la venta |
| `sku` | Identificador único del artículo de pedido que se compró |
| `store_id` | `Foreign key` asociado con el `store` tabla. Unirse a `store.store_id` para determinar qué vista de la tienda de comercio está asociada al artículo de pedido |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Customer's email` | Dirección de correo electrónico del cliente que realiza el pedido. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `customer_email` campo |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `Customer's lifetime number of orders` campo |
| `Customer's lifetime revenue` | Suma del total de ingresos de todos los pedidos realizados por este cliente. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `Customer's lifetime revenue` campo |
| `Customer's order number` | Clasificación de pedido secuencial para el pedido de este cliente. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `Customer's order number` campo |
| `Order item total value (quantity * price)` | Valor total de un artículo de pedido en el momento de la venta después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Se calcula multiplicando el `qty_ordered` por el `base_price` |
| `Order's coupon_code` | Cupón aplicado al pedido. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `coupon_code` campo |
| `Order's increment_id` | Identificador único del pedido. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `increment_id` campo |
| `Order's status` | Estado del pedido. Calculado al unirse `sales_order_item.order_id` hasta `sales_order.entity_id` y devolviendo el `status` campo |
| `Store name` | Nombre de la tienda de Commerce asociada con el artículo de pedido. Calculado al unirse `sales_order_item.store_id` hasta `store.store_id` y devolviendo el `name` campo |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Products ordered` | Cantidad total de productos incluidos en los carros de compras en el momento de la venta | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valor total de los productos incluidos en los carros de compras en el momento de la venta después de aplicar las reglas de precio del catálogo, los descuentos por niveles y los precios especiales, y antes de aplicar los impuestos, el envío o los descuentos del carro de compras | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Unir rutas

`catalog_product_entity`

* Unirse a `catalog_product_entity` tabla para crear columnas que devuelven atributos de producto asociados al artículo de pedido.
   * Ruta: `sales_order_item.product_id` (muchos) => `catalog_product_entity.entity_id` (uno)

`sales_order`

* Unirse a `sales_order` para crear nuevas columnas de nivel de pedido asociadas al artículo de pedido.
   * Ruta: `sales_order_item.order_id` (muchos) => `sales_order.entity_id` (uno)

`sales_order_item`

* Unirse a `sales_order_item` para crear columnas que asocien detalles del SKU configurable o del paquete principal con el producto simple. [Atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para obtener ayuda sobre la configuración de estos cálculos, si está compilando en el administrador de Datas Warehouse.
   * Ruta: `sales_order_item.parent_item_id` (muchos) => `sales_order_item.item_id` (uno)

`store`

* Unirse a `store` para crear columnas que devuelvan detalles relacionados con el almacén de comercio asociado al artículo de pedido.
   * Ruta: `sales_order_item.store_id` (muchos) => `store.store_id` (uno)
