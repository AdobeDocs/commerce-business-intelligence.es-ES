---
title: tabla enterprise_rma
description: Descubra cómo analizar la información sobre una solicitud de devolución específica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# tabla enterprise_rma

Cada fila de la `enterprise_rma` tabla (denominada con frecuencia `magento_rma` en Commerce 2.x, pero el nombre se puede personalizar) contiene información sobre una solicitud de devolución específica.

>[!NOTE]
>
>Esta tabla solo viene estándar con su cuenta de comercio si es un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `entity\_id` | Identificador único de la tabla. Cada `entity\_id` representa una solicitud de devolución. |
| `date\_requested` | La fecha en que se solicitó la devolución. |
| `status` | El estado del retorno. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. |
| `order\_id` | Clave externa asociada con la variable `sales\_flat\_order` tabla. |
| `customer\_id` | Clave externa asociada con la variable `customer\_entity` tabla. |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Order's created\_at` | Esta es la fecha del pedido original. Se puede utilizar para obtener el tiempo entre la solicitud de pedido y la solicitud de devolución. |
| `Customer's order number` | Es el número de pedido del cliente asociado al pedido original. |
| `Seconds between order's created\_at and return's date\_requested` | El número de segundos desde la fecha de pedido hasta la solicitud de devolución. |
| `Return's total value` | Es la cantidad monetaria total que se devuelve. Será la suma de la cantidad de devolución individual de cada artículo de retorno. |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of returns` | Número de devoluciones solicitadas. | `Operation` columna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Columna: `date requested` |
| `Total returned amount` | El importe monetario total devuelto. | `Operation `Columna: `Return's total value`<br>`Operation`: Sum<br>`Timestamp` Columna: fecha solicitada |
| `Average returned amount` | El importe monetario promedio devuelto. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Columna: `date requested` |
| `Average time to return` | El tiempo promedio desde el pedido hasta el retorno. | `Operation` Columna: Segundos entre la fecha de creación del pedido y la fecha de devolución solicitada<br>`Operation`: `Average`<br>`Timestamp` Columna: `date requested` |

{style=&quot;table-layout:auto&quot;}

## Conexiones a otras tablas

`sale_flat_order`

* Cree columnas unidas para segmentar y filtrar por atributos de nivel de pedido en la variable `enterprise_rma` mediante la siguiente unión:
   * Commerce 1.x: `enterprise_rma.order_id` (muchos) => `sales_flat_order.entity_id` (1)
   * Commerce 2.x: `magento_rma.order_id` (muchos) => `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* Cree columnas &quot;varios a uno&quot; como `Return's total value` en el `enterprise_rma` mediante la siguiente unión:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (muchos) => `enterprise_rma.entity_id` (1)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muchos) => `magento_rma.entity_id` (1)
