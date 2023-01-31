---
title: tabla customer_entity
description: Obtenga información sobre cómo acceder a los registros de todas las cuentas registradas.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Tabla customer_entity

La variable `customer_entity` contiene registros de todas las cuentas registradas. Una cuenta se considera registrada si se inscribe en una cuenta, independientemente de si completa o no una compra. Cada fila corresponde a una cuenta registrada única, identificada por el `entity_id`.

Esta tabla no contiene registros de clientes que realizan un pedido mediante el cierre de compra de un invitado. Si la tienda acepta el cierre de compra de invitado, [obtenga información sobre cómo contar](../data-warehouse-mgr/guest-orders.md) para esos clientes.

## Columnas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `created_at` | Marca de tiempo correspondiente a la fecha de registro de la cuenta, generalmente almacenada localmente en UTC. Según la configuración de [!DNL MBI], esta marca de tiempo puede convertirse en una zona horaria de informes en [!DNL MBI] que difiere de la zona horaria de la base de datos |
| `email` | Dirección de correo electrónico asociada a la cuenta |
| `entity_id` (PK) | Identificador único de la tabla y se utiliza comúnmente en las uniones al `customer_id` en otras tablas dentro de la instancia |
| `group_id` | Clave externa asociada con la variable `customer_group` tabla. Unirse a `customer_group.customer_group_id` para determinar el grupo de clientes asociado a la cuenta registrada |
| `store_id` | Clave externa asociada con la variable `store` tabla. Unirse a `store`.`store_id` para determinar qué vista del almacén de comercio está asociada a la cuenta registrada |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Customer's first 30 day revenue` | Suma total de ingresos para todos los pedidos realizados por este cliente en un plazo de 30 días a partir de la fecha del primer pedido del cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y resumen del `base_grand_total` campo para todos los pedidos donde `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, que es el número de segundos en 30 días |
| `Customer's first order date` | Marca de tiempo del primer pedido realizado por este cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y devolver el mínimo `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Región de facturación asociada al primer pedido del cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y devolver el `Billing address region` donde `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Código de cupón asociado al primer pedido del cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y devolver el `sales_order.coupon_code` donde `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nombre del grupo del cliente registrado. Calculado uniéndose `customer_entity.group_id` a `customer_group`.`customer_group_id` y devolver el `customer_group_code` field |
| `Customer's lifetime number of coupons` | Número total de cupones aplicados a todos los pedidos realizados por este cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y contando el número de pedidos donde `sales_order.coupon_code` no es `NULL` |
| `Customer's lifetime number of orders` | Recuento total de pedidos realizados por este cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y contando el número de filas de la variable `sales_order` tabla |
| `Customer's lifetime revenue` | Suma total de ingresos para todos los pedidos realizados por este cliente. Calculado uniéndose `customer_entity.entity_id` a `sales_order.customer_id` y resumen del `base_grand_total` campo para todos los pedidos realizados por este cliente |
| `Seconds since customer's first order date` | Tiempo transcurrido entre la fecha del primer pedido del cliente y ahora. Calculado restando `Customer's first order date` desde la marca de tiempo del servidor en el momento de ejecutar la consulta, devuelta como un número entero de segundos |
| `Store name` | El nombre del almacén de comercio asociado con esta cuenta registrada. Calculado uniéndose `customer_entity.store_id` a `store.store_id` y devolver el `name` field |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Avg first 30 day revenue` | El ingreso promedio por cliente de los pedidos realizados dentro de los 30 días posteriores al primer pedido del cliente | Operación: Promedio<br/>Operando: `Customer's first 30 day revenue`<br/>Marca de tiempo: `created_at`<br/>Filtros:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (excluye a los clientes que aún no han alcanzado los 30 días desde su primer pedido) |
| `Avg lifetime coupons` | El número promedio de cupones aplicados a los pedidos por cliente durante su vida útil | Operación: Promedio<br/>Operando: `Customer's lifetime number of coupons`<br/>Marca de tiempo: `created_at` |
| `Avg lifetime orders` | El número promedio de pedidos realizados por cliente durante su vida útil | Operación: Promedio<br/>Operando: `Customer's lifetime number of orders`<br/>Marca de tiempo: `created_at` |
| `Avg lifetime revenue` | El promedio de ingresos totales por cliente para todos los pedidos realizados a lo largo de su vida útil | Operación: Promedio<br/>Operando: `Customer's lifetime revenue`<br/>Marca de tiempo: `created_at` |
| `New customers` | Número de clientes con al menos un pedido, contabilizado en la fecha del primer pedido. Excluye las cuentas que se registran pero nunca realizan un pedido | Operación: Recuento<br/>Operando: `entity_id`<br/>Marca de tiempo: `Customer's first order date` |
| `Registered accounts` | Número de cuentas registradas. Incluye todas las cuentas registradas, independientemente de si la cuenta realizó o no un pedido | Operación: Recuento<br/>Operando: `entity_id`<br/>Marca de tiempo: `created_at` |

{style=&quot;table-layout:auto&quot;}

## Rutas de unión de clave externa

`customer_group`

* Unirse a `customer_group` para crear nuevas columnas que devuelvan el nombre del grupo de clientes de la cuenta registrada.
   * Ruta: `customer_entity.group_id` (muchos) => `customer_group.customer_group_id` (1)

`store`

* Unirse a `store` para crear nuevas columnas que devuelvan detalles relacionados con el almacén asociado a la cuenta registrada.
   * Ruta: `customer_entity.store_id` (muchos) => `store.store_id` (1)
