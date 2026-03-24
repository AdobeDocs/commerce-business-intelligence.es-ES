---
title: Diagramas de relación de entidad
description: Obtenga información acerca de algunos diagramas ER para ayudarle a visualizar la relación entre un puñado de tablas comunes de bases de datos de Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/pWd5aVoaq2TPkGr37cNeF8CEZ63fItwCEez61eEgGBo
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 346
ht-degree: 0%

---

# Diagrama de relación de entidad

¿Qué es un **[!UICONTROL entity relationship (ER) diagram]**? Un diagrama [!UICONTROL ER] es una visualización de las tablas de una base de datos y de cómo se relacionan entre sí. Este tema contiene algunos diagramas de [!UICONTROL ER] que le ayudarán a visualizar la relación entre algunas tablas comunes de bases de datos de Adobe Commerce.

>[!NOTE]
>
>A lo largo de este tema, verá las palabras **join**, **relation** y **path**. Todas estas palabras se utilizan para describir cómo se conectan dos tablas.

## Diagrama de Core Commerce [!UICONTROL ER]

![4_DB_Chart](../../assets/4_DB_Chart.png)

Este diagrama `ER` representa las relaciones entre las tablas principales de una base de datos de Commerce. Al ver varias relaciones a la vez, puede ver cómo se relacionan los datos en muchas tablas.

Las secciones siguientes contienen `ER` diagramas específicos de dos tablas a la vez. Para ver un diagrama y la descripción que lo acompaña, haga clic en el encabezado de esa sección.

## `customer\_entity & sales\_flat\_order`

![Un cliente tiene muchos pedidos](../../assets/2_OneCustomerManyOrders.png)

Un cliente puede realizar muchos pedidos. La relación entre estas dos tablas es `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` no es igual a `sales\_flat\_order.entity\_id`. El primero se puede considerar como `customer\_id` y el segundo como `order\_id.`

En [!DNL Commerce Intelligence], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, se define de la siguiente manera:

![Diagrama de relación de entidad que muestra la ruta de sales_plain_order a customer_entity](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un pedido puede contener muchos elementos. La relación entre estas dos tablas es `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

En [!DNL Commerce Intelligence], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, defina la ruta como se muestra a continuación.

![Diagrama de relación de entidad que muestra la ruta de sales_flat_order_item a sales_flat_order](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un producto se puede comprar muchos artículos. La relación entre estas dos tablas es `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

En [!DNL Commerce Intelligence], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse. Cuando esté listo para crear la ruta, defina la ruta como se muestra a continuación.

![Diagrama de relación de entidad que muestra la ruta de sales_plain_order_item a catalog_product_entity](../../assets/SFOI___CPE_path.png)
