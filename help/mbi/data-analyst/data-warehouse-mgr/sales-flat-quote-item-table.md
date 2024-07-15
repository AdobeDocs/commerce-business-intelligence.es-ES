---
title: tabla quote_item
description: Aprenda a trabajar con la tabla quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Tabla quote_item

La tabla `quote_item` (`sales_flat_quote_item` en M1) contiene registros de todos los elementos agregados a un carro de compras, independientemente de si el carro se abandonó o se convirtió en una compra. Cada fila representa un elemento del carro de compras. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días.

>[!NOTE]
>
>El análisis de carros de compras abandonados históricos sólo es posible si no se eliminan registros de las tablas `quote` y `quote_item`. Si elimina registros, solo podrá ver los carros que aún no se han eliminado de la base de datos.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_price` | Precio de una unidad individual de un producto en el momento en que el artículo se agregó al carro de compras, después de aplicar [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html), y antes de aplicar impuestos, envíos o descuentos del carro de compras. Se representa en la moneda base de la tienda. |
| `created_at` | Marca de tiempo de creación del elemento del carro de compras, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Únase a `quote_item.item_id` para determinar los atributos de producto principales asociados con un producto simple. Para los elementos del carro de compras principal (es decir, paquetes o tipos de productos configurables), `parent_item_id` es `NULL` |
| `product_id` | `Foreign key` se asoció con la tabla `catalog_product_entity`. Únase a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados con el elemento de pedido |
| `product_type` | Tipo de producto que se agregó al carro de compras. Los [tipos de productos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) potenciales incluyen: simple, configurable, agrupado, virtual, paquete y descargable |
| `qty` | Cantidad de unidades incluidas en el carro de compras para el artículo de carro en particular |
| `quote_id` | `Foreign key` se asoció con la tabla `quote`. Únase a `quote.entity_id` para determinar los atributos del carro asociados con el elemento del carro de compras |
| `sku` | Identificador único del elemento del carro de compras |
| `store_id` | Clave externa asociada con la tabla `store`. Únase a `store.store_id` para determinar qué vista de la tienda Commerce está asociada con el elemento del carro de compras |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Cart creation date` | Marca de tiempo asociada con la fecha de creación del carro de compras. Se calcula uniendo `quote_item.quote_id` a `quote.entity_id` y devolviendo la marca de tiempo `created_at` |
| `Cart is active? (1/0)` | Campo booleano que devuelve &quot;1&quot; si el carro fue creado por un cliente y aún no se ha convertido en un pedido. Devuelve &quot;0&quot; para carros de compras convertidos o creados mediante el administrador. Se calcula uniendo `quote_item.quote_id` a `quote.entity_id` y devolviendo el campo `is_active` |
| `Cart item total value (qty * base_price)` | Valor total de un elemento en el momento en que se agregó el elemento al carro de compras, después de aplicar [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) y antes de aplicar impuestos, envíos o descuentos del carro de compras. Calculado multiplicando `qty` por `base_price` |
| `Seconds since cart creation` | Tiempo transcurrido entre la fecha de creación del carro de compras y el momento actual. Se calcula uniendo `quote_item.quote_id` a `quote.entity_id` y devolviendo el campo `Seconds since cart creation` |
| `Store name` | Nombre del almacén de Commerce asociado al artículo de pedido. Se calcula uniendo `sales_order_item.store_id` a `store.store_id` y devolviendo el campo `name` |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of abandoned cart items` | Cantidad total de artículos agregados a carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro más allá del cual se considera abandonado |
| `Abandoned cart item value` | Suma de los ingresos totales asociados con los carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro más allá del cual se considera abandonado |

{style="table-layout:auto"}

## Rutas de unión de clave externa

`catalog_product_entity`

* Únase a la tabla `catalog_product_entity` para crear columnas que devuelvan atributos de producto asociados con el elemento del carro de compras.
   * Ruta de acceso: `quote_item.product_id` (varios) => `catalog_product_entity.entity_id` (uno)

`quote`

* Únase a la tabla `quote` para crear nuevas columnas de nivel de carro de compras asociadas al elemento de carro de compras.
   * Ruta de acceso: `quote_item.quote_id` (varios) => `quote.entity_id` (uno)

`quote_item`

* Únase a `quote_item` para crear columnas que asocien detalles del SKU principal configurable o del paquete con el producto simple. [Póngase en contacto con soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obtener ayuda con la configuración de estos cálculos, si está generando en el administrador de Datas Warehouse.
   * Ruta de acceso: `quote_item.parent_item_id` (varios) => `quote_item.item_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén de Commerce asociado al elemento del carro de compras.
   * Ruta de acceso: `quote_item.store_id` (varios) => `store.store_id` (uno)
