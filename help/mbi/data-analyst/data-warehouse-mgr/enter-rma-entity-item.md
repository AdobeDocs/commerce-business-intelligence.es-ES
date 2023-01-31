---
title: Tabla Enterprise_Rma_Item_Entity
description: Descubra cómo analizar información sobre un elemento específico de una devolución solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# tabla enterprise_rma_item_entity

Cada fila de la `enterprise_rma_item_entity` tabla (denominada con frecuencia `magento_rma_item_entity` en Commerce 2.x, pero el nombre se puede personalizar) contiene información sobre un elemento específico de una devolución solicitada.

>[!NOTE]
>
>Esta tabla solo viene estándar con su cuenta de comercio si es un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Columnas nativas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `entity\_id` | Identificador único de la tabla. Cada `entity\_id` representa un elemento que se solicitó para su devolución. |
| `rma\_entity\_id` | Clave externa asociada con la variable `enterprise\_rma` tabla. |
| `status` | El estado del retorno del elemento. Los valores incluyen &quot;recibido&quot;, &quot;pendiente&quot;, &quot;autorizado&quot;, entre otros. Los valores de este estado no coinciden necesariamente con el valor del estado de devolución general. |
| `qty\_requested` | La cantidad que el cliente solicita para que se devuelva. |
| `qty\_approved` | Cantidad aprobada para devolución. |
| `qty\_returned` | La cantidad realmente devuelta. |
| `order\_item\_id` | Clave externa asociada con la variable `sales\_flat\_order\_item` tabla. |
| `product\_sku` | El sku que está siendo devuelto. |

{style=&quot;table-layout:auto&quot;}

## Columnas calculadas comunes

| **Nombre de columna** | **Descripción** |
|---|---|
| `Return date\_requested` | Esta es la fecha en la que el cliente solicitó la devolución. |
| `Item price` | El precio del artículo. |
| `Return item's total value (qty\_returned * price)` | Es el valor monetario total de los artículos que se devuelven. Se utilizará para calcular el importe total de devolución en la variable `enterprise\_rma` tabla. |

{style=&quot;table-layout:auto&quot;}

## Métricas comunes

| **Nombre de la métrica** | **Descripción** | **Construcción** |
|---|---|---|
| `Number of items returned` | Número de elementos que se devuelven. | Columna de operación: cantidad devuelta<br>Operación: Sum<br>Columna de marca de tiempo: Fecha de retorno solicitada |
| `Returned items' total value` | El importe monetario devuelto. | Columna de operación: Valor total del artículo devuelto (cantidad devuelta * precio)<br>Operación: Sum<br>Columna de marca de tiempo: Fecha de retorno solicitada |

{style=&quot;table-layout:auto&quot;}

## Conexiones a otras tablas

`enterprise_rma`

* Crear columnas unidas como `Return date\_requested` en el `enterprise_rma_item_entity` mediante la siguiente unión:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (muchos) => `enterprise_rma.entity_id` (1)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (muchos) => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* Crear columnas unidas en la variable  `enterprise_rma_item_entity` mediante la siguiente unión:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (muchos) => `sales_flat_order_item.item_id` (1)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (muchos) => `sales_order_item.item_id` (1)
