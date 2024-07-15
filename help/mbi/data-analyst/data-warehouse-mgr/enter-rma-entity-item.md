---
title: Tabla Enterprise_Rma_Item_Entity
description: Obtenga información sobre cómo analizar información sobre un elemento específico de una devolución solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# tabla enterprise_rma_item_entity

Cada fila de la tabla `enterprise_rma_item_entity` (denominada con frecuencia `magento_rma_item_entity` en Commerce 2.x, pero el nombre se puede personalizar) contiene información sobre un elemento específico de una devolución solicitada.

>[!NOTE]
>
>Esta tabla solo viene de serie con su cuenta de Commerce si es cliente de `Enterprise Edition` o `Enterprise Cloud Edition`.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `entity\_id` | Identificador único de la tabla. Cada `entity\_id` representa un elemento que se ha solicitado para su devolución. |
| `rma\_entity\_id` | Clave externa asociada con la tabla `enterprise\_rma`. |
| `status` | El estado de devolución del elemento. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. Es posible que los valores de este estado no coincidan con el valor del estado de la devolución general. |
| `qty\_requested` | Cantidad que el cliente solicita devolver. |
| `qty\_approved` | Cantidad aprobada para devolución. |
| `qty\_returned` | La cantidad devuelta. |
| `order\_item\_id` | Clave externa asociada con la tabla `sales\_flat\_order\_item`. |
| `product\_sku` | El SKU que se devuelve. |

{style="table-layout:auto"}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Return date\_requested` | Esta es la fecha en la que el cliente solicitó la devolución. |
| `Item price` | El precio del artículo. |
| `Return item's total value (qty\_returned * price)` | Es el valor monetario total de los elementos que se devuelven. Se utiliza para calcular la cantidad total de devolución en la tabla `enterprise\_rma`. |

{style="table-layout:auto"}

## Métricas comunes

| **Nombre de métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of items returned` | El número de elementos que se devuelven. | Columna de operación: cantidad devuelta<br>Operación: suma<br>Columna de marca de tiempo: fecha de devolución solicitada |
| `Returned items' total value` | El importe monetario devuelto. | Columna de operación: Valor total del elemento de devolución (cantidad devuelta * precio)<br>Operación: Sum<br>Columna de marca de tiempo: Fecha de devolución solicitada |

{style="table-layout:auto"}

## Conexiones a otras tablas

`enterprise_rma`

* Cree columnas unidas como `Return date\_requested` en la tabla `enterprise_rma_item_entity` mediante la siguiente unión:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (varios) => `enterprise_rma.entity_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (varios) => `magento_rma.entity_id` (uno)

`sales_flat_order_item`

* Crear columnas unidas en  `enterprise_rma_item_entity` tabla a través de la siguiente unión:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (varios) => `sales_flat_order_item.item_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (varios) => `sales_order_item.item_id` (uno)
