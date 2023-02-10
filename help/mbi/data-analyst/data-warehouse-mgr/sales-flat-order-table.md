---
title: tabla sales_order
description: Aprenda a trabajar con la tabla sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---

# `sales_order` Tabla

La variable `sales_order` tabla (`sales_flat_order` en M1) es donde se captura cada pedido. En la mayoría de los casos, cada fila representa un pedido único, aunque hay algunas implementaciones personalizadas de Comercio que resultan en dividir un pedido en filas independientes.

Esta tabla incluye todos los pedidos de los clientes, independientemente de si el pedido se procesó o no a través del cierre de compra de los clientes. Si la tienda acepta el cierre de compra para invitados, puede encontrar más información al respecto [caso de uso](../data-warehouse-mgr/guest-orders.md).

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_currency_code` | Moneda para todos los valores capturados en `base_*` campos (es `base_grand_total`, `base_subtotal`, etc.). Esto suele reflejar la moneda predeterminada del almacén de comercio |
| `base_discount_amount` | Valor de descuento aplicado al pedido |
| `base_grand_total` | Precio final pagado por el cliente en el pedido, después de aplicar todos los impuestos, envíos y descuentos. Aunque el cálculo preciso es personalizable, en general la variable `base_grand_total` se calcula como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de la mercancía de todos los artículos incluidos en el pedido. Impuestos, envíos, descuentos, etc. no están incluidos |
| `base_shipping_amount` | Valor de envío aplicado al pedido |
| `base_tax_amount` | Valor de impuesto aplicado al pedido |
| `billing_address_id` | `Foreign key` asociado con la variable `sales_order_address` tabla. Unirse a `sales_order_address.entity_id` para determinar los detalles de la dirección de facturación asociados al pedido |
| `coupon_code` | Cupón aplicado al pedido. Si no se aplica ningún cupón, este campo se `NULL` |
| `created_at` | Marca de fecha y hora de creación del pedido, generalmente almacenada localmente en UTC. Según la configuración de [!DNL MBI], esta marca de tiempo puede convertirse en una zona horaria de informes en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `customer_email` | Dirección de correo electrónico del cliente que realiza el pedido. Esto se rellenará en todas las situaciones, incluidos los pedidos procesados mediante el cierre de compra de un invitado |
| `customer_group_id` | Clave externa asociada con la variable `customer_group` tabla. Unirse a `customer_group.customer_group_id` para determinar el grupo de clientes asociado a la solicitud |
| `customer_id` | `Foreign key` asociado con la variable `customer_entity` , si el cliente está registrado. Unirse a `customer_entity.entity_id` para determinar los atributos del cliente asociados al pedido. Si el pedido se realizó a través del cierre de compra del invitado, este campo se `NULL` |
| `entity_id` (PK) | Identificador único de la tabla y que normalmente se utiliza en las combinaciones con otras tablas dentro de la instancia de comercio |
| `increment_id` | Identificador único de un pedido y denominado comúnmente como `order_id` en Adobe Commerce. La variable `increment_id` se utiliza con mayor frecuencia para conexiones a fuentes externas, como [!DNL Google Ecommerce] |
| `shipping_address_id` | Clave externa asociada con la variable `sales_order_address` tabla. Unirse a `sales_order_address.entity_id` para determinar los detalles de dirección de envío asociados con el pedido |
| `status` | Estado del pedido. Puede devolver valores como &quot;completo&quot;, &quot;procesado&quot;, &quot;cancelado&quot;, &quot;reembolsado&quot;, así como cualquier estado personalizado implementado en la instancia de Commerce. Sujeto a cambios a medida que se procesa el pedido |
| `store_id` | `Foreign key` asociado con la variable `store` tabla. Unirse a `store`.`store_id` para determinar qué vista del almacén de comercio está asociada al pedido |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Billing address city` | Ciudad de facturación para el pedido. Calculado uniéndose `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolver el `city` field |
| `Billing address country` | Código de país de facturación del pedido. Calculado uniéndose `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolver el `country_id` |
| `Billing address region` | Región de facturación (estado o provincia con mayor frecuencia) del pedido. Calculado uniéndose `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolver el `region` field |
| `Customer's first order date` | Marca de tiempo del primer pedido realizado por este cliente. A menudo se considera que es la &quot;fecha de adquisición&quot; de un cliente. Calculado devolviendo el mínimo `sales_order`.`created_at` valor para cada cliente único |
| `Customer's first order's billing region` | Región de facturación de adquisición para el cliente que realizó el pedido. Calculado devolviendo el valor `Billing address region` asociado con el primer pedido del cliente |
| `Customer's first order's coupon_code` | Código de cupón de adquisición para el cliente que realizó este pedido. Calculado devolviendo el valor `coupon_code` asociado con el primer pedido del cliente |
| `Customer's group code` | Nombre del grupo del cliente que realizó este pedido. Calculado uniéndose `sales_order`.`customer_group_id` a `customer_group`.`customer_group_id` y devolver el `customer_group_code` field |
| `Customer's lifetime number of coupons` | Cantidad total de cupones aplicados a todos los pedidos realizados por este cliente. Se calcula contando el número de pedidos en los que la variable `coupon_code` no es `NULL` para cada cliente único |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Calculado contando el número de filas del `sales_order` tabla para cada cliente único |
| `Customer's lifetime revenue` | Suma total de ingresos para todos los pedidos realizados por este cliente. Calculado sumando la variable `base_grand_total` campo para todos los pedidos de cada cliente único |
| `Customer's order number` | Clasificación de pedido secuencial para el pedido de este cliente. Se calcula identificando todos los pedidos realizados por un cliente, ordenándolos en orden ascendente según la variable `created_at` marca de tiempo y asignar un valor entero incremental a cada pedido. Por ejemplo, el primer pedido del cliente devuelve un `Customer's order number` de 1; su segundo orden devuelve un valor `Customer's order number` de 2; y así sucesivamente |
| `Customer's order number (previous-current)` | Clasificación del pedido anterior del cliente concatenado con la clasificación de este pedido, separada por una `-` carácter. Calculado concatenando (&quot;`Customer's order number` - 1&quot;) con &quot;`-`&quot; seguido de &quot;`Customer's order number`&quot;. Por ejemplo, para el pedido asociado con la segunda compra del cliente, esta columna devolverá un valor de `1-2`. Se utiliza con mayor frecuencia al representar el tiempo entre dos eventos de pedido (es decir, en el gráfico &quot;Tiempo entre pedidos&quot;) |
| `Is customer's last order?` | Determina si el pedido corresponde o no al último o más reciente pedido del cliente. Calculado comparando la variable `Customer's order number` valor con `Customer's lifetime number of orders`. Cuando estos dos campos son iguales para el orden dado, esta columna devuelve &quot;Yes&quot;; de lo contrario, devuelve &quot;No&quot;. |
| `Number of items in order` | Cantidad total de artículos incluidos en el pedido. Calculado uniéndose `sales_order`.`entity_id` a `sales_order_item`.`order_id` y resumen del `sales_order_item`.`qty_ordered` field |
| `Seconds between customer's first order date and this order` | Tiempo transcurrido entre este pedido y el primer pedido del cliente. Calculado restando `Customer's first order date` de la variable `created_at` para cada pedido, devuelto como un número entero de segundos |
| `Seconds since previous order` | Tiempo transcurrido entre este pedido y el pedido inmediatamente anterior del cliente. Calculado restando la variable `created_at` para el orden anterior del `created_at` de este orden, se devuelve como un número entero de segundos. Por ejemplo, para el registro de pedido correspondiente al tercer pedido de un cliente, esta columna devuelve el número de segundos entre el segundo pedido y el tercer pedido del cliente. Para el primer pedido del cliente, este campo devuelve `NULL` |
| `Shipping address city` | Ciudad de envío para el pedido. Calculado uniéndose `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` y devolver el `city` field |
| `Shipping address country` | Código de país de envío del pedido. Calculado uniéndose `sales_order`.`Shipping_address_id` a `sales_order_address`.`entity_id` y devolver el `country_id` |
| `Shipping address region` | Región de envío (generalmente estado o provincia) para el pedido. Calculado uniéndose `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` y devolver el `region` field |
| `Store name` | Nombre del almacén de comercio asociado a este pedido. Calculado uniéndose `sales_order`.`store_id` a `store`.`store_id` y devolver el `name` field |

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Avg order value` | El ingreso promedio por pedido, donde los ingresos se definen como la variable `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | El tiempo promedio entre el pedido de un cliente (n-1) y el nth order, para todos los clientes y pedidos | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | La suma del valor bruto de la mercancía para todos los pedidos, donde GMV se define como el subtotal, antes de aplicar todos los impuestos y descuentos | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | La mediana de tiempo entre el pedido de un cliente (n-1) y el nth order, para todos los clientes y pedidos | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Recuento total de pedidos realizados | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La suma de los ingresos para todos los pedidos, donde los ingresos se definen como el precio final pagado por el cliente, después de aplicar todos los impuestos, descuentos, envíos, etc. | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | La suma del importe de envío de todos los pedidos | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | La suma de los impuestos aplicados a todos los pedidos | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Número de clientes únicos que realizan un pedido en el intervalo de tiempo de informe dado. Por ejemplo, si el intervalo del informe era semanal, cada cliente que realice al menos un pedido en una semana determinada se contará exactamente una vez, independientemente de cuántos pedidos haya realizado en esa semana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Unión de rutas

`customer_entity`

* Unirse a `customer_entity` para crear nuevas columnas de nivel de cliente asociadas con el cliente que realizó el pedido.
   * Ruta: `sales_order.customer_id` (muchos) => `customer_entity.entity_id` (1)

`customer_group`

* Unirse a `customer_group` para crear nuevas columnas que devuelvan el nombre del grupo de clientes del cliente que realizó el pedido.
   * Ruta: `sales_order.customer_group_id` (muchos) => `customer_group.customer_group_id` (1)

`sales_order_address`

* Unirse a `sales_order_address` para crear nuevas columnas que devuelvan ubicaciones de facturación y envío asociadas al pedido. Se pueden unir dos rutas, dependiendo de si se requieren los detalles de facturación o envío.
   * Rutas:
      * Envío: `sales_order.shipping_address_id`(muchos) => `sales_order_address.entity_id` (1)
      * Facturación: `sales_order.billing_address_id`(muchos) => `sales_order_address.entity_id` (1)

`store`

* Unirse a `store` para crear nuevas columnas que devuelvan detalles relacionados con el almacén de comercio asociado al pedido.
   * Ruta: `sales_order.store_id` (muchos) => `store.store_id` (1)
