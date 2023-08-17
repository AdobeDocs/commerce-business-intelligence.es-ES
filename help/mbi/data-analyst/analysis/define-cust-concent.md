---
title: Definir la concentración de clientes
description: Aprenda a configurar un tablero que le ayude a medir cómo se distribuyen los ingresos totales entre la base de clientes.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Concentración de clientes

En este tema se muestra cómo configurar un tablero que le ayude a medir cómo se distribuyen los ingresos totales entre la base de clientes. Comprenda qué porcentaje de clientes contribuyen con qué porcentaje de ingresos y cree listas segmentadas para comercializar mejor a sus clientes de alta contribución y conservarlos.

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Primeros pasos

Primero debe cargar un archivo que contenga solo una clave principal con el valor de una. Esto permite crear algunas columnas calculadas necesarias para el análisis.

Puede utilizar [el cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y la imagen siguiente para dar formato al archivo.

## Columnas calculadas

Si se basa en la arquitectura original (por ejemplo, si no tiene el `Data Warehouse Views` en la opción `Manage Data` ), desea ponerse en contacto con el equipo de asistencia para crear las columnas siguientes. En la nueva arquitectura, estas columnas se pueden crear desde el `Manage Data > Data Warehouse` página. A continuación se ofrecen instrucciones detalladas.

Se hace una distinción adicional si su negocio permite pedidos de invitados. Si es así, puede ignorar todos los pasos de `customer_entity` tabla. Si no se permiten pedidos de invitado, ignore todos los pasos para la `sales_flat_order` tabla.

Columnas para crear

* `Sales_flat_order/customer_entity` tabla
* (entrada) `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]: - **Caso de que A sea nulo y luego nulo fin de else 1**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` tabla (este es el archivo que cargó con el número `1`)
* Número de clientes
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* Ruta - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` O `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Columna seleccionada - `sales_flat_order.customer_email` O `customer_entity.entity_id`

* `customer_entity` tabla
* Número de clientes
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Ruta - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Columna seleccionada - `Number of customers`

* (entrada) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* Propietario del evento - `Number of customers`
* Clasificación del evento - `Customer's lifetime revenue`

* Percentil de ingresos del cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **Caso en el que A es nulo y luego nulo (A/B)* Fin de 100 **
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` tabla
* Número de clientes
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Ruta - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Columna seleccionada - `Number of customers`

* (entrada) Clasificación por ingresos de duración de clientes
* [!UICONTROL Column type]: – `Same table > Event Number`
* Propietario del evento - `Number of customers`
* Clasificación del evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentil de ingresos del cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **Caso en el que A es nulo y luego nulo (A/B)* Fin de 100 **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>Los percentiles utilizados son incluso divisiones de clientes, que representan el percentil X de la base de clientes. Cada cliente está asociado con un número entero entre 1 y 100, que se puede considerar como sus ingresos de duración *clasificar*. Por ejemplo, si el percentil de ingresos del cliente para un cliente específico es **5**, este cliente se encuentra en ***percentil 5*** de todos los clientes en términos de ingresos por duración.

## Métricas

* **Valor total de duración del cliente**
* En el `customer_entity` tabla
* Esta métrica realiza una **Sum**
* En el `Customer's lifetime revenue` columna
* Ordenado por el `Customer's first order date` timestamp

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

* **Concentración del 10 % superior**
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

Si tiene alguna pregunta mientras realiza este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
