---
title: Análisis de Pedidos Devueltos
description: Aprenda a configurar un tablero que proporcione un análisis detallado de las devoluciones de su tienda.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Pedidos devueltos

En este tema se muestra cómo configurar un tablero que proporcione un análisis detallado de las devoluciones de la tienda.

![](../../assets/detailed-returns-dboard.png)

Antes de empezar, debe ser un [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) cliente de y debe asegurarse de que su empresa utiliza el `enterprise\_rma` tabla para devoluciones.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Primeros pasos

Columnas que rastrear

* **`enterprise_rma`** o **`rma`** tabla
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** o **`rma_item_entity`** tabla
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Conjuntos de filtros para crear

* **`enterprise_rma`** tabla
* Nombre del conjunto de filtros: `Returns we count`
* Lógica del conjunto de filtros:
   * Marcador de posición: introduzca la lógica personalizada aquí

* **`enterprise_rma_item_entity`** tabla
* Nombre del conjunto de filtros: `Returns items we count`
* Lógica del conjunto de filtros:
   * Marcador de posición: introduzca la lógica personalizada aquí

### Columnas calculadas

Columnas para crear

* **`enterprise_rma`** tabla
* **`Order's created at`**
* Seleccione una definición: `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* Seleccione una [!UICONTROL table]: `sales_flat_order`
* Seleccione una [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Seleccione una definición: `Joined Column`
* Seleccione una [!UICONTROL table]: `sales_flat_order`
* Seleccione una [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** es creado por un analista como parte de su `[RETURNS ANALYSIS]` boleto

* **`enterprise_rma_item_entity`** tabla
* **`return_date_requested`**
* Seleccione una definición: `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleccione una [!UICONTROL table]: `enterprise_rma`
* Seleccione una [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** es creado por un analista como parte de su `[RETURNS ANALYSIS]` boleto

* **`sales_flat_order`** tabla
* **`Order contains a return? (1=yes/0=No)`**
* Seleccione una definición: `Exists`
* Seleccione una [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** es creado por un analista como parte de su `[RETURNS ANALYSIS]` boleto
* **`Customer's previous order contains return? (1=yes/0=no)`** es creado por un analista como parte de su `[RETURNS ANALYSIS]` boleto

>[!NOTE]
>
>Si está interesado en analizar solo el horario laboral de Segundos a resolución o Segundos a primera respuesta, informe al analista al solicitar el ticket.

### Métricas

* **Devuelve**
* En el **`enterprise_rma`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** columna
* Ordenado por el **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Elementos devueltos**
* En el **`enterprise_rma_item_entity`** tabla
* Esta métrica realiza una **Sum**
* En el **`qty_approved`** columna
* Ordenado por el **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valor total del artículo devuelto**
* En el **`enterprise_rma_item_entity`** tabla
* Esta métrica realiza una **Sum**
* En el **`Returned item total value (qty_returned * price)`** columna
* Ordenado por el **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tiempo promedio entre el pedido y la devolución**
* En el **`enterprise_rma`** tabla
* Esta métrica realiza una **Media**
* En el **`Time between order's created_at and date_requested`** columna
* Ordenado por el **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

### Informes

* **Probabilidad de repetir el pedido después de realizar una devolución**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Métrica `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Fórmula: Probabilidad de orden de repetición
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL Tipo de gráfico]: `Bar`

* **Tiempo promedio para el retorno (todo el tiempo)**
* Métrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Number`

* **Porcentaje de pedidos con una devolución**
* Métrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Métrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Fórmula: % de pedidos con devolución
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Ingresos devueltos por mes**
* Métrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL Tipo de gráfico]: `Line`

* **Clientes que han realizado una devolución y no han vuelto a comprar**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 
   [!UICONTROL Agrupar por]: `Customer_email`
* 

   [!UICONTROL Tipo de gráfico]: `Table`

* **Tasa de devolución por artículo**
* Métrica `A`: `Returned items` (Ocultar)
* [!UICONTROL Metric]: Elementos devueltos

* Métrica `B`: `Items sold` (Ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL Tipo de gráfico]: `Table`

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar al panel de muestra anterior.

Si tiene alguna pregunta mientras realiza este análisis o desea contactar con el equipo de Servicios profesionales, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
