---
title: Pérdida de comercio
description: Obtenga información sobre cómo generar y analizar la tasa de pérdida de comercio.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Tasa de pérdida

En este tema, se muestra cómo calcular una **tasa de pérdida** para su **clientes comerciales**. A diferencia de SaaS o de las empresas de suscripción tradicionales, los clientes comerciales normalmente no tienen un **&quot;Evento de pérdida&quot;** para mostrarle que ya no deben contar para sus clientes activos. Por este motivo, las instrucciones siguientes le permiten definir a un cliente como &quot;eclipsado&quot; en función de una cantidad determinada de tiempo transcurrido desde su último pedido.

![](../../assets/Churn_rate_image.png)

Muchos clientes desean ayuda para empezar a conceptualizar qué **periodo de tiempo** deben utilizar según sus datos. Si desea utilizar el comportamiento histórico del cliente para definir esto **pérdida de intervalo de tiempo**, es posible que desee familiarizarse con el [definición de pérdida](../analysis/define-cust-churn.md) artículo. A continuación, puede utilizar los resultados en la fórmula para la tasa de pérdida en las instrucciones siguientes.

## Columnas calculadas

Columnas que crear

* **`customer_entity`** tabla
* **`Customer's last order date`**
   * Seleccione un [!UICONTROL definition]: `Max`
   * Select [!UICONTROL table]: `sales_flat_order`
   * Select [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Seleccione un [!UICONTROL definition]: `Age`
   * Select [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Métricas

* **Clientes nuevos (por fecha de primer pedido)**
   * Clientes que contamos

>[!NOTE]
>
>Es posible que esta métrica ya exista en su cuenta.

* En el **`customer_entity`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** column
* Solicitado por el **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Clientes nuevos (por fecha de último pedido)**
   * Clientes que contamos

>[!NOTE]
>
>Es posible que esta métrica ya exista en su cuenta.

* En el **`customer_entity`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** column
* Solicitado por el **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Tasa de pérdida**
   * [!UICONTROL Metric]: Clientes nuevos (por fecha de primer pedido)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Segundos desde la última fecha de pedido del cliente >= [Su corte autodefinido para los clientes rechazados ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *Métrica `A`:`New customers cumulative`*
* *Métrica `B`:`Churned customers by last order date`*
* *Métrica `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

A continuación se muestran algunos meses comunes > segundas conversiones, pero google proporciona otros valores, como semana > segundos de conversión para cualquier valor personalizado que esté buscando.

| **Months** | **Segundos** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado final puede ser similar al panel de muestra anterior.
