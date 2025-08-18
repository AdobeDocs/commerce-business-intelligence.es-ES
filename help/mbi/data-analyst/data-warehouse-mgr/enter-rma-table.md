---
title: tabla enterprise_rma
description: Obtenga información sobre cómo analizar información sobre una solicitud de retorno específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# tabla enterprise_rma

Cada fila de la tabla `enterprise_rma` (denominada a menudo `magento_rma` en Adobe Commerce 2.x, pero el nombre se puede personalizar) contiene información sobre una solicitud de retorno específica.

>[!NOTE]
>
>Esta tabla solo viene de serie con su cuenta de Adobe Commerce si es cliente de `Enterprise Edition` o `Enterprise Cloud Edition`.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `entity\_id` | Identificador único de la tabla. Cada `entity\_id` representa una solicitud de retorno. |
| `date\_requested` | La fecha en la que se solicitó la devolución. |
| `status` | El estado de la devolución. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. |
| `order\_id` | Clave externa asociada con la tabla `sales\_flat\_order`. |
| `customer\_id` | Clave externa asociada con la tabla `customer\_entity`. |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Order's created\_at` | Esta es la fecha del pedido original. Esto se puede utilizar para obtener el tiempo entre el pedido y la solicitud de devolución. |
| `Customer's order number` | Número de pedido del cliente asociado con el pedido original. |
| `Seconds between order's created\_at and return's date\_requested` | El número de segundos desde la fecha de pedido hasta la solicitud de devolución. |
| `Return's total value` | Es la cantidad monetaria total que se devuelve. Es la suma del importe de devolución individual de cada artículo de devolución. |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of returns` | El número de devoluciones solicitadas. | `Operation` columna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Columna: `date requested` |
| `Total returned amount` | El importe monetario total devuelto. | `Operation `Columna: `Return's total value`<br>`Operation`: Sum<br>`Timestamp` Columna: fecha solicitada |
| `Average returned amount` | El importe monetario promedio devuelto. | `Operation` ` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Columna: `date requested` |
| `Average time to return` | El tiempo promedio desde el pedido hasta la devolución. | Columna `Operation`: segundos entre la fecha de creación del pedido y la fecha de devolución solicitada<br>`Operation`: `Average`<br>`Timestamp` Columna: `date requested` |

{style="table-layout:auto"}

## Conexiones a otras tablas

`sale_flat_order`

* Cree columnas unidas para segmentar y filtrar por atributos de nivel de pedido en la tabla `enterprise_rma` mediante la siguiente unión:
   * Commerce 1.x: `enterprise_rma.order_id` (varios) => `sales_flat_order.entity_id` (uno)
   * Commerce 2.x: `magento_rma.order_id` (varios) => `sales_order.entity_id` (uno)

`enterprise_rma_item_entity`

* Cree columnas varios a uno como `Return's total value` en la tabla `enterprise_rma` mediante la siguiente combinación:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (varios) => `enterprise_rma.entity_id` (uno)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (varios) => `magento_rma.entity_id` (uno)
