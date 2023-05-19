---
title: Pérdida de comercio
description: Obtenga información sobre cómo generar y analizar la tasa de pérdida de Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Tasa de pérdida

En este tema se muestra cómo calcular una **tasa de pérdida** para su **clientes comerciales**. A diferencia del SaaS o de las empresas de suscripción tradicionales, los clientes de comercio no suelen tener un **&quot;evento de pérdida&quot;** para mostrarle que ya no deben contar hacia sus clientes activos. Por este motivo, las siguientes instrucciones le permiten definir un cliente como &quot;perdido&quot; en función de un tiempo determinado transcurrido desde su último pedido.

![](../../assets/Churn_rate_image.png)

Muchos clientes quieren ayuda para empezar a conceptualizar lo que **periodo de tiempo** deben utilizar en función de sus datos. Si desea utilizar el comportamiento histórico del cliente para definir esto **plazo de cancelación**, es posible que desee familiarizarse con el [definición de pérdida](../analysis/define-cust-churn.md) tema. A continuación, puede utilizar los resultados en la fórmula para la tasa de pérdida en las instrucciones siguientes.

## Columnas calculadas

Columnas para crear

* **`customer_entity`** tabla
* **`Customer's last order date`**
   * Seleccione una [!UICONTROL definition]: `Max`
   * Seleccionar [!UICONTROL table]: `sales_flat_order`
   * Seleccionar [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Seleccione una [!UICONTROL definition]: `Age`
   * Seleccionar [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Métricas

* **Clientes nuevos (por fecha de primer pedido)**
   * Clientes que se cuentan

>[!NOTE]
>
>Esta métrica puede existir en su cuenta.

* En el **`customer_entity`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** columna
* Ordenado por el **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Clientes nuevos (por fecha de último pedido)**
   * Clientes que se cuentan

   >[!NOTE]
   >
   >Esta métrica puede existir en su cuenta.

* En el **`customer_entity`** tabla
* Esta métrica realiza una **Recuento**
* En el **`entity_id`** columna
* Ordenado por el **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Tasa de pérdida**
   * [!UICONTROL Metric]: Clientes nuevos (por fecha de primer pedido)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Segundos transcurridos desde la última fecha de pedido del cliente >= [Su límite autodefinido para los clientes perdidos ]**`^`**
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

A continuación se muestran algunas conversiones comunes de mes > segundo, pero Google proporciona otros valores, incluidas las conversiones de semana > segundo para cualquier valor personalizado que pueda estar buscando.

| **Meses** | **Seconds** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar al panel de muestra anterior.
