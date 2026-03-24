---
title: Análisis de Niveles de Inventario
description: Obtenga información sobre cómo analizar los niveles de inventario.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Developer, User
feature: Dashboards, Reports
TQID: https://experienceleague.adobe.com/z2NS33cMO3wETk6FFyI-rkbPkWxxw2zYxUUjdC4zRa4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c1579802-ddd4-4214-8a91-97b2066abe11id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# Analizar niveles de inventario

En este tema se muestra cómo configurar un tablero que proporciona información sobre el inventario actual y contiene instrucciones para los clientes sobre la arquitectura heredada o la nueva arquitectura. Se encuentra en la arquitectura heredada si no tiene la opción **[!UICONTROL Data Warehouse Views]** en el menú **[!UICONTROL Manage Data]**. Si usa la arquitectura heredada, envíe una [nueva solicitud de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) con el asunto **[!UICONTROL INVENTORY ANALYSIS]** una vez que llegue a la sección designada en las instrucciones de _Columnas calculadas_ a continuación.

## Columnas para rastrear:

### Columnas para seguir instrucciones

* **[!UICONTROL cataloginventory_stock_item]** tabla:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** tabla:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Columnas calculadas:

+++ Nueva arquitectura

* **[!UICONTROL catalog_product_entity]** tabla:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * Seleccionar [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * Definición:
         * Caso de uso cuando A es nulo o B es nulo y luego nulo más redondo(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) final

* **[!UICONTROL cataloginventory_stock_item]** tabla:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] entradas:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * Definición:
         * caso cuando A es nulo o B es nulo o B = 0,0 entonces nulo otro redondeo (A::decimal/B,2) fin

+++
+++ Arquitectura heredada

* **[!UICONTROL catalog_product_entity]** tabla:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * Seleccionar columna DATETIME: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Seleccionar un(a) [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Creado por un analista cuando envía su solicitud de soporte de **[ANÁLISIS DE INVENTARIO]**

* **[!UICONTROL cataloginventory_stock_item]** tabla:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleccionar un(a) [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Creado por un analista cuando el archivo envía su solicitud de soporte de **[!UICONTROL INVENTORY ANALYSIS]**

+++

## Métricas

### Instrucciones de métricas

* **[!UICONTROL cataloginventory_stock_item]** tabla:
   * **`Inventory on hand`**: esta métrica realiza una
      * **Sum** en el
      * **`qty`** columna ordenada por
      * Columna [None]

## Informes

### Instrucciones del informe

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Intervalo de tiempo: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * Intervalo de tiempo: `None`
   * 
     [!UICONTROL Agrupar por]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * Intervalo de tiempo: `None`
   * 
     [!UICONTROL Agrupar por]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

Si tiene alguna pregunta al generar este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
