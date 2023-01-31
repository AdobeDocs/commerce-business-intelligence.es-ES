---
title: Rendimiento del cupón
description: Obtenga más información sobre el análisis del rendimiento del cupón.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Análisis avanzado del código de cupón

Comprender el rendimiento de los cupones de su negocio es una forma interesante de segmentar sus pedidos y también comprender mejor a sus clientes. Este artículo le explica paso a paso la creación de análisis para comprender qué clientes adquiere mediante el uso de cupones, cómo funcionan y cómo rastrean el uso general de cupones.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Introducción

Como primer paso, debe asegurarse de que las siguientes columnas se sincronizan con la Data Warehouse. Si no lo son, continúe y rastree las variables, navegando a &quot;Administrar datos&quot; > &quot;Data Warehouse&quot; y sincronizando lo siguiente:

* **sales\_plana\_order** tabla
* **coupon\_code**
* **base\_descuento\_amount**

## Columnas calculadas

Columnas que se van a crear independientemente de la política de pedidos de invitados:

* `sales\_flat\_order` tabla
* **¿Se ha aplicado el cupón del pedido?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:: caso cuando `A` es nulo entonces `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - código de cupón**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]:: Cadena
   * [!UICONTROL Calculation]:: `concat(A,' - ',B)`


* **Número de pedidos con este cupón**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Propietario del evento:`INPUT customer_id - coupon code`
   * Clasificación del evento: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` conjunto de filtros

Columnas adicionales que crear si los pedidos de invitados NO son compatibles:

* `customer\_entity` tabla
   * **¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Seleccione un [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **Cupón del primer pedido del cliente**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleccione un [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **Número de cupones utilizado por el cliente durante toda la vida**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **Cliente que adquiere cupones o cliente que no adquiere cupones**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]:: **caso en el que A=&#39;Coupon&#39; then &#39;Coupon acquisition customer&#39; else &#39;Non coupon acquisition customer&#39; end**
   * **Porcentaje de pedidos del cliente con cupón**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]:: `Decimal`
      * [!UICONTROL Calculation]:: **caso en el que A es nulo o B es nulo o B=0, entonces nulo si no es final A/B**
   * **Uso de cupones del cliente**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]:: `String`
      * [!UICONTROL Calculation]:: **caso en el que A es nulo, entonces nulo cuando A=0 entonces &#39;Nunca se usó cupón&#39; cuando A&lt;0.5 entonces &#39;Precio mayoritario completo&#39; cuando A=0.5 entonces &#39;50/50&#39; cuando A=1 entonces &#39;Solo cupones&#39; cuando A>0.5 y luego &#39;Cupón mayoritario&#39; si no &#39;No definido&#39; finalizan**









* `sales\_flat\_order` tabla
   * **¿El primer pedido del cliente incluye cupón? (Cupón/Sin cupón)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleccione un [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **Cupón del primer pedido del cliente**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleccione un [!UICONTROL column]: `Customer's first order coupon?`


Columnas adicionales que crear si los pedidos de invitados NO son compatibles:

* `sales\_flat\_order` tabla
   * **¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón)** **-** creado por un analista como parte de su ticket \[COUPON ANALYSIS\]
   * **Cupón del primer pedido del cliente**{:}**-** creado por un analista como parte de su ticket \[COUPON ANALYSIS\]

* **Número de cupones utilizado por el cliente durante toda la vida**{:}**-** creado por un analista como parte de su ticket \[COUPON ANALYSIS\]
* **Cliente que adquiere cupones o cliente que no adquiere cupones**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:: **caso en el que A=&#39;Coupon&#39; then &#39;Coupon acquisition customer&#39; else &#39;Non coupon acquisition customer&#39; end**


* **Porcentaje de pedidos del cliente con cupón**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]:: `Decimal`
   * [!UICONTROL Calculation]:: **caso en el que A es nulo o B es nulo o B=0, entonces nulo si no es final A/B**


* **Uso de cupones del cliente**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]:: `String`
   * [!UICONTROL Calculation]:: **caso en el que A es nulo, entonces nulo cuando A=0 entonces &#39;Nunca se usó cupón&#39; cuando A&lt;0.5 entonces &#39;Precio mayoritario completo&#39; cuando A=0.5 entonces &#39;50/50&#39; cuando A=1 entonces &#39;Solo cupones&#39; cuando A>0.5 y luego &#39;Cupón mayoritario&#39; si no &#39;No definido&#39; finalizan**


## Métricas

* **Importe de descuento de cupón**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* En el `sales\_flat\_order` tabla
* Esta métrica realiza una **Sum**
* En el `discount\_amount` column
* Solicitado por el `created\_at` timestamp
* [!UICONTROL Filter]:

* **Número de cupones utilizados**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* En el `sales\_flat\_order` tabla
* Esta métrica realiza una **Recuento**
* En el `entity\_id` column
* Solicitado por el `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **% de los clientes de cupones adquiridos y no de cupones**
   * [!UICONTROL Metric]: `New customers`

* Métrica `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` o `Non coupon acquisition customer`
* 

   [!UICONTROL Tipo de gráfico]: `Pie`

* **Número de clientes adquiridos con cupones y no adquiridos con cupones**
   * [!UICONTROL Metric]: `New customers`

* Métrica A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` o `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Ingresos medios de duración: Cupón Acq. (90+ días de edad)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Cupón

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Ingresos medios de duración: Acq. sin cupones (90+ días de edad)**
   * [!UICONTROL Metric]: Ingresos medios de duración
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Sin cupón

* Métrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Media de ingresos por vida útil por cupón de primer pedido**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Métrica `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL Tipo de gráfico]: `Column`

