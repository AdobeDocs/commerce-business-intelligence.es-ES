---
title: Comprensión y compilación de análisis básicos
description: Aprenda a comprender y crear análisis básicos.
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '3113'
ht-degree: 0%

---

# Análisis básico

Una vez que conozca el [!DNL Adobe Commerce Intelligence] y tenga una comprensión básica de la herramienta, querrá empezar a crear informes. Una de las preguntas más comunes que puede hacerse es &quot;¿Qué debería estar mirando?&quot;

La siguiente información describe algunas de las métricas e informes comunes que pueden ser útiles. Algunos de estos informes existen en su cuenta, por lo que asegúrese de revisar las métricas y los informes que existen dentro de su cuenta para evitar la creación de duplicados.

## Tablas y columnas que desea comprender

Al crear una métrica, debe conocer cuatro datos:

1. La tabla en la que se encuentran los datos,
1. La acción específica que desea realizar,
1. La columna en la que desea realizar esa acción y
1. La marca de tiempo que desee utilizar para realizar el seguimiento de esos datos.

Lo más probable es que los nombres de las tablas utilizadas en estos ejemplos sean ligeramente diferentes de los nombres de las columnas y tablas de la base de datos, ya que cada base de datos es única. Consulte las definiciones siguientes si necesita ayuda para identificar una tabla o columna correspondiente en la base de datos.

## Tabla Customers

Esta tabla contiene la información clave sobre cada cliente, como un ID de cliente único, una dirección de correo electrónico, etc. Los ejemplos siguientes utilizan **[!UICONTROL customer_entity]** como el nombre de una tabla cliente de ejemplo.

Si algunos de estos cálculos no existen actualmente en la base de datos, cualquier usuario administrador de la cuenta puede crearlos. Además, debe asegurarse de que estas dimensiones se puedan agrupar para todas las métricas aplicables.

**Dimension**

