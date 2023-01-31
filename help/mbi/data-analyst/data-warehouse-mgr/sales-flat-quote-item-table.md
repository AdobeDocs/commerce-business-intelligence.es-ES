---
title: tabla comillas_elementos
description: Aprenda a trabajar con la tabla de elementos de comillas.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# Tabla de comillas_elementos

La variable `quote_item` tabla (`sales_flat_quote_item` en [!DNL Magento] 1) contiene registros de cada artículo agregado a un carro de compras, ya sea que el carro de compras se haya abandonado o se haya convertido en una compra. Cada fila representa un artículo del carro de compras. Debido al tamaño potencial de esta tabla, le recomendamos que elimine registros periódicamente si se cumplen ciertos criterios, como si hay algún carro de compras no convertido de más de 60 días.

>[!NOTE]
>
>El análisis de los carros de compras abandonados históricos solo es posible si no se eliminan registros del `quote` y `quote_item` tabla. Si elimina registros, solo podrá ver los carros que aún no se hayan eliminado de la base de datos.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_price` | Precio de una unidad individual de un producto en el momento en que se agregó el artículo a un carro de compras, después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) se aplican y antes de que se apliquen impuestos, envíos o descuentos en el carro de compras, representados en la moneda base del almacén |
| `created_at` | Marca de fecha y hora de creación del artículo del carro de compras, generalmente almacenado localmente en UTC. Según la configuración de [!DNL MBI], esta marca de tiempo puede convertirse en una zona horaria de informes en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `item_id` (PK) | Identificador único de la tabla |
| `name` | Nombre de texto del elemento de pedido |
| `parent_item_id` | `Foreign key` que relaciona un producto simple con su paquete principal o producto configurable. Unirse a `quote_item.item_id` para determinar los atributos de producto principales asociados con un producto simple. Para los elementos del carro principal (es decir, los tipos de producto empaquetables o configurables), la variable `parent_item_id` será `NULL` |
| `product_id` | `Foreign key` asociado con la variable `catalog_product_entity` tabla. Unirse a `catalog_product_entity.entity_id` para determinar los atributos de producto asociados con el elemento de pedido |
| `product_type` | Tipo de producto que se agregó al carro de compras. Potencial [tipos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) incluir: simple, configurable, agrupado, virtual, agrupado y descargable |
| `qty` | Cantidad de unidades incluidas en el carro de compras para el artículo del carro de compras en particular |
| `quote_id` | `Foreign key` asociado con la variable `quote` tabla. Unirse a `quote.entity_id` para determinar los atributos del carro de compras asociados con el artículo del carro de compras |
| `sku` | Identificador único del artículo del carro de compras |
| `store_id` | Clave externa asociada con la variable `store` tabla. Unirse a `store.store_id` para determinar qué vista del almacén de comercio está asociada al artículo del carro de compras |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Cart creation date` | Marca de tiempo asociada a la fecha de creación del carro de compras. Calculado uniéndose `quote_item.quote_id` a `quote.entity_id` y devolver el `created_at` timestamp |
| `Cart is active? (1/0)` | Campo booleano que devuelve &quot;1&quot; si el carro de compras fue creado por un cliente y aún no se ha convertido en un pedido. Devuelve &quot;0&quot; para los carros convertidos o los carros creados a través del administrador. Calculado uniéndose `quote_item.quote_id` a `quote.entity_id` y devolver el `is_active` field |
| `Cart item total value (qty * base_price)` | Valor total de un elemento en el momento en que se agregó el elemento a un carro de compras, después de [reglas de precios de catálogo, descuentos por niveles y precios especiales](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) y antes de aplicar impuestos, envíos o descuentos en el carro de compras. Calculado multiplicando la variable `qty` por `base_price` |
| `Seconds since cart creation` | Tiempo transcurrido entre la fecha de creación del carro de compras y ahora. Calculado uniéndose `quote_item.quote_id` a `quote.entity_id` y devolver el `Seconds since cart creation` field |
| `Store name` | Nombre del almacén de comercio asociado al artículo de pedido. Calculado uniéndose `sales_order_item.store_id` a `store.store_id` y devolver el `name` field |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of abandoned cart items` | Cantidad total de artículos añadidos al carro de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual se considera abandonado el carro de compras |
| `Abandoned cart item value` | Suma de los ingresos totales asociados con carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtros:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual se considera abandonado el carro de compras |

{style=&quot;table-layout:auto&quot;}

## Rutas de unión de clave externa

`catalog_product_entity`

* Unirse a `catalog_product_entity` para crear nuevas columnas que devuelvan atributos de producto asociados con el artículo del carro de compras.
   * Ruta: `quote_item.product_id` (muchos) => `catalog_product_entity.entity_id` (1)

`quote`

* Unirse a `quote` para crear nuevas columnas de nivel de carro de compras asociadas con el elemento del carro de compras.
   * Ruta: `quote_item.quote_id` (muchos) => `quote.entity_id` (1)

`quote_item`

* Unirse a `quote_item` para crear nuevas columnas que asocien detalles del SKU principal configurable o del paquete con el producto simple. Tenga en cuenta que deberá [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md) para obtener ayuda sobre la configuración de estos cálculos, si se crea en el administrador de Datas Warehouse.
   * Ruta: `quote_item.parent_item_id` (muchos) => `quote_item.item_id` (1)

`store`

* Unirse a `store` para crear nuevas columnas que devuelvan detalles relacionados con el almacén de comercio asociado al artículo del carro de compras.
   * Ruta: `quote_item.store_id` (muchos) => `store.store_id` (1)
