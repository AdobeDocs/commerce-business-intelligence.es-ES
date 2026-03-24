---
title: tabla quote_item
description: Aprenda a trabajar con la tabla quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/wLNm1g1L6-0Ded-bZT991KvJi3dVO6zA4i2qftiX2J0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 646
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
| `base_price` | Precio de una unidad individual de un producto en el momento en que el artículo se agregó al carro de compras, después de aplicar [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=es), y antes de aplicar impuestos, envíos o descuentos del carro de compras. Se representa en la moneda base de la tienda. |
| `created_at` | Marca de tiempo de creación del elemento del carro de compras, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Únase a `quote_item.item_id` para determinar los atributos de producto principales asociados con un producto simple. Para los elementos del carro de compras principal (es decir, paquetes o tipos de productos configurables), `parent_item_id` es `NULL` |
| `product_id` | `Foreign key` se asoció con la tabla `catalog_product_entity`. Únase a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados con el elemento de pedido |
| `product_type` | Tipo de producto que se agregó al carro de compras. Los [tipos de productos](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=es#product-types) potenciales incluyen: simple, configurable, agrupado, virtual, paquete y descargable |
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
| `Cart item total value (qty * base_price)` | Valor total de un elemento en el momento en que se agregó el elemento al carro de compras, después de aplicar [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=es) y antes de aplicar impuestos, envíos o descuentos del carro de compras. Calculado multiplicando `qty` por `base_price` |
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

* Únase a `quote_item` para crear columnas que asocien detalles del SKU principal configurable o del paquete con el producto simple. [Póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) para obtener ayuda con la configuración de estos cálculos, si está generando en el administrador de Data Warehouse.
   * Ruta de acceso: `quote_item.parent_item_id` (varios) => `quote_item.item_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén de Commerce asociado al elemento del carro de compras.
   * Ruta de acceso: `quote_item.store_id` (varios) => `store.store_id` (uno)
