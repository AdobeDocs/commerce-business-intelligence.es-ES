---
title: Diagramas de relación de entidades
description: Obtenga información sobre algunos diagramas ER para ayudarle a visualizar la relación entre un puñado de tablas comunes de bases de datos de Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Diagrama de relación de entidades

¿Qué es un **[!UICONTROL entity relationship (ER) diagram]**? Un `ER` diagrama es una visualización de tablas dentro de una base de datos y cómo se relacionan entre sí. Este artículo contiene algunos diagramas ER para ayudarle a visualizar la relación entre un puñado de tablas comunes de bases de datos de Commerce.

>[!NOTE]
>
>A lo largo de este artículo verá las palabras **join**, **relación** y **ruta**. Estas palabras se utilizan para describir cómo están conectadas dos tablas.

## Comercio principal `ER` Diagrama

![4_DB_Chart](../../assets/4_DB_Chart.png)

Esta `ER` diagrama representa las relaciones entre las tablas principales de una base de datos de Commerce. Al ver varias relaciones a la vez, puede ver cómo se relacionarían los datos en muchas tablas.

Las secciones siguientes contienen `ER` diagramas específicos de dos tablas a la vez. Para ver un diagrama y su descripción adjunta, haga clic en el encabezado de esa sección.

## `customer\_entity & sales\_flat\_order`

![Un cliente hace muchos pedidos](../../assets/2_OneCustomerManyOrders.png)

Un cliente puede realizar muchos pedidos. La relación entre estas dos tablas es `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` no es igual a `sales\_flat\_order.entity\_id`. La primera se puede considerar como un `customer\_id` y la segunda se puede considerar como un `order\_id.` Puede leer más sobre esto en la [`entity\_id` sección](https://support.magento.com/hc/en-us/articles/360016729951) de _[!DNL Magento]: Conceptos erróneos comunes_ artículo.

Within [!DNL MBI], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse . Cuando esté listo para crear la ruta, se definirá de la siguiente manera:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un pedido puede contener muchos elementos. La relación entre estas dos tablas es `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL MBI], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse . Cuando esté listo para crear la ruta, se definirá de la siguiente manera:

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Se puede comprar un producto con muchos artículos. La relación entre estas dos tablas es `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL MBI], si la ruta entre estas dos tablas no existe, puede [crear la ruta](../data-warehouse-mgr/create-paths-calc-columns.md) en la pestaña Data Warehouse . Cuando esté listo para crear la ruta, se definirá de la siguiente manera:

![](../../assets/SFOI___CPE_path.png)
