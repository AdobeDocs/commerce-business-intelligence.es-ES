---
title: Diagramas de relación de entidad
description: Obtenga información acerca de algunos diagramas de ER para ayudarle a visualizar la relación entre un puñado de tablas comunes de bases de datos de Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Diagrama de relación de entidad

¿Qué es un? **[!UICONTROL entity relationship (ER) diagram]**? Un [!UICONTROL ER] el diagrama es una visualización de las tablas de una base de datos y de cómo se relacionan entre sí. Este tema contiene algunos [!UICONTROL ER] diagramas para ayudarle a visualizar la relación entre algunas tablas comunes de bases de datos de Adobe Commerce.

>[!NOTE]
>
>A lo largo de este tema, verá las palabras **unirse**, **parentesco**, y **ruta**. Todas estas palabras se utilizan para describir cómo se conectan dos tablas.

## Commerce principal [!UICONTROL ER] Diagrama

![Gráfico_DB_4](../../assets/4_DB_Chart.png)

Esta `ER` Un diagrama representa las relaciones entre las tablas principales de una base de datos de Commerce. Al ver varias relaciones a la vez, puede ver cómo se relacionan los datos en muchas tablas.

Las secciones siguientes contienen `ER` Diagramas específicos de dos tablas a la vez. Para ver un diagrama y la descripción que lo acompaña, haga clic en el encabezado de esa sección.

## `customer\_entity & sales\_flat\_order`

![Un cliente, varios pedidos](../../assets/2_OneCustomerManyOrders.png)

Un cliente puede realizar muchos pedidos. La relación entre estas dos tablas es `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` no es igual a `sales\_flat\_order.entity\_id`. La primera puede considerarse como una `customer\_id` y el segundo puede ser considerado como un `order\_id.`

En [!DNL Commerce Intelligence]Sin embargo, si la ruta entre estas dos tablas no existe, puede [creación de la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, se define de la siguiente manera:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un pedido puede contener muchos elementos. La relación entre estas dos tablas es `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

En [!DNL Commerce Intelligence]Sin embargo, si la ruta entre estas dos tablas no existe, puede [creación de la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, defina la ruta como se muestra a continuación.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un producto se puede comprar muchos artículos. La relación entre estas dos tablas es `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

En [!DNL Commerce Intelligence]Sin embargo, si la ruta entre estas dos tablas no existe, puede [creación de la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, defina la ruta como se muestra a continuación.

![](../../assets/SFOI___CPE_path.png)
