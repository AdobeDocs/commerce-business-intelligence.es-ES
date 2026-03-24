---
title: Umbral de envío gratuito
description: Aprenda a configurar un tablero que realice un seguimiento del rendimiento de su umbral de envío gratuito.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
TQID: https://experienceleague.adobe.com/dh7Ep6xzBaaeO5LAnsUogg0jSCIXMjv-faBsPyGXpcg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 507
ht-degree: 0%

---

# Envío gratuito

>[!NOTE]
>
>Este tema contiene instrucciones para los clientes que utilizan la arquitectura original y la nueva arquitectura. Se encuentra en la nueva arquitectura si tiene disponible la sección `Data Warehouse Views` después de seleccionar `Manage Data` en la barra de herramientas principal.

En este tema se muestra cómo configurar un tablero que realice un seguimiento del rendimiento de su umbral de envío gratuito. Este panel, que se muestra a continuación, es una buena manera de probar dos umbrales de envío gratuito en A/B. Por ejemplo, es posible que su empresa no esté segura de si debe ofrecer envío gratuito a 50 o 100 dólares. Debe realizar una prueba A/B de dos subconjuntos aleatorios de los clientes y realizar el análisis en [!DNL Commerce Intelligence].

Antes de comenzar, debes identificar dos periodos de tiempo diferentes en los que has tenido valores diferentes para el umbral de envío gratuito de tu tienda.

![Gráfico que muestra el análisis del umbral de envío gratuito y la distribución del valor del pedido](../../assets/free_shipping_threshold.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Si está en la arquitectura original (por ejemplo, si no tiene la opción `Data Warehouse Views` en el menú `Manage Data`), desea ponerse en contacto con el equipo de asistencia para crear las columnas siguientes. En la nueva arquitectura, estas columnas se pueden crear desde la página `Manage Data > Data Warehouse`. A continuación se ofrecen instrucciones detalladas.

* **`sales_flat_order`** tabla
   * Este cálculo crea bloques en incrementos en relación con los tamaños de carro habituales. Esto puede variar entre incrementos, incluidos, 5, 10, 50, 100

* Arquitectura original de **`Order subtotal (buckets)`**: creada por un analista como parte de su vale de `[FREE SHIPPING ANALYSIS]`
* **`Order subtotal (buckets)`** nueva arquitectura:
   * Como se ha mencionado anteriormente, este cálculo crea bloques en incrementos en relación con los tamaños típicos del carro de compras. Si tiene una columna nativa de subtotales como `base_subtotal`, se puede usar como base para esta nueva columna. Si no es así, puede ser una columna calculada que excluya los gastos de envío y los descuentos de los ingresos.

  >[!NOTE]
  >
  >Los tamaños del &quot;cubo&quot; dependen de lo que sea apropiado para usted como cliente. Puede comenzar con su `average order value` y crear algunos contenedores menores y mayores que esa cantidad. Al consultar el cálculo siguiente, puede ver cómo copiar fácilmente parte de la consulta, editarla y crear bloques adicionales. El ejemplo se realiza en incrementos de 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` o `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
cuando `A< 200` y `A <= 250` entonces `201 - 250`
cuando `A<251` y `A<= 300` entonces `251 - 300`
cuando `A<301` y `A<= 350` entonces `301 - 350`
cuando `A<351` y `A<=400` entonces `351 - 400`
cuando `A<401` y `A<=450` entonces `401 - 450`
else &#39;más de 450&#39;
fin


## Métricas

No hay métricas nuevas!!!

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

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
  >Puede cortar la cola mostrando los `X` `sorted by` `Order subtotal` (contenedores) superiores en `Show top/bottom`.

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
