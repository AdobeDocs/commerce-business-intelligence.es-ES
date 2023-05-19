---
title: tabla quote_item
description: Aprenda a trabajar con la tabla quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Tabla quote_item

El `quote_item` tabla (`sales_flat_quote_item` en M1) contiene registros de todos los artículos agregados a un carro de compras, independientemente de si se abandonó o se convirtió en una compra. Cada fila representa un elemento del carro de compras. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días.

>[!NOTE]
>
>El análisis de carros de compras abandonados históricos solo es posible si no elimina registros del `quote` y `quote_item` tabla. Si elimina registros, solo podrá ver los carros que aún no se han eliminado de la base de datos.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_price` | Precio de una unidad individual de un producto en el momento en que se agregó el artículo a un carro de compras, después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Se representa en la moneda base de la tienda. |
| `created_at` | Marca de tiempo de creación del elemento del carro de compras, almacenada localmente en UTC. Según la configuración en [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir en una zona horaria de informe en [!DNL Commerce Intelligence] que difiere de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Unirse a `quote_item.item_id` para determinar los atributos de producto principales asociados a un producto simple. Para los elementos de carro de compras principales (es decir, paquetes o tipos de productos configurables), la variable `parent_item_id` es `NULL` |
| `product_id` | `Foreign key` asociado con el `catalog_product_entity` tabla. Unirse a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados al artículo de pedido |
| `product_type` | Tipo de producto que se agregó al carro de compras. potencial [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluir: simple, configurable, agrupado, virtual, paquete y descargable |
| `qty` | Cantidad de unidades incluidas en el carro de compras para el artículo de carro en particular |
| `quote_id` | `Foreign key` asociado con el `quote` tabla. Unirse a `quote.entity_id` para determinar los atributos de carro asociados al artículo de carro de compras |
| `sku` | Identificador único del elemento del carro de compras |
| `store_id` | Clave externa asociada con el `store` tabla. Unirse a `store.store_id` para determinar qué vista de la tienda de comercio está asociada con el elemento del carro de compras |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Cart creation date` | Marca de tiempo asociada con la fecha de creación del carro de compras. Calculado al unirse `quote_item.quote_id` hasta `quote.entity_id` y devolviendo el `created_at` timestamp |
| `Cart is active? (1/0)` | Campo booleano que devuelve &quot;1&quot; si el carro fue creado por un cliente y aún no se ha convertido en un pedido. Devuelve &quot;0&quot; para carros de compras convertidos o creados mediante el administrador. Calculado al unirse `quote_item.quote_id` hasta `quote.entity_id` y devolviendo el `is_active` campo |
| `Cart item total value (qty * base_price)` | Valor total de un elemento en el momento en que se agregó el elemento a un carro, después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Se calcula multiplicando el `qty` por el `base_price` |
| `Seconds since cart creation` | Tiempo transcurrido entre la fecha de creación del carro de compras y el momento actual. Calculado al unirse `quote_item.quote_id` hasta `quote.entity_id` y devolviendo el `Seconds since cart creation` campo |
| `Store name` | Nombre de la tienda de Commerce asociada con el artículo de pedido. Calculado al unirse `sales_order_item.store_id` hasta `store.store_id` y devolviendo el `name` campo |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of abandoned cart items` | Cantidad total de artículos agregados a carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual un carro de compras se considera abandonado |
| `Abandoned cart item value` | Suma de los ingresos totales asociados con los carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual un carro de compras se considera abandonado |

{style="table-layout:auto"}

## Rutas de unión de clave externa

`catalog_product_entity`

* Unirse a `catalog_product_entity` para crear columnas que devuelvan atributos de producto asociados al artículo del carro de compras.
   * Ruta: `quote_item.product_id` (muchos) => `catalog_product_entity.entity_id` (uno)

`quote`

* Unirse a `quote` tabla para crear nuevas columnas de nivel de carro de compras asociadas al elemento de carro de compras.
   * Ruta: `quote_item.quote_id` (muchos) => `quote.entity_id` (uno)

`quote_item`

* Unirse a `quote_item` para crear columnas que asocien detalles del SKU configurable o del paquete principal con el producto simple. [Atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para obtener ayuda sobre la configuración de estos cálculos, si está compilando en el administrador de Datas Warehouse.
   * Ruta: `quote_item.parent_item_id` (muchos) => `quote_item.item_id` (uno)

`store`

* Unirse a `store` para crear columnas que devuelvan detalles relacionados con el almacén de comercio asociado al elemento del carro de compras.
   * Ruta: `quote_item.store_id` (muchos) => `store.store_id` (uno)
