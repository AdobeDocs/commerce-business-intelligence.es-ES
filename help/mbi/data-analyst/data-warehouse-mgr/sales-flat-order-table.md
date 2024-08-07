---
title: tabla sales_order
description: Aprenda a trabajar con la tabla sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Tabla `sales_order`

La tabla `sales_order` (`sales_flat_order` en M1) es donde se captura cada pedido. Normalmente, cada fila representa un orden único, aunque hay algunas implementaciones personalizadas de Commerce que resultan en la división de un orden en filas independientes.

Esta tabla incluye todos los pedidos de clientes, independientemente de si el pedido se procesó mediante el cierre de compra de invitado. Si tu tienda acepta el pago y envío de invitados, puedes encontrar más información sobre este [caso de uso](../data-warehouse-mgr/guest-orders.md).

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `base_currency_code` | Moneda de todos los valores capturados en `base_*` campos (es decir `base_grand_total`, `base_subtotal`, etc.). Esto generalmente refleja la moneda predeterminada de la tienda Commerce |
| `base_discount_amount` | Valor de descuento aplicado al pedido |
| `base_grand_total` | Precio final pagado por el cliente en el pedido, después de aplicar todos los impuestos, envíos y descuentos. Aunque el cálculo preciso se puede personalizar, en general `base_grand_total` se calcula como `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valor bruto de mercancía de todos los artículos incluidos en el pedido. No se incluyen impuestos, gastos de envío, descuentos, etc |
| `base_shipping_amount` | Valor de envío aplicado al pedido |
| `base_tax_amount` | Valor de impuesto aplicado al pedido |
| `billing_address_id` | `Foreign key` se asoció con la tabla `sales_order_address`. Únase a `sales_order_address.entity_id` para determinar los detalles de la dirección de facturación asociados con el pedido |
| `coupon_code` | Cupón aplicado al pedido. Si no se aplica ningún cupón, este campo es `NULL` |
| `created_at` | Marca de tiempo de creación del pedido, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos |
| `customer_email` | Dirección de correo electrónico del cliente que realiza el pedido. Esto se rellena en todas las situaciones, incluidos los pedidos procesados mediante el cierre de compra de invitado |
| `customer_group_id` | Clave externa asociada con la tabla `customer_group`. Únase a `customer_group.customer_group_id` para determinar el grupo de clientes asociado con el pedido |
| `customer_id` | `Foreign key` está asociado con la tabla `customer_entity`, si el cliente está registrado. Únase a `customer_entity.entity_id` para determinar los atributos del cliente asociados con el pedido. Si el pedido se realizó mediante el cierre de compra de invitado, este campo es `NULL` |
| `entity_id` (PK) | Identificador único de la tabla y que se utiliza comúnmente en combinaciones con otras tablas dentro de la instancia de Commerce |
| `increment_id` | Identificador único de un pedido y conocido comúnmente como `order_id` en Adobe Commerce. `increment_id` se utiliza con mayor frecuencia para las uniones a orígenes externos, como [!DNL Google Ecommerce] |
| `shipping_address_id` | Clave externa asociada con la tabla `sales_order_address`. Únase a `sales_order_address.entity_id` para determinar los detalles de la dirección de envío asociados con el pedido |
| `status` | Estado del pedido. Puede devolver valores como &quot;completado&quot;, &quot;procesamiento&quot;, &quot;cancelado&quot;, &quot;devuelto&quot; y cualquier estado personalizado implementado en la instancia de Commerce. Sujeto a cambios conforme se procesa el pedido |
| `store_id` | `Foreign key` se asoció con la tabla `store`. Unirse a `store`.`store_id` para determinar qué vista de la tienda Commerce está asociada con el pedido |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Billing address city` | Ciudad de facturación del pedido. Calculado uniéndose a `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolviendo el campo `city` |
| `Billing address country` | Código de país de facturación del pedido. Calculado uniéndose a `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolviendo `country_id` |
| `Billing address region` | Región de facturación (generalmente, estado o provincia) del pedido. Calculado uniéndose a `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` y devolviendo el campo `region` |
| `Customer's first order date` | Marca de tiempo del primer pedido realizado por este cliente. A menudo se considera la &quot;fecha de adquisición&quot; de un cliente. Calculado devolviendo el mínimo `sales_order`.Valor de `created_at` para cada cliente único |
| `Customer's first order's billing region` | Región de facturación de adquisición del cliente que realizó el pedido. Se calcula devolviendo el `Billing address region` asociado con el primer pedido del cliente |
| `Customer's first order's coupon_code` | Código de cupón de adquisición del cliente que realizó este pedido. Se calcula devolviendo el `coupon_code` asociado con el primer pedido del cliente |
| `Customer's group code` | Nombre del grupo del cliente que realizó este pedido. Calculado uniéndose a `sales_order`.`customer_group_id` a `customer_group`.`customer_group_id` y devolviendo el campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Cantidad total de cupones aplicados a todos los pedidos realizados por este cliente. Se calcula contando el número de pedidos donde `coupon_code` no es `NULL` para cada cliente único |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Se calcula contando el número de filas de la tabla `sales_order` para cada cliente único |
| `Customer's lifetime revenue` | Suma del total de ingresos de todos los pedidos realizados por este cliente. Se calcula sumando el campo `base_grand_total` para todos los pedidos de cada cliente único |
| `Customer's order number` | Clasificación de pedido secuencial para el pedido de este cliente. Se calcula identificando todos los pedidos realizados por un cliente, ordenándolos en orden ascendente por la marca de tiempo `created_at` y asignando un valor entero incremental a cada pedido. Por ejemplo, el primer pedido del cliente devuelve un `Customer's order number` de 1, el segundo pedido del cliente devuelve un `Customer's order number` de 2, etc. |
| `Customer's order number (previous-current)` | Clasificación del pedido anterior del cliente concatenado con la clasificación de este pedido, separado por un carácter `-`. Se calcula concatenando (&quot;`Customer's order number` - 1&quot;) con &quot;`-`&quot; seguido de &quot;`Customer's order number`&quot;. Por ejemplo, para el pedido asociado con la segunda compra del cliente, esta columna devuelve un valor de `1-2`. Normalmente se utiliza al representar el tiempo entre dos eventos de pedido (es decir, en el gráfico &quot;Tiempo entre pedidos&quot;) |
| `Is customer's last order?` | Determina si el pedido corresponde al último pedido del cliente o al más reciente. Se calcula comparando el valor `Customer's order number` con `Customer's lifetime number of orders`. Cuando estos dos campos son iguales para el orden determinado, esta columna devuelve `Yes`; de lo contrario, devuelve `No` |
| `Number of items in order` | Cantidad total de artículos incluidos en el pedido. Calculado uniéndose a `sales_order`.`entity_id` a `sales_order_item`.`order_id` y sumando `sales_order_item`.`qty_ordered` campo |
| `Seconds between customer's first order date and this order` | Tiempo transcurrido entre este pedido y el primer pedido del cliente. Se calcula restando `Customer's first order date` de `created_at` para cada pedido devuelto como un número entero de segundos |
| `Seconds since previous order` | Tiempo transcurrido entre este pedido y el pedido inmediatamente anterior del cliente. Se calcula restando el `created_at` del pedido anterior del `created_at` de este pedido, devuelto como un número entero de segundos. Por ejemplo, para el registro de pedido correspondiente al tercer pedido de un cliente, esta columna devuelve el número de segundos entre el segundo y el tercer pedido del cliente. Para el primer pedido del cliente, este campo devuelve `NULL` |
| `Shipping address city` | Ciudad de envío del pedido. Calculado uniéndose a `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` y devolviendo el campo `city` |
| `Shipping address country` | Código de país de envío del pedido. Calculado uniéndose a `sales_order`.`Shipping_address_id` a `sales_order_address`.`entity_id` y devolviendo `country_id` |
| `Shipping address region` | Región de envío (generalmente estado o provincia) del pedido. Calculado uniéndose a `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` y devolviendo el campo `region` |
| `Store name` | El nombre de la tienda de Commerce asociada con este pedido. Calculado uniéndose a `sales_order`.`store_id` a `store`.`store_id` y devolviendo el campo `name` |

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Avg order value` | Ingresos promedio por pedido, donde los ingresos se definen como `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | El tiempo promedio entre el pedido de un cliente (n-1) y el pedido n, para todos los clientes y pedidos | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | La suma del valor bruto de la mercancía para todos los pedidos, donde GMV se define como el subtotal, antes de aplicar todos los impuestos y descuentos | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | La mediana de tiempo entre el pedido de un cliente (n-1) y el pedido n, para todos los clientes y pedidos | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Recuento total de pedidos realizados | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La suma de los ingresos de todos los pedidos, donde los ingresos se definen como el precio final pagado por el cliente, después de aplicar todos los impuestos, descuentos, envíos, etc | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | La suma del importe de envío de todos los pedidos | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | La suma de los impuestos aplicados a todos los pedidos | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | El número de clientes únicos que realizan un pedido en el intervalo de tiempo especificado para la creación de informes. Por ejemplo, si el intervalo del informe es semanal, cada cliente que realiza al menos un pedido en una semana determinada se cuenta exactamente una vez, independientemente de cuántos pedidos haya realizado en esa semana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Rutas de unión

`customer_entity`

* Únase a la tabla `customer_entity` para crear nuevas columnas de nivel de cliente asociadas al cliente que realizó el pedido.
   * Ruta de acceso: `sales_order.customer_id` (varios) => `customer_entity.entity_id` (uno)

`customer_group`

* Únase a la tabla `customer_group` para crear columnas que devuelvan el nombre del grupo de clientes del cliente que realizó el pedido.
   * Ruta de acceso: `sales_order.customer_group_id` (varios) => `customer_group.customer_group_id` (uno)

`sales_order_address`

* Únase a la tabla `sales_order_address` para crear columnas que devuelvan ubicaciones de facturación y envío asociadas con el pedido. Se pueden unir dos rutas, en función de si se requieren los detalles de facturación o envío.
   * Rutas:
      * Envío: `sales_order.shipping_address_id`(varios) => `sales_order_address.entity_id` (uno)
      * Facturación: `sales_order.billing_address_id`(muchos) => `sales_order_address.entity_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén de Commerce asociado al pedido.
   * Ruta de acceso: `sales_order.store_id` (varios) => `store.store_id` (uno)
