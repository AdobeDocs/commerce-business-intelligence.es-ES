---
title: tabla sales_order_item
description: Aprenda a trabajar con la tabla sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Tabla `sales_order_item`

La tabla `sales_order_item` (`sales_flat_order_item` en M1) contiene registros de todos los productos comprados en un pedido. Cada fila representa un(a) `sku` único(a) incluido en un pedido. La cantidad de unidades compradas para un(a) `sku` específico(a) se representa con mayor frecuencia mediante el campo `qty_ordered`.

## Tipos de productos

`sales_order_item` captura detalles de todos los [tipos de productos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=es#product-types) que se compraron. Una práctica habitual de [!DNL Adobe Commerce] es ofrecer productos configurables o, en otras palabras, un producto que se pueda personalizar según el tamaño, el color y otros atributos del producto. Aunque un producto configurable tiene su propio `sku`, puede estar relacionado con varios productos simples, en los que cada producto simple representa una configuración de producto única. Consulte [configurar productos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obtener más información.

Por ejemplo, piense en un producto configurable como una camiseta. Cuando un cliente cierra la compra, selecciona opciones para modificar el color y el tamaño. Si el cliente selecciona un color de `blue` y un tamaño de `small`, acaba comprando un producto simple como `t-shirt-blue-small` que se relaciona con el producto principal de `t-shirt`.

Cuando se incluye un producto configurable en un pedido, se generan dos filas en la tabla `sales_order_item`: una para el [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html?lang=es) `sku` y otra para el elemento principal [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=es). Estos dos registros de la tabla `sales_order_item` se pueden relacionar entre sí mediante la siguiente combinación:

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Por lo tanto, es posible informar sobre las ventas de productos en el nivel simple o en el nivel configurable. De manera predeterminada, todas las métricas estándar de `order-item-level` en [!DNL Commerce Intelligence] están configuradas para excluir los productos simples y *solo* informan sobre las versiones configurables. Esto se logra a través del conjunto de filtros `Ordered products we count`, que filtra en la condición donde `parent_item_id` es `NULL`.

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|----|----|
| `base_price` | Precio de una unidad individual de un producto en el momento de la venta después de aplicar [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=es), y antes de aplicar impuestos, envíos o descuentos del carro de compras. Se representa en la moneda base de la tienda. |
| `created_at` | Marca de tiempo de creación del elemento de pedido, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos. |
| `item_id` (PK) | Identificador único de la tabla. |
| `name` | Nombre de texto del elemento de pedido. |
| `order_id` | `Foreign key` se asoció con la tabla `sales_order`. Únase a `sales_order.entity_id` para determinar los atributos de pedido asociados con el elemento de pedido. |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Únase a `sales_order_item.item_id` para determinar los atributos de producto principales asociados con un producto simple. Para los elementos de pedido principales (es decir, paquetes o tipos de productos configurables), `parent_item_id` es `NULL`. |
| `product_id` | `Foreign key` se asoció con la tabla `catalog_product_entity`. Únase a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados con el elemento de pedido. |
| `product_type` | Tipo de producto que se vendió. Los [tipos de productos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=es#product-types) potenciales incluyen: simple, configurable, agrupado, virtual, agrupado y descargable. |
| `qty_ordered` | Cantidad de unidades incluidas en el carro de compras para el artículo de pedido concreto en el momento de la venta. |
| `sku` | Identificador único del artículo de pedido que se compró. |
| `store_id` | `Foreign key` se asoció con la tabla `store`. Únase a `store.store_id` para determinar qué vista de la tienda Commerce está asociada con el elemento de pedido. |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Customer's email` | Dirección de correo electrónico del cliente que realiza el pedido. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `customer_email`. |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `Customer's lifetime number of orders`. |
| `Customer's lifetime revenue` | Suma del total de ingresos de todos los pedidos realizados por este cliente. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `Customer's lifetime revenue`. |
| `Customer's order number` | Clasificación de pedido secuencial para el pedido de este cliente. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `Customer's order number`. |
| `Order item total value (quantity * price)` | Valor total de un artículo de pedido en el momento de la venta después de aplicar [reglas de precio de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=es), y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Se calcula multiplicando `qty_ordered` por `base_price`. |
| `Order's coupon_code` | Cupón aplicado al pedido. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `coupon_code`. |
| `Order's increment_id` | Identificador único del pedido. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `increment_id`. |
| `Order's status` | Estado del pedido. Se calcula uniendo `sales_order_item.order_id` a `sales_order.entity_id` y devolviendo el campo `status`. |
| `Store name` | Nombre del almacén de Commerce asociado al artículo de pedido. Se calcula uniendo `sales_order_item.store_id` a `store.store_id` y devolviendo el campo `name`. |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Products ordered` | Cantidad total de productos incluidos en los carros de compras en el momento de la venta | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valor total de los productos incluidos en los carros de compras en el momento de la venta después de aplicar las reglas de precio del catálogo, los descuentos por niveles y los precios especiales, y antes de aplicar los impuestos, el envío o los descuentos del carro de compras | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Rutas de unión

`catalog_product_entity`

* Únase a la tabla `catalog_product_entity` para crear columnas que devuelvan atributos de producto asociados con el elemento de pedido.
   * Ruta de acceso: `sales_order_item.product_id` (varios) => `catalog_product_entity.entity_id` (uno)

`sales_order`

* Únase a la tabla `sales_order` para crear nuevas columnas de nivel de pedido asociadas al elemento de pedido.
   * Ruta de acceso: `sales_order_item.order_id` (varios) => `sales_order.entity_id` (uno)

`sales_order_item`

* Únase a `sales_order_item` para crear columnas que asocien detalles del SKU principal configurable o del paquete con el producto simple. [Póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) para obtener ayuda con la configuración de estos cálculos, si está generando en el administrador de Data Warehouse.
   * Ruta de acceso: `sales_order_item.parent_item_id` (varios) => `sales_order_item.item_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén de Commerce asociado al elemento de pedido.
   * Ruta de acceso: `sales_order_item.store_id` (varios) => `store.store_id` (uno)
