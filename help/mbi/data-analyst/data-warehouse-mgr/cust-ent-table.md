---
title: tabla customer_entity
description: Obtenga información sobre cómo acceder a los registros de todas las cuentas registradas.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Tabla customer_entity

La tabla `customer_entity` contiene registros de todas las cuentas registradas. Una cuenta se considera registrada si se inscribe en una cuenta, independientemente de si alguna vez completa una compra. Cada fila corresponde a una cuenta registrada única, identificada por el `entity_id` de esa cuenta.

Esta tabla no contiene registros de clientes que realizan un pedido a través del cierre de compra de un invitado. Si su tienda acepta pagos de invitados, vea [cómo contabilizar los pedidos de invitados](../data-warehouse-mgr/guest-orders.md) para esos pedidos.

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `created_at` | Marca de tiempo correspondiente a la fecha de registro de la cuenta, almacenada localmente en UTC. Según la configuración de [!DNL Commerce Intelligence], esta marca de tiempo se puede convertir a una zona horaria de informe en [!DNL Commerce Intelligence] que difiera de la zona horaria de la base de datos |
| `email` | Dirección de correo electrónico asociada a la cuenta |
| `entity_id` (PK) | Identificador único de la tabla y que se utiliza comúnmente en combinaciones con `customer_id` en otras tablas dentro de la instancia |
| `group_id` | Clave externa asociada con la tabla `customer_group`. Únase a `customer_group.customer_group_id` para determinar el grupo de clientes asociado con la cuenta registrada |
| `store_id` | Clave externa asociada con la tabla `store`. Unirse a `store`.`store_id` para determinar qué vista de la tienda Commerce está asociada a la cuenta registrada |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Customer's first 30 day revenue` | Suma total de ingresos para todos los pedidos realizados por este cliente en un plazo de 30 días a partir de la primera fecha de pedido del cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y sumando el campo `base_grand_total` para todos los pedidos en los que `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, que es el número de segundos en 30 días |
| `Customer's first order date` | Marca de tiempo del primer pedido realizado por este cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y devolviendo el mínimo `sales_order`.Valor `created_at` |
| `Customer's first order's billing region` | Región de facturación asociada al primer pedido del cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y devolviendo `Billing address region` donde `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Código de cupón asociado con el primer pedido del cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y devolviendo `sales_order.coupon_code` donde `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nombre del grupo del cliente registrado. Se calcula uniendo `customer_entity.group_id` a `customer_group`.`customer_group_id` y devolviendo el campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Número total de cupones aplicados a todos los pedidos realizados por este cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y contando el número de pedidos donde `sales_order.coupon_code` no es `NULL` |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y contando el número de filas de la tabla `sales_order` |
| `Customer's lifetime revenue` | Suma del total de ingresos de todos los pedidos realizados por este cliente. Se calcula uniendo `customer_entity.entity_id` a `sales_order.customer_id` y sumando el campo `base_grand_total` para todos los pedidos realizados por este cliente |
| `Seconds since customer's first order date` | Tiempo transcurrido entre la primera fecha de pedido del cliente y el momento actual. Se calcula restando `Customer's first order date` de la marca de tiempo del servidor en el momento en que se ejecuta la consulta, devuelto como un número entero de segundos |
| `Store name` | El nombre de la tienda Commerce asociada con esta cuenta registrada. Se calcula uniendo `customer_entity.store_id` a `store.store_id` y devolviendo el campo `name` |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Avg first 30 day revenue` | Ingresos promedio por cliente para pedidos realizados dentro de los 30 días posteriores al primer pedido del cliente | Operación: Average<br/>Operand: `Customer's first 30 day revenue`<br/>Marca de tiempo: `created_at`<br/>Filtros:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (excluye a los clientes que aún no han alcanzado los 30 días desde su primer pedido) |
| `Avg lifetime coupons` | Número promedio de cupones aplicados a pedidos por cliente durante su vida útil | Operación: Average<br/>Operand: `Customer's lifetime number of coupons`<br/>Marca de tiempo: `created_at` |
| `Avg lifetime orders` | El número promedio de pedidos realizados por cliente durante su vida útil | Operación: Average<br/>Operand: `Customer's lifetime number of orders`<br/>Marca de tiempo: `created_at` |
| `Avg lifetime revenue` | Ingresos totales promedio por cliente de todos los pedidos realizados durante su vida útil | Operación: Average<br/>Operand: `Customer's lifetime revenue`<br/>Marca de tiempo: `created_at` |
| `New customers` | El número de clientes con al menos un pedido, contabilizados en la fecha de su primer pedido. Excluye las cuentas que se registran pero nunca realizan un pedido | Operación: Count<br/>Operand: `entity_id`<br/>Marca de tiempo: `Customer's first order date` |
| `Registered accounts` | Número de cuentas registradas. Incluye todas las cuentas registradas, independientemente de si la cuenta ha realizado o no un pedido | Operación: Count<br/>Operand: `entity_id`<br/>Marca de tiempo: `created_at` |

{style="table-layout:auto"}

## Rutas de unión de clave externa

`customer_group`

* Únase a la tabla `customer_group` para crear columnas que devuelvan el nombre de grupo de clientes de la cuenta registrada.
   * Ruta de acceso: `customer_entity.group_id` (varios) => `customer_group.customer_group_id` (uno)

`store`

* Únase a la tabla `store` para crear columnas que devuelvan detalles relacionados con el almacén asociado a la cuenta registrada.
   * Ruta de acceso: `customer_entity.store_id` (varios) => `store.store_id` (uno)
