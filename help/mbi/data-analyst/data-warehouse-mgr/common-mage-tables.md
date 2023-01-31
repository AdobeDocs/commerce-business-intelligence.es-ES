---
title: Tablas de comercio común
description: Obtenga información sobre algunas de las tablas más comunes que [!DNL MBI] los clientes utilizan .
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Tablas de comercio común

La primera vez que conecta una instancia de Commerce a [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] duplica automáticamente los datos de algunas de las tablas de comercio (normalmente de 4 a 6 tablas) para configurar el conjunto inicial de tableros e informes. Aunque esto ofrece un bueno punto de partida, la mayoría de las instancias de almacenamiento generan decenas, si no cientos, de tablas adicionales que pueden proporcionar una perspectiva crítica del rendimiento de su negocio.

A continuación se muestra una lista de algunas de las tablas más comunes que [!DNL MBI] los clientes utilizan . Tras [conectar la instancia de Commerce a MBI](../../data-analyst/importing-data/integrations/magento.md), puede usar la variable [Administrador de Datas Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar el seguimiento de los campos de datos relevantes.

| Nombre de tabla | Descripción |
|---|---|
| `catalog_category_entity` | Cada fila de la `catalog_category_entity` describe una categoría específica. Con el `catalog_category_entity_varchar` y `catalog_category_product` tabla de asignación, puede obtener información de categoría para cada producto. |
| `catalog_category_product` | Cada fila de la `catalog_category_product` en la tabla se muestra una combinación de un producto y una categoría. Por lo tanto, un producto dado puede existir en esta tabla varias veces con diferentes categorías, y una categoría determinada puede existir en esta tabla varias veces asociada con diferentes productos. Esta tabla indexa el `catalog_category_entity` (que contiene detalles de nivel de categoría) y la variable `catalog_product_entity` (que contiene detalles a nivel de producto). |
| `catalog_product_entity` | Cada fila de la `catalog_product_entity` representa un producto específico. Esto incluye cuándo se creó ese producto en su cuenta de comercio y su SKU. |
| `customer_entity` | Cada fila de la [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) representa a un usuario registrado en su sitio web. Los detalles básicos a nivel de cliente, como la fecha de registro y la dirección de correo electrónico, están activos en esta tabla. |
| `quote` | Cada fila de la [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representa un carro que se creó en el proceso de cierre de compra, independientemente de si el carro de compras se convirtió o no en un pedido. Debido al tamaño potencial de esta tabla, le recomendamos que elimine registros periódicamente si se cumplen ciertos criterios, como si hay algún carro de compras no convertido de más de 60 días. |
| `quote_item` | Cada fila de la [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representa un elemento agregado a un carro de compras, independientemente de si el carro de compras finalmente se convirtió en un pedido o no. Debido al tamaño potencial de esta tabla, le recomendamos que elimine registros periódicamente si se cumplen ciertos criterios, como si hay algún carro de compras no convertido de más de 60 días. |
| `sales_order` | Cada fila de la [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representa un pedido colocado en el sitio. Esta tabla contiene información de nivel de pedido como la fecha del pedido, el cliente que realizó el pedido, el total del pedido y el uso del código de descuento y cupón. |
| `sales_order_address` | Cada fila del `sales_order_address` contiene información de envío y facturación de un pedido específico. En el `sales_order` la tabla `billing_address_id` y `shipping_address_id` para un pedido determinado, consulte una fila específica (identificada por `entity_id`) en el `sales_order_address` tabla. |
| `sales_order_item` | Cada fila de la [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifica un elemento específico de un orden específico. Cada fila contiene detalles como el producto, la cantidad comprada y el pedido con el que está asociado el artículo dado. |

{style=&quot;table-layout:auto&quot;}

## Documentación relacionada

[[!DNL Magento] Diagramas de relación de entidades](../data-warehouse-mgr/entity-rel-diag.md)
