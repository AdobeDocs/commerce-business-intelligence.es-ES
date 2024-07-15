---
title: Análisis de Pedidos Devueltos
description: Aprenda a configurar un tablero que proporcione un análisis detallado de las devoluciones de su tienda.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Pedidos devueltos

En este tema se muestra cómo configurar un tablero que proporcione un análisis detallado de las devoluciones de la tienda.

![](../../assets/detailed-returns-dboard.png)

Antes de comenzar, debe ser cliente de [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) y debe asegurarse de que su compañía esté usando la tabla `enterprise\_rma` para las devoluciones.

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

* Seleccionar un(a) [!UICONTROL table]: `sales_flat_order`
* Seleccionar un(a) [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Seleccione una definición: `Joined Column`
* Seleccionar un(a) [!UICONTROL table]: `sales_flat_order`
* Seleccionar un(a) [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** lo ha creado un analista como parte de su ticket de `[RETURNS ANALYSIS]`

* **`enterprise_rma_item_entity`** tabla
* **`return_date_requested`**
* Seleccione una definición: `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleccionar un(a) [!UICONTROL table]: `enterprise_rma`
* Seleccionar un(a) [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** lo ha creado un analista como parte de su ticket de `[RETURNS ANALYSIS]`

* **`sales_flat_order`** tabla
* **`Order contains a return? (1=yes/0=No)`**
* Seleccione una definición: `Exists`
* Seleccionar un(a) [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** lo ha creado un analista como parte de su ticket de `[RETURNS ANALYSIS]`
* **`Customer's previous order contains return? (1=yes/0=no)`** lo ha creado un analista como parte de su ticket de `[RETURNS ANALYSIS]`

>[!NOTE]
>
>Si está interesado en analizar solo el horario laboral de Segundos a resolución o Segundos a primera respuesta, informe al analista al solicitar el ticket.

### Métricas

* **Devuelve**
* En la tabla **`enterprise_rma`**
* Esta métrica realiza **Count**
* En la columna **`entity_id`**
* Ordenado por **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Elementos devueltos**
* En la tabla **`enterprise_rma_item_entity`**
* Esta métrica arroja una **Sum**
* En la columna **`qty_approved`**
* Ordenado por **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valor total del elemento devuelto**
* En la tabla **`enterprise_rma_item_entity`**
* Esta métrica arroja una **Sum**
* En la columna **`Returned item total value (qty_returned * price)`**
* Ordenado por **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tiempo promedio entre el pedido y la devolución**
* En la tabla **`enterprise_rma`**
* Esta métrica realiza un **Average**
* En la columna **`Time between order's created_at and date_requested`**
* Ordenado por **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

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

* **Tiempo promedio para regresar (todo el tiempo)**
* Métrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
  [!INTERVALO UICONTROL]: `None`
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
  [!INTERVALO UICONTROL]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Ingresos devueltos por mes**
* Métrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 
  [!UICONTROL Tipo de gráfico]: `Line`

* **Clientes que han realizado una devolución y no han comprado de nuevo**
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

* **Tasa de retorno por elemento**
* Métrica `A`: `Returned items` (Ocultar)
* [!UICONTROL Metric]: elementos devueltos

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

Si tiene alguna pregunta al generar este análisis o quiere contactar con el equipo de Servicios profesionales, [póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
