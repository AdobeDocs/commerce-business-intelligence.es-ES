---
title: Tabla Enterprise_Rma_Item_Entity
description: Obtenga información sobre cómo analizar información sobre un elemento específico de una devolución solicitada.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
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
