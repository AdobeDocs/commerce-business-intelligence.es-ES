---
title: Definir la concentración de clientes
description: Aprenda a configurar un tablero que le ayude a medir cómo se distribuyen los ingresos totales entre la base de clientes.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 0%

---

# Concentración de clientes

En este tema se muestra cómo configurar un tablero que le ayude a medir cómo se distribuyen los ingresos totales entre la base de clientes. Comprenda qué porcentaje de clientes contribuyen con qué porcentaje de ingresos y cree listas segmentadas para comercializar mejor a sus clientes de alta contribución y conservarlos.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Primeros pasos

Primero debe cargar un archivo que contenga solo una clave principal con el valor de una. Esto permite crear algunas columnas calculadas necesarias para el análisis.

Puedes usar [el cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y la imagen siguiente para dar formato al archivo.

## Columnas calculadas

Si se encuentra en la arquitectura original (por ejemplo, si no tiene la opción `Data Warehouse Views` en el menú `Manage Data`), debe ponerse en contacto con el equipo de atención al cliente para crear las columnas siguientes. En la nueva arquitectura, estas columnas se pueden crear desde la página `Manage Data > Data Warehouse`. A continuación se ofrecen instrucciones detalladas.

Se hace una distinción adicional si su negocio permite pedidos de invitados. Si es así, puede omitir todos los pasos de la tabla `customer_entity`. Si no se permiten pedidos de invitado, ignore todos los pasos de la tabla `sales_flat_order`.

Columnas para crear

* `Sales_flat_order/customer_entity` tabla
* (entrada) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **caso cuando A es nulo y luego nulo 1 fin**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` tabla (este es el archivo que subió con el número `1`)
* Número de clientes
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Ruta - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` O `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Columna seleccionada: `sales_flat_order.customer_email` O `customer_entity.entity_id`

* `customer_entity` tabla
* Número de clientes
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Ruta de acceso - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Columna seleccionada: `Number of customers`

* (entrada) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Propietario del evento - `Number of customers`
* Clasificación del evento - `Customer's lifetime revenue`

* Percentil de ingresos del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso cuando A es nulo entonces nulo más (A/B)* 100 fin **
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` tabla
* Número de clientes
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Ruta de acceso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Columna seleccionada: `Number of customers`

* (entrada) Clasificación por ingresos de duración de clientes
* [!UICONTROL Column type]: - `Same table > Event Number`
* Propietario del evento - `Number of customers`
* Clasificación del evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentil de ingresos del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso cuando A es nulo entonces nulo más (A/B)* 100 fin **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>Los percentiles utilizados son incluso divisiones de clientes, que representan el percentil X de la base de clientes. Cada cliente está asociado con un número entero entre 1 y 100, que se puede considerar como sus ingresos de por vida *rank*. Por ejemplo, si el percentil de ingresos del cliente para un cliente específico es **5**, este cliente se encuentra en el ***quinto percentil*** de todos los clientes en términos de ingresos por duración.

## Métricas

* **Valor total de duración de cliente**
* En la tabla `customer_entity`
* Esta métrica arroja una **Sum**
* En la columna `Customer's lifetime revenue`
* Ordenado por la marca de tiempo `Customer's first order date`

## Informes

* **Concentración de clientes**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
  [!UICONTROL Agrupar por]: `Independent`
* Métrica `A`: `Total customer lifetime revenue by percentile`
* Métrica `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Mostrar arriba/abajo: `100% of Customer's revenue percentile Name`
* 
  [!UICONTROL Chart type]: `Line`

* **Concentración del 10% superior**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Métrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
  [!UICONTROL Agrupar por]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Concentración inferior del 50% con una sola compra**

* Métrica `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
  [!UICONTROL Agrupar por]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Concentración inferior del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Métrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Ocultar gráfico
* 
  [!UICONTROL Agrupar por]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar al panel de muestra anterior.

Si tiene alguna pregunta al generar este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