* **[!UICONTROL Entity_id]**: Un identificador único para cada cliente. También puede ser un número de cliente único o una dirección de correo electrónico de cliente, y debe actuar como una clave de referencia para la tabla del pedido.
* **[!UICONTROL Created_at]**: La fecha en la que se creó la cuenta del cliente y se añadió a la base de datos.
* **[!UICONTROL Customer's lifetime revenue]**: Ingresos totales generados por un cliente.
* **[!UICONTROL Customer's first 30-day revenue]**: Cantidad total de ingresos generados por un cliente en sus primeros 30 días.
* **[!UICONTROL Customer's lifetime number of orders]**: El número de pedidos realizados por un cliente durante su vida útil.
* **[!UICONTROL Customer's lifetime number of coupons]**: El número total de cupones utilizados por un cliente durante su vida útil.
* **[!UICONTROL Customer's first order date]**: La fecha del primer pedido de un cliente. Puede ser diferente a la fecha created_at si un cliente no realizó un pedido en el momento de su creación.

**¿Aceptas órdenes de invitados?**

*Si es así, es posible que esta tabla no contenga todos los clientes. Póngase en contacto con [equipo de apoyo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para garantizar que los análisis de clientes incluyan a todos los clientes.*

*¿No estás seguro de si aceptas órdenes de invitados? Consulte [este tema](../data-warehouse-mgr/guest-orders.md) para obtener más información.*

## Tabla de pedidos

En esta tabla, cada fila representa un orden. Las columnas de esta tabla contienen información básica sobre cada pedido, como el ID del pedido, la fecha de creación, el estado, el ID del cliente que realizó el pedido, etc. Los ejemplos siguientes utilizan **[!UICONTROL sales_flat_order]** como el nombre de una tabla de pedidos de ejemplo.

**Dimension**

* **[!UICONTROL Customer_id]**: Un identificador único del cliente que realizó el pedido. Esto se utiliza a menudo para mover información entre las tablas cliente y pedidos. En estos ejemplos, se espera el customer_id en el **[!UICONTROL sales_flat_order]** tabla para alinear con **[!UICONTROL entitiy_id]** en el **[!UICONTROL customer_entity]** tabla.
* **[!UICONTROL Created_at]**: La fecha en la que se creó o colocó el pedido.
* **[!UICONTROL Customer_email]**: La dirección de correo electrónico del cliente que realizó el pedido. También puede ser el identificador único del cliente.
* **[!UICONTROL Customer's lifetime number of orders]**: una copia de la columna con el mismo nombre en el `Customers` tabla.
* **[!UICONTROL Customer's order number]**: Número de pedido secuencial del cliente asociado al pedido. Por ejemplo, si la fila que está viendo es el primer pedido de un cliente, esta columna es &quot;1&quot;; pero, si era el 15º pedido del cliente, en esta columna se muestra &quot;15&quot; para este pedido. Si esta dimensión no existe en su `Customers` , pregunte a la [equipo de apoyo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para ayudarle a crearlo.
* **[!UICONTROL Customer's order number (previous-current)]**: una concatenación de dos valores en la variable **[!UICONTROL Customer's order number]** columna. Se utiliza en un informe de ejemplo a continuación para mostrar el tiempo transcurrido entre dos pedidos cualesquiera. Por ejemplo, el tiempo entre la primera fecha de pedido de un cliente y su segunda fecha de pedido se representa como &quot;1-2&quot; con este cálculo.
* **[!UICONTROL Coupon_code]**: Muestra qué cupones se utilizaron en cada pedido.
* **[!UICONTROL Seconds since previous order]**: Tiempo (en segundos) entre los pedidos de un cliente.

## Tabla de elementos de pedidos

En esta tabla, cada fila representa un artículo que se vendió. Esta tabla contiene información sobre los artículos vendidos en cada pedido, como el número de referencia del pedido, el número de producto, la cantidad, etc. Los ejemplos siguientes utilizan `sales_flat_order_item` como nombre de una tabla de elementos de pedidos de muestra.

**Dimension**

* **[!UICONTROL Item_id]**: Identificador único de cada fila de la tabla.
* **[!UICONTROL Order_id]**: La clave de referencia para su `Orders` que indica qué artículos se compraron en el mismo pedido. Si un pedido contiene varios elementos, este valor se repite.
* **[!UICONTROL Product_id]**: si desea información sobre el producto específico comprado (como el color, el tamaño, etc.), utilice esta columna para extraer esa información de la tabla de productos.
* **[!UICONTROL Order's created_at]**: La marca de tiempo con la que se realizó el pedido, que generalmente se copia en el `order line items` de la tabla de `Orders` tabla.
* **[!UICONTROL Order's coupon_code]**: similar a la `Order's created_at` dimensión, esta columna se copia de la tabla pedidos.

## Tabla de suscripciones

Esta tabla se utiliza para administrar la información de suscripción, como el ID de suscripción, la dirección de correo electrónico del suscriptor, la fecha de inicio de la suscripción, etc.

**Dimension**

* **[!UICONTROL Customer_id]**: Un identificador único del cliente que realizó el pedido. Esta es una forma común de crear una ruta entre la tabla Customers y la tabla Orders. En estos ejemplos, se espera el customer_id en el **sales_plain_order** tabla para alinear con `entitiy_id` en el `customer_entity` tabla.
* **[!UICONTROL Start date]**: La fecha en la que comenzó la suscripción de un cliente.

## Tabla de gasto de marketing

Al analizar el gasto en marketing, puede incluir lo siguiente [!DNL Facebook], [!DNL Google AdWords]u otras fuentes de los análisis. Si tiene varias fuentes de gasto de marketing, póngase en contacto con el [Equipo de Managed Services](https://business.adobe.com/products/magento/fully-managed-service.html) para obtener ayuda sobre la configuración de una tabla consolidada para sus campañas de marketing.

**Dimension**

* **[!UICONTROL Spend]**: el gasto total en publicidad. Entrada [!DNL Facebook], esta sería la columna de gasto en `facebook_ads_insights_####` tabla. Para [!DNL Google AdWords], este sería el `adCost` en la columna `campaigns####` tabla.
* El `####` que se anexa a cada una de estas tablas se refiere al ID de cuenta específico de su [!DNL Facebook] o [!DNL Google AdWords] cuenta.
* **[!UICONTROL Clicks]**: el número total de clics. Entrada [!DNL Facebook], esta sería la columna clicks en `facebook_ads_insights_####` tabla. Entrada [!DNL Google AdWords], esta sería la columna adClicks en la `campaigns####` tabla.
* **[!UICONTROL Impressions]**: el número total de impresiones. Entrada [!DNL Facebook], estas serían las impresiones en el `facebook_ads_insights_####` tabla. Entrada [!DNL Google AdWords], estas serían las impresiones del `campaigns####` tabla.
* **[!UICONTROL Campaign]**: el número total de clics. Entrada [!DNL Facebook], sería la columna campaign_name en el `facebook_ads_insights_####` tabla. Entrada [!DNL Google AdWords], esta sería la columna de campaña en la `campaigns####` tabla.
* **[!UICONTROL Date]**: la hora y la fecha en que se produjo la actividad (gasto, clics o impresiones) para una campaña en particular. Entrada [!DNL Facebook], este sería el `date_start` en la columna `facebook_ads_insights_####` tabla. Entrada [!DNL Google AdWords], esta sería la columna de fecha en la `campaigns####` tabla.
* **[!UICONTROL Customer's first order's source]**: Origen del pedido a partir del primer pedido de un cliente. En primer lugar, compruebe si tiene una columna denominada `customer's first order's source` en su cuenta. Si no ve esta columna, puede crear la columna que desee siguiendo estas instrucciones.
* **[!UICONTROL Customer's first order's medium]**: El medio del pedido a partir del primer pedido de un cliente. En primer lugar, compruebe si tiene una columna denominada `customer's first order's source` en su cuenta. Si no ve esta columna, puede crear la columna que desee siguiendo estas instrucciones.
* **[!UICONTROL Customer's first order's campaign]**: La campaña del pedido a partir del primer pedido de un cliente. En primer lugar, compruebe si tiene una columna denominada `customer's first order's source` en su cuenta. Si no ve esta columna, puede crear la columna que desee siguiendo estas instrucciones.

## Informes y métricas comunes

Estos son algunos ejemplos comunes de informes y métricas que pueden resultar útiles:

* [Customer Analytics](#customeranalytics)
* [Análisis de pedidos](#orderanalytics)
* [Marketing Spend Analytics](#mktgspendanalytics)

## Análisis de clientes {#customeranalytics}

### Nuevos usuarios

* **Descripción**: un recuento del número total de usuarios recién adquiridos durante un periodo determinado. `New Users` es diferente de `Unique Customers`, porque `New Users` tiene la marca de tiempo de que se creó una cuenta con su servicio (esto no significa que necesariamente hayan realizado un pedido) mientras que `Unique Customers` ha realizado al menos un pedido.
* **Definición de métrica**: Esta métrica realiza una **Recuento** de `entity_id` de `customer_entity` tabla ordenada por `created_at`.
* **Ejemplo de informe**: Número de nuevos usuarios creados el mes pasado
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![Nuevos usuarios](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### Clientes únicos

* **Descripción**: un recuento de la cantidad total de clientes distintos durante un periodo determinado. Esto es diferente a `New Users`, porque solo realiza el seguimiento de los clientes que han realizado al menos un pedido. Un informe de cliente distinto solo realiza el seguimiento de un cliente una vez en un intervalo de tiempo determinado. Si establece el intervalo de tiempo en `By Day` y un cliente realiza más de una compra en ese día, el cliente solo se cuenta una vez. Si desea ver un número total de compras en general, consulte `Number of Orders`.
* **Definición de métrica**: Esta métrica realiza una **Recuento distinto** de `customer_id` de `sales_flat_order` tabla ordenada por `created_at`.
* **Ejemplo de informe**: Clientes distintos por semana durante los últimos 90 días
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![Clientes únicos.](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### Nuevos suscriptores

* **Descripción**: Un recuento del número total de nuevos suscriptores adquiridos durante un periodo determinado.
* **Definición de métrica**: Esta métrica realiza una **Recuento distinto** de `customer_id` de `subscriptions` tabla ordenada por `start_date`.
* **Ejemplo de informe**: Nuevos suscriptores este año por mes
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![Suscriptores](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### Clientes repetidos

* **Descripción**: el número total de clientes que realizaron más de un pedido durante un periodo. En un informe de clientes repetidos, puede utilizar el `Distinct Customers` y la métrica `Customer's Order Number` dimensión de su `orders` tabla.
* **Métrica utilizada**: `Distinct Customers`
* **Ejemplo de informe**: Número de segundas y terceras compras realizadas el año pasado
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's Order Number`, luego seleccione `2` y `3`

  ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **Ejemplo 2 del informe**: el número de clientes repetidos los últimos años
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

  ![Clientes que repiten el año pasado](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### Clientes principales por número de pedidos de duración

* **Descripción**: Una lista de los clientes principales en función de su número total de pedidos. Esto le proporciona una lista directa de sus compradores más frecuentes.
* **Métrica utilizada**: `Orders`
* **Ejemplo de informe**: Principales 25 clientes por número de pedidos acumulado
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**: Los 25 principales clasificados por pedidos

  ![Principales 25 clientes por pedidos](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### Principales clientes por ingresos por duración

* **Descripción**: una lista de los clientes principales en función de los ingresos de por vida.
* **Métrica utilizada**: `Average Lifetime Revenue`
* **Ejemplo de informe**: Principales 25 clientes por ingresos por duración
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**: Los 25 principales clasificados por ingresos por duración

  ![Principales 25 clientes por ingresos](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### Ingresos promedio por duración por cohorte

* **Descripción**: efectúe el seguimiento de [ingresos medios a largo plazo de cohortes distintas](../dev-reports/lifetime-rev-cohort-analysis.md) de usuarios a lo largo del tiempo para identificar las cohortes de mayor rendimiento. Las cohortes se agrupan por una fecha común, como la fecha de primer orden o la fecha de creación.
* **Métrica utilizada**: `Revenue`
* **Ejemplo de informe**: Ingresos promedio por duración de cliente por cohorte
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**: conjunto móvil de cohortes de las ocho cohortes más recientes con al menos cuatro meses de datos
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**: Valor Medio Acumulado Por Miembro De Cohorte

  ![Ingresos de duración del cliente por cohorte](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### Clientes por uso de cupones

* **Descripción**: Un recuento del número de clientes adquiridos que han utilizado un código de cupón/descuento. Esto puede ayudarle a obtener una visión clara de los solicitantes de descuentos frente a los compradores a precio completo.
* **Métrica utilizada**: `New Users`
* **Ejemplo de informe**: Clientes con cupones y sin cupones por mes
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Número de Pedidos Buenos a 0 y Número de Cupones Vencidos del Cliente Igual a 0
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Número de Duración de Clientes de Pedidos Buenos a 0 y Número de Duración de Cupones del Cliente Buenos a 0
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

  ![Clientes por uso de cupones](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **Ejemplo 2 del informe**: Porcentaje de clientes con y sin cupones por mes
   * **[!UICONTROL Metric A]**: `Non coupon customers` (ocultar métrica)
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customer's Lifetime Number of Orders Greater Than 0` y `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customers Lifetime Number of Orders Greater Than 0` y `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **Ocultar todas las métricas**

![Uso de cupones](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### Ingresos medios de los primeros 30 días

* **Descripción**: la media de la cantidad de ingresos generados por los clientes en los primeros 30 días como clientes.
* **Descripción de métrica**: Esta métrica realiza una **Media** de `Customer's First 30 Day Revenue` de `customer_entity` tabla ordenada por `created_at`.
* **Descripción del informe**: Promedio histórico de los ingresos de los primeros 30 días del cliente
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![Ingresos promedio de los primeros 30 días](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### Ingresos medios por duración de clientes

* **Descripción**: Cantidad promedio de ingresos generados por los clientes a lo largo de su vida útil.
* **Descripción de métrica**: Esta métrica realiza una **Media** de la `Customer's Lifetime Revenue` en la columna `customer_entity` tabla basada en el `created_at`.
* **Descripción del informe**: Promedio histórico de los ingresos del cliente durante toda su vida útil
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![Ingresos de duración del cliente](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## Análisis de pedidos {#orderanalytics}

### Ingresos

* **Descripción**: la métrica de ingresos muestra los ingresos totales obtenidos en un período de tiempo seleccionado.
* Esta métrica realiza una **sum** de `grand_total` de `sales_flat_order` tabla ordenada por `created_at`.
* **Ejemplo de informe**: Ingresos por mes, hasta la fecha
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **Intervalo de tiempo**: `By Month`

>[!TIP]
>
>Asegúrese de que el cálculo de la métrica de ingresos sea coherente con la definición que analiza internamente. Por ejemplo, es posible que desee contar los ingresos de pedidos que se han enviado, convertir divisas de diferentes regiones o excluir impuestos. Además, puede utilizar [Conjuntos de filtros](../../data-user/reports/ess-manage-data-filters.md) para garantizar la coherencia en todas las métricas creadas en la misma tabla.

![Ingresos](../../assets/revenue.png)<!--{: width="929"}-->

### Pedidos

* **Descripción**: un recuento del número total de pedidos durante un periodo determinado. Un informe Pedidos realiza un seguimiento de los cambios en el volumen de pedidos causados por nuevas ofertas de productos, promociones o cualquier otra cosa que pueda aumentar (o disminuir) el volumen de transacciones. Es posible que a menudo quiera segmentar esta métrica según algunas variables para responder a sus preguntas.
* **Definición de métrica**: Esta métrica realiza una **Recuento** de `entity_id` de `sales_flat_order` tabla ordenada por `created_at`.
* **Ejemplo de informe**: Pedidos por mes, hasta la fecha
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>Al igual que la métrica de ingresos, debería tener [Conjuntos de filtros](../../data-user/reports/ess-manage-data-filters.md) para excluir pedidos incompletos, de prueba o devueltos.

![Pedidos](../../assets/orders_pic.png)<!--{: width="929"}-->

### Productos solicitados

* **Descripción**: la métrica Productos pedidos indica la cantidad de artículos vendidos durante un período de tiempo específico.
* **Definición de métrica**: Esta métrica realiza una **sum** de `qty_ordered` de `sales_flat_order_item` tabla ordenada por `created_at`.
* **Ejemplo de informe**: Artículos vendidos por mes, hasta la fecha
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

  ![Productos pedidos](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* Combine esta métrica con la métrica número de pedidos para calcular el número de artículos por pedido. A continuación, añada códigos de cupones al informe para determinar cómo afectan las promociones al tamaño del carro de compras o segmente los pedidos nuevos frente a los repetidos para comprender mejor el comportamiento de sus clientes.
* **Ejemplo de informe**: productos por pedido: primer pedido frente a pedidos repetidos
   * **[!UICONTROL Metric A]**: Productos pedidos: primer pedido
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**: Pedidos: primer pedido
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**: productos pedidos: repetir pedidos
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**: Pedidos: Repetir pedidos
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>Desmarque la `Multiple Y-Axes box` y `Hide` todas las métricas

![Productos pedidos 2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### Valor de pedido promedio

* **Descripción**: hace un seguimiento del valor medio de los pedidos realizados durante un periodo. Utilice esta métrica para determinar rápidamente cómo ha fluctuado el valor de pedido promedio (AOV) como resultado de sus esfuerzos de marketing, oferta de productos y otros cambios en su negocio.
* **Definición de métrica**: Esta métrica realiza una **media** de `grand_total` de `sales_flat_order` tabla ordenada por `created_at`.
* **Ejemplo de informe**: AOV frente a año anterior, hasta la fecha
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

  ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### Productos más comprados con cupones

* **Descripción**: Este informe proporciona una perspectiva de los productos que se venden cuando ofrece promociones o cupones.
* **Métrica utilizada**: productos solicitados
* **Ejemplo de informe**: Productos más comprados con cupones
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]: `name` (o `SKU`, o cualquier otro identificador de producto)
   * **[!UICONTROL Show top/bottom]**: Los 25 principales ordenados por productos

  ![Productos con cupones](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### Tiempo entre pedidos

* **Descripción**: Pruebe las suposiciones y expectativas sobre los ciclos de compra de sus clientes con una **tiempo entre pedidos** análisis que analiza el promedio (¡o mediana!) cantidad de tiempo entre compras. En la tabla siguiente, puede ver que sus mejores clientes (aquellos que realizan más de tres pedidos) realizan su segunda compra en menos de seis meses. Los clientes que no hayan realizado un cuarto pedido esperan 14 meses antes de realizar una segunda compra.
* **Definición de métrica**: Esta métrica realiza una **media** de `Time since previous order` de `sales_flat_order` ordenado por `created_at`.
* **Ejemplo de informe**:
   * **Métrica 1**: ≤ 3 pedidos
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **Métrica 2**: > 3 pedidos
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>Desmarque la `Multiple Y-Axes` cuadro.

![Tiempo entre pedidos](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## Análisis de gasto de marketing {#mktgspendanalytics}

### Gasto en publicidad

* **Descripción**: puede analizar la inversión en marketing en varios periodos de tiempo e intervalos, por campañas, conjuntos de anuncios u otras segmentaciones.
* **Definición de métrica**: Esta métrica realiza una Suma en la columna de gasto de la `Marketing Spend` tabla ordenada por el `date` columna.
* **Ejemplo de informe**: Gasto en publicidad por campaña
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![Gasto en publicidad](../../assets/ad_spend.png)<!--{: width="929"}-->

### Impresiones de publicidad y clics en publicidad

* **Descripción**: Además de analizar la inversión en publicidad, puede analizar las impresiones de la publicidad y los clics en anuncios.
* **Definición de métrica**: Esta métrica realiza una Suma en la columna de impresiones (o clics) de la variable `Marketing Spend` ordenada por la columna de fecha.
* **Ejemplo de informe**: Añada impresiones y clics de publicidad por día
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

  ![Impresiones de publicidad](../../assets/ad_impressions.png)<!--{: width="929"}-->

### Tasa de pulsaciones (CTR)

* **Descripción**: Con las métricas de impresiones de publicidad y clics en publicidad que creó anteriormente, puede analizar la tasa de clics por diferentes campañas a lo largo del tiempo.
* **Ejemplo de informe**: CTR por campaña
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Seleccione el `%` opción.
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>Puede **title** la fórmula como `CTR`, y **ocultar** todas las métricas.

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### Costo por clic (CPC)

* **Descripción**: Con las métricas de gasto en publicidad y clics en publicidad que ha creado anteriormente, puede analizar el coste por clic en diferentes campañas a lo largo del tiempo.
* **Ejemplo de informe**: CPC por campaña
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * Seleccione el `currency` opción
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>Puede **title** la fórmula como `CPC`, y **ocultar** todas las métricas.

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### Clientes por fuente de adquisición

* **Descripción**: Si realiza el seguimiento de la fuente, el medio y la campaña de un pedido utilizando [!DNL Google eCommerce], puede analizar a los clientes por su fuente de adquisición. Esto le ayuda a identificar qué fuentes de marketing están adquiriendo clientes y a responder preguntas como &quot;la mayoría de sus clientes están realizando sus primeros pedidos a través de [!DNL Google], [!DNL Facebook], o alguna otra fuente?&quot;
* **Ejemplo de informe**: Clientes por fuente de adquisición
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>Desproteger [este artículo](../analysis/most-value-source-channel.md) para obtener más ejemplos de informes que utilizan una fuente de adquisición.

![Fuente de adquisición](../../assets/acquisition_source.png)<!--{: width="929"}-->

### Clientes por medio de adquisición y campaña de adquisición

* **Descripción**: Al igual que analizar los clientes por fuente de adquisición, también puede analizarlos según el medio y la campaña de su primer pedido. Esto puede ayudarle a responder preguntas como &quot;¿qué campañas están atrayendo nuevos clientes?&quot;
* **Ejemplo de informe**: Clientes por campaña de adquisición con medio de pago
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>Para el filtro en su `New Customers` métrica, puede agregar cualquier otro medio que se considere medio de pago para su negocio, como cpc o búsqueda de pago.

![Medio de adquisición](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### Coste de adquisición de cliente (CAC) o coste por adquisición (CPA)

* **Descripción**: una forma de analizar el coste de una campaña es atribuir todos los costes únicamente a los clientes que ha adquirido a través de la campaña.
* **Ejemplo de informe**: CAC por campaña
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Seleccione el `currency` opción
   * **[!UICONTROL Group By]**:
      * Para métrica `A`, seleccione `Customer's first order's campaign`
      * Para métrica `B`, seleccione `campaign`

  ![Nuevos usuarios.](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>Puede **title** la fórmula como `CTR`, y **ocultar** todas las métricas. Además, consulte [este artículo](../analysis/roi-ad-camp.md) para obtener más información.

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### Valor de duración por fuente de adquisición, medio y campaña

* **Descripción**: Además de analizar el número de clientes adquiridos por cada campaña, puede analizar los ingresos promedio de por vida de estos clientes. Esto le ayuda a identificar:
   * Si determinadas campañas atraen a un gran volumen de clientes, pero estos tienen un valor bajo a largo plazo.
   * Si determinadas campañas atraen un volumen bajo de clientes, pero esos clientes tienen un valor alto a largo plazo.
* **Ejemplo de informe**: Primero añada el `New customers` métrica. A continuación, añada el `Average lifetime revenue` métrica. Seleccione el lapso de tiempo deseado y elija el `interval` as `None`. Finalmente, seleccione la `group by` opción como`Customer's first order's campaign`.
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>Para los dos filtros, puede agregar cualquier otro medio que se considere medio &quot;de pago&quot; para su negocio (como cpc o búsqueda de pago). También puede añadir otras fuentes que desee analizar, como Facebook. Desproteger [este artículo](../analysis/roi-ad-camp.md) para obtener más información sobre CAC, LTV y ROI.

![Valor de duración por fuente de adquisición, medio y campaña](../../assets/LTV_2.png)<!--{: width="929"}-->

### Retorno de la inversión (ROI)

* **Descripción**: una forma de calcular el ROI por campaña es analizar todos los pedidos realizados a través de la campaña. Sin embargo, hay un método alternativo que analiza el valor de duración de los clientes adquiridos a través de una campaña. Para analizar el retorno de la inversión, es importante que los nombres de las campañas sean coherentes en los datos de gasto y en los datos transaccionales. Si crea el siguiente informe y no existen valores de ROI debido a que los nombres de campaña no coinciden, es posible que tenga que consultar el [Etiquetado UTM](../../best-practices/utm-tagging-google.md) que ha implementado.
* **Ejemplo de informe**: ROI por campaña
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * Seleccione el `% `opción
   * **[!UICONTROL Group By]**:
      * Para métrica `A` y `B`, seleccione `Customer's first order's campaign`
      * Para métrica `C`, seleccione `campaign`

>[!NOTE]
>
>Puede asignar a la fórmula el título &quot;ROI&quot; (retorno de la inversión) y Ocultar todas las métricas. Además, puede ajustar los filtros de las métricas para analizar fuentes y medios alternativos. Además, consulte [este tema](../analysis/roi-ad-camp.md) para obtener más información sobre CAC, LTV y ROI.

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
