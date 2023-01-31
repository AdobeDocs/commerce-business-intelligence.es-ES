---
title: tabla sales_order_item
description: Aprenda a trabajar con la tabla sales_order_item .
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c0892aa046c80f90561b4a178525ef9ed05b435a
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# `sales_order_item` Tabla

La variable `sales_order_item` tabla (`sales_flat_order_item` en [!DNL Magento] 1) contiene registros de todos los productos que se compraron en un pedido. Cada fila representa un `sku` incluido en un pedido. La cantidad de unidades compradas para un `sku` se representa con mayor frecuencia por la variable `qty_ordered` campo .

## Tipos de productos

La variable `sales_order_item` captura detalles de todos [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) que se compraron. Una práctica habitual en Comercio es ofrecer productos configurables o, en otras palabras, un producto que se puede personalizar según el tamaño, el color y otros atributos del producto. Aunque un producto configurable tiene su propio `sku`, puede estar relacionado con varios productos simples, donde cada producto simple representa una configuración de producto única. Consulte [configuración de productos](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) para obtener más información.

Por ejemplo, considere un producto configurable como una camiseta. Cuando un cliente cierra la compra, selecciona opciones para modificar el color y el tamaño. Si el cliente selecciona un color de `blue`y un tamaño de `small`, terminan comprando un producto simple como `t-shirt-blue-small` que se refiere al producto primario de `t-shirt`.

Cuando un producto configurable se incluye en un pedido, se generan dos filas en la variable `sales_order_item` tabla: uno para el [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`y una para la variable [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) principal. Estos dos registros en la variable `sales_order_item` se puede relacionar entre sí mediante el siguiente vínculo:

* (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Por lo tanto, es posible informar sobre las ventas de productos tanto en el nivel simple como en el nivel configurable. De forma predeterminada, todas las `order-item-level` métricas en [!DNL MBI] están configurados para excluir los productos simples, y *only* informe sobre las versiones configurables. Esto se logra mediante la variable `Ordered products we count` conjunto de filtros, que filtra en la condición donde `parent_item_id` es `NULL`.

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|----|----|
| `base_price` | Precio de una unidad individual de un producto en el momento de la venta después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de que se apliquen impuestos, envíos o descuentos en el carro de compras, representados en la moneda base del almacén |
| `created_at` | Marca de fecha y hora de creación del elemento de pedido, normalmente almacenado localmente en UTC. Según la configuración de [!DNL MBI], esta marca de tiempo puede convertirse en una zona horaria de informes en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `order_id` | `Foreign key` asociado con la variable `sales_order` tabla. Unirse a `sales_order.entity_id` para determinar los atributos de pedido asociados al elemento de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Unirse a `sales_order_item.item_id` para determinar los atributos de producto principales asociados con un producto simple. Para los elementos de pedido principales (es decir, los tipos de producto empaquetables o configurables), la variable `parent_item_id` será `NULL` |
| `product_id` | `Foreign key` asociado con la variable `catalog_product_entity` tabla. Unirse a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados con el elemento de pedido |
| `product_type` | Tipo de producto vendido. Potencial [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluir: simple, configurable, agrupado, virtual, agrupado y descargable |
| `qty_ordered` | Cantidad de unidades incluidas en el carro de compras para el artículo de pedido en particular en el momento de la venta |
| `sku` | Identificador único del artículo de pedido comprado |
| `store_id` | `Foreign key` asociado con la variable `store` tabla. Unirse a `store.store_id` para determinar qué vista del almacén de comercio está asociada al artículo de pedido |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Customer's email` | Dirección de correo electrónico del cliente que realiza el pedido. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `customer_email` field |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `Customer's lifetime number of orders` field |
| `Customer's lifetime revenue` | Suma total de ingresos para todos los pedidos realizados por este cliente. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `Customer's lifetime revenue` field |
| `Customer's order number` | Clasificación de pedido secuencial para el pedido de este cliente. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `Customer's order number` field |
| `Order item total value (quantity * price)` | Valor total de un artículo de pedido en el momento de la venta después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Calculado multiplicando la variable `qty_ordered` por `base_price` |
| `Order's coupon_code` | Cupón aplicado al pedido. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `coupon_code` field |
| `Order's increment_id` | Identificador único del pedido. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `increment_id` field |
| `Order's status` | Estado del pedido. Calculado uniéndose `sales_order_item.order_id` a `sales_order.entity_id` y devolver el `status` field |
| `Store name` | Nombre del almacén de comercio asociado al artículo de pedido. Calculado uniéndose `sales_order_item.store_id` a `store.store_id` y devolver el `name` field |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Products ordered` | Cantidad total de productos incluidos en el carro de compras en el momento de la venta | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | El valor total de los productos incluidos en el carro de compras en el momento de la venta después de aplicar las reglas de precios del catálogo, descuentos por niveles y precios especiales y antes de aplicar cualquier impuesto, envío o descuento en el carro de compras | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` Unión de rutas

`catalog_product_entity`

* Unirse a `catalog_product_entity` para crear nuevas columnas que devuelvan atributos de producto asociados con el elemento de pedido.
   * Ruta: `sales_order_item.product_id` (muchos) => `catalog_product_entity.entity_id` (1)

`sales_order`

* Unirse a `sales_order` para crear nuevas columnas de nivel de pedido asociadas al elemento de pedido.
   * Ruta: `sales_order_item.order_id` (muchos) => `sales_order.entity_id` (1)

`sales_order_item`

* Unirse a `sales_order_item` para crear nuevas columnas que asocien detalles del SKU principal configurable o del paquete con el producto simple. Tenga en cuenta que deberá [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md) para obtener ayuda sobre la configuración de estos cálculos, si se crea en el administrador de Datas Warehouse.
   * Ruta: `sales_order_item.parent_item_id` (muchos) => `sales_order_item.item_id` (1)

`store`

* Unirse a `store` para crear nuevas columnas que devuelvan detalles relacionados con el almacén de comercio asociado al elemento de pedido.
   * Ruta: `sales_order_item.store_id` (muchos) => `store.store_id` (1)
