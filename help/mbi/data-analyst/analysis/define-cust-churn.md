---
title: Definir la pérdida de clientes
description: Aprenda a configurar un tablero que le ayude a definir la pérdida para sus clientes transaccionales.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Pérdida de cliente transaccional

En este artículo, le mostramos cómo configurar un panel que le ayude a definir la pérdida para sus clientes transaccionales.

![](../../assets/churn-deashboard.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Columnas que crear

* `customer_entity` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: `Count`
* Seleccione un [!UICONTROL table]: `sales_flat_order`
* Seleccione un [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_plana_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Pedidos que contamos

* `sales_flat_order` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: Columna unida
* Seleccione un [!UICONTROL table]: `customer_entity`
* Seleccione un [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Seleccione una definición: `Age`
* Seleccione un [!UICONTROL column]: `created_at`

* **`Customer's order number`** será creado por un analista como parte de su **[DEFINICIÓN DE LA IGLESIA]** ticket
* **`Is customer's last order`** será creado por un analista como parte de su **[DEFINICIÓN DE LA IGLESIA]** ticket
* **`Seconds since previous order`** será creado por un analista como parte de su **[DEFINICIÓN DE LA IGLESIA]** ticket
* **`Months since order`** será creado por un analista como parte de su **[DEFINICIÓN DE LA IGLESIA]** ticket
* **`Months since previous order`** será creado por un analista como parte de su **[DEFINICIÓN DE LA IGLESIA]** ticket

## Métricas

¡No hay métricas nuevas!

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Probabilidad de pedido de repetición inicial**
* Métrica A: Todos los pedidos repetidos
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Todos los pedidos de tiempo
* [!UICONTROL Metric]: Número de pedidos

* [!UICONTROL Formula]: Probabilidad de pedido de repetición inicial
* 
   [!UICONTROL Fórmula]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Probabilidad de pedido de repetición a partir de meses desde el pedido**
* Métrica A: Repetir pedidos por meses desde el orden anterior (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Últimos pedidos por meses desde el pedido (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Métrica C: Todos los pedidos repetidos (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Grupo por]: `Independent`

* Métrica D: Todos los últimos pedidos (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Grupo por]: `Independent`

* [!UICONTROL Formula]: Probabilidad de pedido de repetición inicial
* 
   [!UICONTROL Fórmula]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostrar arriba.abajo: Principales 24 categorías, ordenadas por nombre de categoría

* 

   [!UICONTROL Chart type]: `Line`

El informe inicial de probabilidad de pedido repetido representa el total de pedidos repetidos/total de pedidos. Todo orden es una oportunidad para repetir el orden; el número de pedidos repetidos es el subconjunto de los que realmente lo hacen.

La fórmula que usamos simplifica a (Total de pedidos repetidos que ocurrieron después de X meses)/ (Total de pedidos que tienen al menos X meses de antigüedad). Nos muestra que históricamente, dado que han pasado X meses desde que se realizó un pedido, hay un Y% de probabilidades de que el usuario realice otro pedido.

Una vez que haya creado su panel, la pregunta más común que recibimos es: ¿Cómo utilizo esto para determinar un umbral de pérdida?

**No hay una respuesta correcta a esto.** Sin embargo, se recomienda encontrar el punto en el que la línea cruza el valor que es la mitad de la tasa de probabilidad de repetición inicial. Este es el punto en el que podemos decir &quot;Si un usuario hubiera hecho un pedido repetido, probablemente lo hubiera hecho ya&quot;. En última instancia, el objetivo es seleccionar el umbral en el que tiene sentido pasar de los esfuerzos de &quot;retención&quot; a los de &quot;reactivación&quot;.

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado final puede ser similar a la imagen de la parte superior de la página

Si tiene alguna pregunta al crear este análisis, o simplemente desea contactar con nuestro equipo de servicios profesionales, [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md).
