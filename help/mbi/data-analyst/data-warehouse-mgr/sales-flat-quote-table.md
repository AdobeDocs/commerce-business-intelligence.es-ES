---
title: Tabla de presupuesto
description: Aprenda a trabajar con la tabla de presupuestos.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/Q-46fusr2IS4ZQDrR8IjHEttueSBpT2-LQBtsejMEC4
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 612
ht-degree: 0%

---

# Tabla de presupuesto

La tabla `quote` (`sales_flat_quote` en M1) contiene registros en cada carro de compras creado en su tienda, ya sea que se hayan abandonado o convertido en una compra. Cada fila representa un carro de compras. Debido al tamaño potencial de esta tabla, Adobe recomienda eliminar registros periódicamente si se cumplen determinados criterios, como si hay carros de compras sin convertir con más de 60 días.

>[!NOTE]
>
>El análisis de carros de compras abandonados históricos sólo es posible si no se eliminan registros de la tabla `quote`. Si elimina registros, solo podrá ver los carros que aún no se han eliminado de la base de datos.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_currency_code` | Moneda de todos los valores capturados en `base_*` campos (es decir `base_grand_total`, `base_subtotal`, etc.). Esto generalmente refleja la moneda predeterminada de la tienda Commerce |
| `base_grand_total` | Precio final cotizado al cliente para el carro de compras, después de aplicar todos los impuestos, envíos y descuentos. Aunque el cálculo preciso se puede personalizar, en general `base_grand_total` se calcula como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de mercancía de todos los artículos incluidos en el carro de compras. No se incluyen impuestos, gastos de envío, descuentos, etc |
| `created_at` | Marca de tiempo de creación del carro de compras, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos |
| `customer_email` | Dirección de correo electrónico del cliente que creó el carro |
| `customer_id` | `Foreign key` está asociado con la tabla `customer_entity`, si el cliente está registrado. Únase a `customer_entity.entity_id` para determinar los atributos del cliente asociados con el usuario que creó el carro de compras. Si el carro se creó mediante el cierre de compra de invitado, este campo es `NULL` |
| `entity_id` (PK) | Identificador único de la tabla y que se utiliza comúnmente en combinaciones con otras tablas dentro de la instancia de Commerce |
| `is_active` | Campo booleano que devuelve &quot;1&quot; si el carro fue creado por un cliente y aún no se ha convertido en un pedido. Devuelve &quot;0&quot; para carros de compras convertidos o creados mediante el administrador |
| `items_qty` | Suma de la cantidad total de todos los artículos incluidos en el carro de compras |
| `reserved_order_id` | `Foreign key` se asoció con la tabla `sales_order`. Únase a `sales_order.increment_id` para determinar los detalles de pedido asociados con un carro de compras convertido. Para los carros de compras que no están asociados con un pedido convertido, `reserved_order_id` permanece como `NULL` |
| `store_id` | `Foreign key` se asoció con la tabla `store`. Unirse a `store`.`store_id` para determinar qué vista de la tienda Commerce está asociada al carro de compras |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Order date` | Marca de tiempo que refleja la fecha de creación del pedido para carros de compras convertidos. Se calcula uniendo `quote.reserved_order_id` a `sales_order.increment_id` y devolviendo el campo `sales_order.created_at` |
| `Seconds between cart creation and order` | Tiempo transcurrido entre la creación del carro y la creación del pedido. Calculado restando `created_at` de `Order date`, devuelto como un número entero de segundos |
| `Seconds since cart creation` | Tiempo transcurrido entre la fecha de creación del carro de compras y el momento actual. Se calcula restando `created_at` de la marca de tiempo del servidor en el momento en que se ejecuta la consulta, devuelto como un número entero de segundos. Normalmente se utiliza para identificar la edad de un carro de compras |
| `Store name` | El nombre de la tienda de Commerce asociada con este pedido. Se calcula uniendo `quote.store_id` a `store.store_id` y devolviendo el campo `name` |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of abandoned carts` | El recuento de carros de compras que cumplen las condiciones específicas de &quot;abandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtros:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro más allá del cual se considera abandonado |
| `Avg time to cart conversion` | Tiempo promedio entre la creación del carro de compras y la creación del pedido para los carros de compras convertidos | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | Suma del total de ingresos potenciales del carro de compras abandonado, donde los ingresos se definen como el campo `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtros:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual se considera abandonado |

{style="table-layout:auto"}

## Rutas de unión de clave externa

`customer_entity`

* Únase a la tabla `customer_entity` para crear nuevas columnas de nivel de cliente asociadas con el cliente que creó el carro de compras.
   * Ruta de acceso: `quote.customer_id` (varios) => `customer_entity.entity_id` (uno)

`sales_order`

* Únase a la tabla `sales_order` para crear columnas que devuelvan detalles de pedido asociados con un carro de compras convertido.
   * Ruta de acceso: `quote.reserved_order_id` (varios) => `sales_order.increment_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén de Commerce asociado al carro de compras.
   * Ruta de acceso: `quote.store_id` (varios) => `store.store_id` (uno)
