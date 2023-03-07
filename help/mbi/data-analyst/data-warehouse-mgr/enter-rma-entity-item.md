---
title: Tabla Enterprise_Rma_Item_Entity
description: Obtenga información sobre cómo analizar información sobre un elemento específico de una devolución solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# tabla enterprise_rma_item_entity

Cada fila de la `enterprise_rma_item_entity` tabla (a menudo denominada `magento_rma_item_entity` en Commerce 2.x, pero el nombre se puede personalizar) contiene información sobre un artículo específico de una devolución solicitada.

>[!NOTE]
>
>Esta tabla solo viene de serie con su cuenta de Commerce si es un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `entity\_id` | Identificador único de la tabla. Cada `entity\_id` representa un elemento que se ha solicitado devolver. |
| `rma\_entity\_id` | Clave externa asociada con el `enterprise\_rma` tabla. |
| `status` | El estado de devolución del elemento. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. Es posible que los valores de este estado no coincidan con el valor del estado de la devolución general. |
| `qty\_requested` | Cantidad que el cliente solicita devolver. |
| `qty\_approved` | Cantidad aprobada para devolución. |
| `qty\_returned` | La cantidad devuelta. |
| `order\_item\_id` | Clave externa asociada con el `sales\_flat\_order\_item` tabla. |
| `product\_sku` | El SKU que se devuelve. |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Return date\_requested` | Esta es la fecha en la que el cliente solicitó la devolución. |
| `Item price` | El precio del artículo. |
| `Return item's total value (qty\_returned * price)` | Es el valor monetario total de los elementos que se devuelven. Se utiliza para calcular el importe total de retorno de la `enterprise\_rma` tabla. |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of items returned` | El número de elementos que se devuelven. | Columna de operación: cantidad devuelta<br>Operación: Sum<br>Columna Timestamp: Fecha de devolución solicitada |
| `Returned items' total value` | El importe monetario devuelto. | Columna de Operación: Valor total del artículo devuelto (cantidad devuelta * precio)<br>Operación: Sum<br>Columna Timestamp: Fecha de devolución solicitada |

{style="table-layout:auto"}

## Conexiones a otras tablas

`enterprise_rma`

* Crear columnas unidas como `Return date\_requested` en el `enterprise_rma_item_entity` mediante la siguiente combinación:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muchos) => `enterprise_rma.entity_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muchos) => `magento_rma.entity_id` (uno)

`sales_flat_order_item`

* Crear columnas unidas en  `enterprise_rma_item_entity` mediante la siguiente combinación:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muchos) => `sales_flat_order_item.item_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muchos) => `sales_order_item.item_id` (uno)
