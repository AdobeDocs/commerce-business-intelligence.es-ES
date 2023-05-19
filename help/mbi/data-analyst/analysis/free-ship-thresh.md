---
title: Umbral de envío gratuito
description: Aprenda a configurar un tablero que realice un seguimiento del rendimiento de su umbral de envío gratuito.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Envío gratuito

>[!NOTE]
>
>Este tema contiene instrucciones para los clientes que utilizan la arquitectura original y la nueva arquitectura. Se encuentra en la nueva arquitectura si tiene el `Data Warehouse Views` disponible tras seleccionar `Manage Data` en la barra de herramientas principal.

En este tema se muestra cómo configurar un tablero que realice un seguimiento del rendimiento de su umbral de envío gratuito. Este panel, que se muestra a continuación, es una buena forma de probar los dos umbrales de envío gratuito de la prueba A/B. Por ejemplo, es posible que su empresa no esté segura de si debe ofrecer envío gratuito a 50 o 100 dólares. Debe realizar una prueba A/B de dos subconjuntos aleatorios de sus clientes y realizar el análisis en [!DNL Commerce Intelligence].

Antes de comenzar, debes identificar dos periodos de tiempo diferentes en los que has tenido valores diferentes para el umbral de envío gratuito de tu tienda.

![](../../assets/free_shipping_threshold.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Si se basa en la arquitectura original (por ejemplo, si no tiene el `Data Warehouse Views` en la opción `Manage Data` ), desea ponerse en contacto con el equipo de asistencia para crear las columnas siguientes. En la nueva arquitectura, estas columnas se pueden crear desde el `Manage Data > Data Warehouse` página. A continuación se ofrecen instrucciones detalladas.

* **`sales_flat_order`** tabla
   * Este cálculo crea bloques en incrementos en relación con los tamaños de carro habituales. Esto puede variar entre incrementos, incluidos, 5, 10, 50, 100

* **`Order subtotal (buckets)`** Arquitectura original: creada por un analista como parte de su `[FREE SHIPPING ANALYSIS]` boleto
* **`Order subtotal (buckets)`** Nueva arquitectura:
   * Como se ha mencionado anteriormente, este cálculo crea bloques en incrementos en relación con los tamaños típicos del carro de compras. Si tiene una columna nativa de subtotales como `base_subtotal`, que puede utilizarse como base para esta nueva columna. Si no es así, puede ser una columna calculada que excluya los gastos de envío y los descuentos de los ingresos.
   >[!NOTE]
   >
   >Los tamaños del &quot;cubo&quot; dependen de lo que sea apropiado para usted como cliente. Podrías empezar con tu `average order value` y cree algunos bloques inferiores y buenos a esa cantidad. Al consultar el cálculo siguiente, verá cómo copiar fácilmente parte de la consulta, editarla y crear bloques adicionales. El ejemplo se realiza en incrementos de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, o `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
cuándo cuando `A< 200` y `A <= 250` entonces `201 - 250`
cuando `A<251` y `A<= 300` entonces `251 - 300`
cuando `A<301` y `A<= 350` entonces `301 - 350`
cuando `A<351` y `A<=400` entonces `351 - 400`
cuando `A<401` y `A<=450` entonces `401 - 450`
else &#39;over 450&#39; end



## Métricas

No hay métricas nuevas!!!

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Valor de pedido promedio con regla de envío A**
   * [!UICONTROL Metric]: `Average order value`

* Métrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Número de pedidos por bloques de subtotales con regla de envío A**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >Puede cortar el extremo de la cola mostrando la parte superior `X` `sorted by` `Order subtotal` (contenedores) en el `Show top/bottom`.

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **Porcentaje de pedidos por subtotal con regla de envío A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL Agrupar por]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* Métrica `A`: `Number of orders by subtotal (hide)`
* Métrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **Porcentaje de pedidos con un subtotal que supera la regla de envío A**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Agrupar por]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* Métrica `A`: `Number of orders by subtotal`
* Métrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


Repita los pasos e informes anteriores para el envío B y el período de tiempo con la regla de envío B.

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar a la imagen de la parte superior de esta página.
