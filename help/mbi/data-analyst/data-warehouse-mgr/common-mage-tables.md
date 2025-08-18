---
title: Tablas comunes de Commerce
description: Obtenga información acerca de algunas de las tablas más comunes que usan  [!DNL Commerce Intelligence] clientes.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Tablas comunes de Commerce

Cuando conecta por primera vez una instancia de [!DNL Adobe Commerce] a [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] replica automáticamente los datos de algunas de sus tablas de comercio (normalmente entre 4 y 6 tablas) para configurar el conjunto inicial de paneles e informes. Aunque esto ofrece un buen punto de partida, la mayoría de las instancias de tienda generan decenas, si no cientos, de tablas adicionales que pueden proporcionar insight crítico en el rendimiento de su negocio.

A continuación se muestra una lista de algunas de las tablas más comunes que utilizan los clientes de [!DNL Commerce Intelligence]. Después de [conectar tu instancia de Commerce a Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), puedes usar [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear campos de datos relevantes.

| Nombre de tabla | Descripción |
|---|---|
| `catalog_category_entity` | Cada fila de la tabla `catalog_category_entity` describe una categoría específica. Con la tabla `catalog_category_entity_varchar` asociada y la tabla de asignación `catalog_category_product`, puede obtener información de categoría para cada producto. |
| `catalog_category_product` | Cada fila de la tabla `catalog_category_product` enumera una combinación de un producto y una categoría. Por lo tanto, un producto determinado puede existir en esta tabla varias veces con diferentes categorías y una categoría determinada puede existir en esta tabla varias veces asociada con diferentes productos. Esta tabla indexa la tabla `catalog_category_entity` (que contiene detalles de nivel de categoría) y la tabla `catalog_product_entity` (que contiene detalles de nivel de producto). |
| `catalog_product_entity` | Cada fila de la tabla `catalog_product_entity` representa un producto específico. Esto incluye cuándo se creó ese producto en su cuenta de Commerce y su SKU. |
| `customer_entity` | Cada fila de la tabla [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) representa un usuario registrado en el sitio web. Los detalles básicos a nivel de cliente, como su fecha de registro y dirección de correo electrónico, están activos en esta tabla. |
| `quote` | Cada fila de la tabla [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representa un carro de compras que se creó durante el proceso de cierre de compra, independientemente de si ese carro de compras se convirtió finalmente en un pedido. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días. |
| `quote_item` | Cada fila de la tabla [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representa un elemento agregado a un carro de compras, independientemente de si el carro de compras se convirtió finalmente en un pedido. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días. |
| `sales_order` | Cada fila de la tabla [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representa un pedido realizado en el sitio. Esta tabla contiene información a nivel de pedido, como la fecha del pedido, el cliente que lo ha realizado, el total del pedido y el uso del código de descuento y cupón. |
| `sales_order_address` | Cada fila de la tabla `sales_order_address` contiene información de envío y facturación para un pedido específico. En la tabla `sales_order`, `billing_address_id` y `shipping_address_id` para un orden determinado hacen referencia a una fila específica (identificada por `entity_id`) en la tabla `sales_order_address`. |
| `sales_order_item` | Cada fila de la tabla [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifica un elemento específico de un orden específico. Cada fila contiene detalles como el producto, la cantidad comprada y el pedido con el que está asociado el artículo determinado. |

{style="table-layout:auto"}

## Documentación relacionada

[Diagramas de relación de entidad](../data-warehouse-mgr/entity-rel-diag.md)
