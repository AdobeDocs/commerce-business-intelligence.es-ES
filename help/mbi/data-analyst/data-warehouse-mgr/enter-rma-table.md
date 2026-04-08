---
title: tabla enterprise_rma
description: Obtenga información sobre cómo analizar información sobre una solicitud de retorno específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: ad4dda927f0b1b2eba9596d7adfd1419676cf03d
workflow-type: tm+mt
source-wordcount: 267
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
| `entity_id` | Identificador único de la tabla. Cada `entity_id` representa una solicitud de retorno. |
| `date_requested` | La fecha en la que se solicitó la devolución. |
| `status` | El estado de la devolución. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. |
| `order_id` | Clave externa asociada con la tabla `sales_flat_order`. |
| `customer_id` | Clave externa asociada con la tabla `customer_entity`. |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Order's created_at` | Esta es la fecha del pedido original. Esto se puede utilizar para obtener el tiempo entre el pedido y la solicitud de devolución. |
| `Customer's order number` | Número de pedido del cliente asociado con el pedido original. |
| `Seconds between order's created_at and return's date_requested` | El número de segundos desde la fecha de pedido hasta la solicitud de devolución. |
| `Return's total value` | Es la cantidad monetaria total que se devuelve. Es la suma del importe de devolución individual de cada artículo de devolución. |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of returns` | El número de devoluciones solicitadas. | `Operation` columna: `entity_id`<br>`Operation`: `Count`<br>`Timestamp` Columna: `date requested` |
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
