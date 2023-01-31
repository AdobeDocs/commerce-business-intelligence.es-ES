---
title: Análisis de pedidos devueltos
description: Aprenda a configurar un tablero que proporcione un análisis detallado de los retornos de su tienda.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Pedidos devueltos

En este artículo, aprenda a configurar un tablero que proporcione un análisis detallado de los retornos de su tienda.

![](../../assets/detailed-returns-dboard.png)

Antes de comenzar, debe ser [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) y debe asegurarse de que su empresa esté utilizando la variable `enterprise\_rma` para las devoluciones.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introducción

Columnas para rastrear

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

Filtrar conjuntos para crear

* **`enterprise_rma`** tabla
* Nombre del conjunto de filtros: `Returns we count`
* Filtrar la lógica del conjunto:
   * Marcador de posición: introduzca su lógica personalizada aquí

* **`enterprise_rma_item_entity`** tabla
* Nombre del conjunto de filtros: `Returns items we count`
* Filtrar la lógica del conjunto:
   * Marcador de posición: introduzca su lógica personalizada aquí

### Columnas calculadas

Columnas que crear

* **`enterprise_rma`** tabla
* **`Order's created at`**
* Seleccione una definición: `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* Seleccione un [!UICONTROL table]: `sales_flat_order`
* Seleccione un [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Seleccione una definición: `Joined Column`
* Seleccione un [!UICONTROL table]: `sales_flat_order`
* Seleccione un [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** lo crea un analista como parte de su `[RETURNS ANALYSIS]` ticket

* **`enterprise_rma_item_entity`** tabla
* **`return_date_requested`**
* Seleccione una definición: `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleccione un [!UICONTROL table]: `enterprise_rma`
* Seleccione un [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** lo crea un analista como parte de su `[RETURNS ANALYSIS]` ticket

* **`sales_flat_order`** tabla
* **`Order contains a return? (1=yes/0=No)`**
* Seleccione una definición: `Exists`
* Seleccione un [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** lo crea un analista como parte de su `[RETURNS ANALYSIS]` ticket
* **`Customer's previous order contains return? (1=yes/0=no)`** lo crea un analista como parte de su `[RETURNS ANALYSIS]` ticket

>[!NOTE]
>
>Si le interesa analizar solo el horario laboral de segundos a resolución o de segundos a primera respuesta, informe al analista cuando solicite el ticket.

### Métricas

* **Devuelve**
* En el **`enterprise_rma`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** column
* Solicitado por el **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Elementos devueltos**
* En el **`enterprise_rma_item_entity`** tabla
* Esta métrica realiza una **Sum**
* En el **`qty_approved`** column
* Solicitado por el **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valor total del elemento devuelto**
* En el **`enterprise_rma_item_entity`** tabla
* Esta métrica realiza una **Sum**
* En el **`Returned item total value (qty_returned * price)`** column
* Solicitado por el **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Promedio de tiempo entre pedido y devolución**
* En el **`enterprise_rma`** tabla
* Esta métrica realiza una **Promedio**
* En el **`Time between order's created_at and date_requested`** column
* Solicitado por el **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

### Informes

* **Repetir la probabilidad de pedido después de realizar un retorno**
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

* Fórmula: Probabilidad de repetición de pedido
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL Tipo de gráfico]: `Bar`

* **Promedio de tiempo para regresar (todo el tiempo)**
* Métrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Number`

* **Porcentaje de pedidos con devolución**
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
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Ingresos devueltos por mes**
* Métrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL Tipo de gráfico]: `Line`

* **Clientes que han realizado una devolución y que no han vuelto a comprar**
* Métrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 
   [!UICONTROL Grupo por]: `Customer_email`
* 

   [!UICONTROL Tipo de gráfico]: `Table`

* **Tasa de devoluciones por artículo**
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
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL Tipo de gráfico]: `Table`

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado puede ser similar al panel de muestra anterior.

Si tiene alguna pregunta al crear este análisis, o simplemente desea contactar con el equipo de Professional Services, [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md).
