---
title: Umbral de envío gratuito
description: Aprenda a configurar un tablero que rastree el rendimiento de su umbral de envío gratuito.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Envío gratuito

>[!NOTE]
>
>Este artículo contiene instrucciones para clientes que utilizan la arquitectura original y la nueva arquitectura. Se encuentra en la nueva arquitectura si tiene la sección &quot;Vistas de Data Warehouse&quot; disponible después de seleccionar &quot;Administrar datos&quot; en la barra de herramientas principal.

En este artículo, demostramos cómo configurar un tablero que rastree el rendimiento de su umbral de envío gratuito. Este tablero, que se muestra a continuación, es una buena manera de probar A/B con dos umbrales de envío libres diferentes. Por ejemplo, es posible que su empresa no esté segura de si debe ofrecer envío gratuito a 50 o 100 dólares. Debe realizar una prueba A/B de dos subconjuntos aleatorios de sus clientes y realizar el análisis en [!DNL MBI].

Antes de comenzar, debe identificar dos períodos de tiempo distintos en los que haya tenido valores diferentes para el umbral de envío gratuito de su tienda.

![](../../assets/free_shipping_threshold.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Si se encuentra en la arquitectura original (por ejemplo, si no tiene la variable `Data Warehouse Views` en la `Manage Data` ), le recomendamos que se ponga en contacto con nuestro equipo de asistencia para crear las columnas siguientes. En la nueva arquitectura, estas columnas se pueden crear desde la variable `Manage Data > Data Warehouse` página. A continuación se proporcionan instrucciones detalladas.

* **`sales_flat_order`** tabla
   * Este cálculo crea bloques en incrementos en relación con los tamaños de carro habituales. Esto puede variar desde incrementos, incluidos, 5, 10, 50, 100

* **`Order subtotal (buckets)`** Arquitectura original: será creado por un analista como parte de su `[FREE SHIPPING ANALYSIS]` ticket
* **`Order subtotal (buckets)`** Nueva arquitectura:
   * Como se ha mencionado anteriormente, este cálculo crea bloques en incrementos en relación con los tamaños de carro habituales. Si tiene una columna de subtotal nativa como `base_subtotal`, que puede utilizarse como base de esta nueva columna. Si no es así, puede ser una columna calculada que excluya el envío y los descuentos de los ingresos.
   >[!NOTE]
   >
   >Los tamaños &quot;contenedores&quot; dependerán de lo que sea apropiado para usted como cliente. Podría comenzar con su `average order value` y cree un cierto número de bloques menor que y bueno que esa cantidad. Al consultar el cálculo siguiente, verá cómo copiar fácilmente parte de la consulta, editarla y crear bloques adicionales. El ejemplo se realiza en incrementos de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`o `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
when `A< 200` y `A <= 250` then `201 - 250`
when `A<251` y `A<= 300` then `251 - 300`
when `A<301` y `A<= 350` then `301 - 350`
when `A<351` y `A<=400` then `351 - 400`
when `A<401` y `A<=450` then `401 - 450`
else &#39;over 450&#39; end



## Métricas

¡¡¡No hay métricas nuevas!!

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Valor de pedido promedio con la regla de envío A**
   * [!UICONTROL Metric]: `Average order value`

* Métrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Número de pedidos por subtotales con la regla de envío A**
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

* **Porcentaje de pedidos por subtotal con la regla de envío A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL Grupo por]: `Independent`
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

* **Porcentaje de pedidos con subtotal que excede la regla de envío A**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Grupo por]: `Independent`

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

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado final puede ser similar a la imagen de la parte superior de esta página.
