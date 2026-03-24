---
title: Definir cancelación de cliente
description: Aprenda a configurar un tablero que le ayude a definir la pérdida para sus clientes transaccionales.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/eDJBh7FlhuKjBa5ft4sqAfZavmBk4V9m-Iu-26cG2VI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 482
ht-degree: 0%

---

# Cancelación de cliente transaccional

En este tema se muestra cómo configurar un tablero que le ayuda a definir la pérdida para sus clientes transaccionales.

![Panel de cancelación de cliente que muestra la tasa de cancelación y las métricas de retención](../../assets/churn-deashboard.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Columnas para crear

* `customer_entity` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: `Count`
* Seleccionar un(a) [!UICONTROL table]: `sales_flat_order`
* Seleccionar un(a) [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_plain_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Pedidos que se cuentan

* `sales_flat_order` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: Columna combinada
* Seleccionar un(a) [!UICONTROL table]: `customer_entity`
* Seleccionar un(a) [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Seleccione una definición: `Age`
* Seleccionar un(a) [!UICONTROL column]: `created_at`

* Un analista ha creado **`Customer's order number`** como parte de su vale **[DEFINIENDO CANCELACIÓN]**
* Un analista ha creado **`Is customer's last order`** como parte de su vale **[DEFINIENDO CANCELACIÓN]**
* Un analista ha creado **`Seconds since previous order`** como parte de su vale **[DEFINIENDO CANCELACIÓN]**
* Un analista ha creado **`Months since order`** como parte de su vale **[DEFINIENDO CANCELACIÓN]**
* Un analista ha creado **`Months since previous order`** como parte de su vale **[DEFINIENDO CANCELACIÓN]**

## Métricas

No hay métricas nuevas.

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Probabilidad de orden de repetición inicial**
* Métrica A: Pedidos repetidos de todo el tiempo
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Pedidos permanentes
* [!UICONTROL Metric]: número de pedidos

* [!UICONTROL Formula]: probabilidad de orden repetido inicial
* 
  [!UICONTROL Fórmula]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Probabilidad de repetición de pedido dada meses desde la solicitud**
* Métrica A: Repetir pedidos por meses desde el pedido anterior (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: últimos pedidos por meses desde el pedido (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Métrica C: Todos los pedidos repetidos (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 
  [!UICONTROL Agrupar por]: `Independent`

* ID de métrica: últimos pedidos permanentes (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 
  [!UICONTROL Agrupar por]: `Independent`

* [!UICONTROL Formula]: probabilidad de orden repetido inicial
* 
  [!UICONTROL Fórmula]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostrar top.bottom: Las 24 categorías principales, ordenadas por nombre de categoría

* 
  [!UICONTROL Chart type]: `Line`

El informe de probabilidad de pedido repetido inicial representa el total de pedidos repetidos/total de pedidos. Cada pedido es una oportunidad para hacer un pedido repetido; el número de pedidos repetidos es el subconjunto de los que realmente lo hacen.

La fórmula que utiliza simplifica a (Total de pedidos repetidos que se produjeron después de X meses)/ (Total de pedidos que tienen al menos X meses de antigüedad). Nos muestra que históricamente, dado que han pasado X meses desde un pedido, hay un Y% de probabilidad de que el usuario realice otro pedido.

Una vez que haya creado su panel, la pregunta más común es: ¿Cómo utilizo esto para determinar un umbral de pérdida?

**No hay &quot;una respuesta correcta&quot; para esto.** Sin embargo, Adobe recomienda encontrar el punto en el que la línea cruza el valor que es la mitad de la tasa de probabilidad de repetición inicial. Este es el punto en el que puede decir &quot;Si un usuario va a hacer un pedido repetido, probablemente ya lo habría hecho&quot;. En última instancia, el objetivo es seleccionar el umbral en el que tiene sentido cambiar de los esfuerzos de &quot;retención&quot; a &quot;reactivación&quot;.

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar a la imagen de la parte superior de la página

Si tiene alguna pregunta al generar este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
