---
title: Tablas de comercio comunes
description: Obtenga información acerca de algunas de las tablas más comunes que [!DNL MBI] Los clientes de utilizan.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Tablas de comercio comunes

La primera vez que conecte una instancia de Commerce a [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] replica automáticamente los datos de algunas de las tablas de comercio (normalmente entre 4 y 6 tablas) para configurar el conjunto inicial de paneles e informes. Aunque esto ofrece un punto de partida bueno, la mayoría de las instancias de tienda generan decenas, si no centenares, de tablas adicionales que pueden proporcionar una perspectiva crítica del rendimiento de su negocio.

A continuación se muestra una lista de algunas de las tablas más comunes que [!DNL MBI] Los clientes de utilizan. Después de usted [conectar su instancia de Commerce a MBI](../../data-analyst/importing-data/integrations/magento.md), puede utilizar el [Administrador de Datas Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar un seguimiento de los campos de datos relevantes.

| Nombre de tabla | Descripción |
|---|---|
| `catalog_category_entity` | Cada fila de la `catalog_category_entity` La tabla describe una categoría específica. Con el asociado `catalog_category_entity_varchar` y la `catalog_category_product` tabla de asignación, puede obtener información de categoría para cada producto. |
| `catalog_category_product` | Cada fila de la `catalog_category_product` La tabla enumera una combinación de un producto y una categoría. Por lo tanto, un producto determinado puede existir en esta tabla varias veces con diferentes categorías y una categoría determinada puede existir en esta tabla varias veces asociada con diferentes productos. Esta tabla indexa el `catalog_category_entity` (que contiene detalles de nivel de categoría) y la `catalog_product_entity` (que contiene detalles de nivel de producto). |
| `catalog_product_entity` | Cada fila de la `catalog_product_entity` representa un producto específico. Esto incluye cuándo se creó ese producto en su cuenta de Commerce y su SKU. |
| `customer_entity` | Cada fila de la [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) representa un usuario registrado en su sitio web. Los detalles básicos a nivel de cliente, como su fecha de registro y dirección de correo electrónico, están activos en esta tabla. |
| `quote` | Cada fila de la [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representa un carro de compras que se creó en el proceso de cierre de compra, independientemente de si ese carro de compras se convirtió finalmente en un pedido. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días. |
| `quote_item` | Cada fila de la [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representa un elemento añadido a un carro de compras, independientemente de si el carro de compras se convirtió finalmente en un pedido. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días. |
| `sales_order` | Cada fila de la [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representa un pedido realizado en su sitio. Esta tabla contiene información a nivel de pedido, como la fecha del pedido, el cliente que lo ha realizado, el total del pedido y el uso del código de descuento y cupón. |
| `sales_order_address` | Cada fila de la `sales_order_address` La tabla contiene información de envío y facturación de un pedido específico. En el `sales_order` , la `billing_address_id` y el `shipping_address_id` para un orden determinado, consulte una fila específica (identificada por `entity_id`) en el `sales_order_address` tabla. |
| `sales_order_item` | Cada fila de la [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifica un artículo específico de un pedido específico. Cada fila contiene detalles como el producto, la cantidad comprada y el pedido con el que está asociado el artículo determinado. |

{style="table-layout:auto"}

## Documentación relacionada

[Diagramas de relación de entidad](../data-warehouse-mgr/entity-rel-diag.md)
