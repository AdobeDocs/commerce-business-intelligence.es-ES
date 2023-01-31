---
title: tabla de comillas
description: Aprenda a trabajar con la tabla de comillas.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Tabla de comillas

La variable `quote` tabla (`sales_flat_quote` en M1) contiene registros de cada carro de compras creado en su tienda, independientemente de si se abandonaron o se convirtieron en una compra. Cada fila representa un carro de compras. Debido al tamaño potencial de esta tabla, le recomendamos que elimine registros periódicamente si se cumplen ciertos criterios, como si hay algún carro de compras no convertido de más de 60 días.

>[!NOTE]
>
>El análisis de los carros de compras abandonados históricos solo es posible si no se eliminan registros del `quote` tabla. Si elimina registros, solo podrá ver los carros que aún no se hayan eliminado de la base de datos.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_currency_code` | Moneda para todos los valores capturados en `base_*` campos (es `base_grand_total`, `base_subtotal`, etc.). Esto suele reflejar la moneda predeterminada del almacén de comercio |
| `base_grand_total` | Precio final cotizado al cliente para el carro de compras, después de aplicar todos los impuestos, envíos y descuentos. Aunque el cálculo preciso es personalizable, en general la variable `base_grand_total` se calcula como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de la mercancía de todos los artículos incluidos en el carro de compras. Impuestos, envíos, descuentos, etc. no están incluidos |
| `created_at` | Marca de fecha y hora de creación del carro de compras, generalmente almacenada localmente en UTC. Según la configuración de [!DNL MBI], esta marca de tiempo puede convertirse en una zona horaria de informes en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `customer_email` | Dirección de correo electrónico del cliente que creó el carro de compras |
| `customer_id` | `Foreign key` asociado con la variable `customer_entity` , si el cliente está registrado. Unirse a `customer_entity.entity_id` para determinar los atributos del cliente asociados al usuario que creó el carro de compras. Si el carro de compras se creó mediante el cierre de compra de invitado, este campo se `NULL` |
| `entity_id` (PK) | Identificador único de la tabla y que normalmente se utiliza en las combinaciones con otras tablas dentro de la instancia de comercio |
| `is_active` | Campo booleano que devuelve &quot;1&quot; si el carro de compras fue creado por un cliente y aún no se ha convertido en un pedido. Devuelve &quot;0&quot; para los carros convertidos o los carros creados a través del administrador |
| `items_qty` | Suma de la cantidad total de todos los artículos incluidos en el carro de compras |
| `reserved_order_id` | `Foreign key` asociado con la variable `sales_order` tabla. Unirse a `sales_order.increment_id` para determinar los detalles de pedido asociados a un carro de compras convertido. Para los carros de compras que no están asociados a un pedido convertido, la variable `reserved_order_id` permanecerá `NULL` |
| `store_id` | `Foreign key` asociado con la variable `store` tabla. Unirse a `store`.`store_id` para determinar qué vista del almacén de comercio está asociada al carro de compras |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Order date` | Marca de tiempo que refleja la fecha de creación del pedido para los carros convertidos. Calculado uniéndose `quote.reserved_order_id` a `sales_order.increment_id` y devolver el `sales_order.created_at` field |
| `Seconds between cart creation and order` | Tiempo transcurrido entre la creación del carro de compras y la creación de pedidos. Calculado restando `created_at` from `Order date`, devuelto como un número entero de segundos |
| `Seconds since cart creation` | Tiempo transcurrido entre la fecha de creación del carro de compras y ahora. Calculado restando `created_at` desde la marca de tiempo del servidor en el momento en que se ejecuta la consulta, devuelta como un número entero de segundos. Se utiliza con mayor frecuencia para identificar la edad de un carro de compras |
| `Store name` | Nombre del almacén de comercio asociado a este pedido. Calculado uniéndose `quote.store_id` a `store.store_id` y devolver el `name` field |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of abandoned carts` | Recuento de carros que cumplen condiciones específicas de &quot;abandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtros:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual se considera abandonado el carro de compras |
| `Avg time to cart conversion` | El tiempo promedio entre la creación del carro de compras y la creación de pedidos para los carros convertidos | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | La suma del total de ingresos potenciales abandonados del carro de compras, donde los ingresos se definen como el `base_grand_total` field | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtros:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, donde &quot;x&quot; corresponde al tiempo transcurrido (en segundos) desde la creación del carro de compras más allá del cual se considera abandonado el carro de compras |

{style=&quot;table-layout:auto&quot;}

## Rutas de unión de clave externa

`customer_entity`

* Unirse a `customer_entity` para crear nuevas columnas de nivel de cliente asociadas al cliente que creó el carro de compras.
   * Ruta: `quote.customer_id` (muchos) => `customer_entity.entity_id` (1)

`sales_order`

* Unirse a `sales_order` para crear nuevas columnas que devuelvan detalles de pedidos asociados con un carro convertido.
   * Ruta:`quote.reserved_order_id` (muchos) => `sales_order.increment_id` (1)

`store`

* Unirse a `store` para crear nuevas columnas que devuelvan detalles relacionados con el almacén de comercio asociado al carro de compras.
   * Ruta: `quote.store_id` (muchos) => `store.store_id` (1)