>[!NOTE]
>
>Si tiene un gran número de códigos de cupones, como hacen muchos de nuestros clientes, querrá aplicar un Top/Bottom como Top 10 ordenado por un promedio de ingresos de duración

* **Probabilidad de repetición de pedido: Adquisiciones de cupones**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Cupón
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Cupón
      * ¿Es el último pedido del cliente? = No
   * 
      [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Seleccione un número estadísticamente significativo de `Customer's by lifetime orders` gráfico. Al mirar el gráfico, como una buena regla, normalmente buscamos números de pedido con 30 o más clientes en el grupo. En función del conjunto de datos, puede ser un número elevado, por lo que puede añadir de 1 a 10.


* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilidad de repetición de pedido: Adquisiciones que no son de cupones**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Sin cupón
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * El primer pedido del cliente incluía un cupón (cupón/sin cupón) = Sin cupón
      * ¿Es el último pedido del cliente? = No
   * 
      [!UICONTROL Fórmula]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Seleccione un número estadísticamente significativo de `Customer's by lifetime orders` para 1-5.



* Métrica `A`: `Number of orders`
* Métrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Tasa de uso de cupones de clientes adquiridos con cupones (pedidos repetidos)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente que adquiere cupones o Cliente que no adquiere cupones = Adquisición de cupones
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente > 1
      * ¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón) = Cupón
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente > 1
      * ¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón) = Cupón
      * ¿Se ha aplicado el cupón del pedido? (Cupón/Sin cupón) = Cupón
   * 
      [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Métrica `A`: `Coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Table` (puede transponer esta tabla para una mejor visualización)

* **Tasa de uso de cupones de clientes no adquiridos mediante cupones (pedidos repetidos)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Cliente que adquiere cupones o Cliente que no adquiere cupones = Adquisición sin cupón
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente > 1
      * ¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón) = Sin cupón
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente > 1
      * ¿El primer pedido del cliente incluyó un cupón? (Cupón/Sin cupón) = Sin cupón
      * ¿Se ha aplicado el cupón del pedido? (Cupón/Sin cupón) = Cupón
   * 
      [!UICONTROL Fórmula]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Métrica `A`: `Non-coupon-acquired customers`
* Métrica `B`: `Number of repeat orders`
* Métrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Table` (puede transponer esta tabla para una mejor visualización)

* **Detalles de uso de cupones (pedidos por primera vez)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente = 1
      * Número de pedidos con este cupón > 10
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente = 1
      * Número de pedidos con este cupón > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente = 1
      * Número de pedidos con este cupón > 10
   * [!UICONTROL Formula]: `B-C` (si C es negativo); B+C (si C es positivo)
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número de pedido del cliente = 1
      * Número de pedidos con este cupón > 10




* Métrica `A`: `First time orders (FTO)`
* Métrica `B`: `Revenue from FTO`
* Métrica `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Métrica `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL Tipo de gráfico]: `Table`
>[!NOTE]
>
>La cantidad de 10 para &quot;Número de pedidos con este cupón&quot; es arbitraria. No dude en utilizar la cantidad más adecuada para este filtro.

* **Número de pedidos con cupón (todo el tiempo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Ingresos netos de pedidos con cupones (todo el tiempo)**
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * ¿Se ha aplicado el cupón del pedido? (Cupón/Sin cupón) = Cupón

* Métrica `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Descuentos de cupones (todo el tiempo)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Métrica `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Número de pedidos con y sin cupones**
   * [!UICONTROL Metric]: `Number of orders`

* Métrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Uso de cupones entre usuarios repetidos**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Número de pedidos de duración > 1 del cliente

* Métrica `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL Tipo de gráfico]: `Pie`

* **Detalles de uso del cupón**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Número de pedidos con este cupón > 10
   * 
      [!UICONTROL Métrica]: `Revenue`
   * [!UICONTROL Filter]:
      * Número de pedidos con este cupón > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Número de pedidos con este cupón > 10
   * [!UICONTROL Formula]: `B-C` (si `C` es negativo); `B+C` (si `C` es positivo)
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (si `C` es negativo); `C/(B+C)` (si `C` es positivo)
   * 

      [!UICONTROL Formato]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Número de pedidos con este cupón > 10
   * 
      [!UICONTROL Fórmula]: `C/A`
   * 

      [!UICONTROL Formato]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Número de pedidos con este cupón > 10





* Métrica `A`: `Number of orders`
* Métrica `B`: `Net revenue from orders`
* Métrica `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Métrica `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Métrica `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL Tipo de gráfico]: `Table`

>[!NOTE]
>
>La cantidad de 10 para &quot;Número de pedidos con este cupón&quot; es arbitraria. No dude en utilizar la cantidad más adecuada para este filtro.

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado final puede ser similar a la imagen situada en la parte superior de la página.

Si tiene alguna pregunta al crear este análisis, o simplemente desea contactar con nuestro equipo de servicios profesionales, [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md).
