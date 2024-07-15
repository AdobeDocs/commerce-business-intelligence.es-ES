---
title: Paneles integrados en el producto
description: Obtenga información acerca de los paneles predeterminados para proporcionar información sobre su empresa.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# Paneles listos para usar.

[!DNL Adobe Commerce Intelligence] incluye paneles predeterminados para proporcionar información sobre su negocio. Con los paneles, puede comprobar el estado de las métricas esenciales, como los ingresos de por vida del usuario, el número de compras repetidas, los productos principales comprados en un período de tiempo determinado y más. Estos paneles preconfigurados se crearon para ayudarle a tomar decisiones comerciales fundadas.

>[!NOTE]
>
>El acceso a estos paneles depende del tipo de cuenta y del nivel de acceso. Si no ve estos paneles, comuníquese con [soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Disponibilidad del informe

Para los paneles de `Customers` y `Executive Summary`, algunos informes solo están disponibles según la configuración de cierre de compra de la tienda. Específicamente, si su tienda permite el pago y envío de invitados o no permite el pago y envío de invitados.

## Clientes (se permite el cierre de compra de invitados)

El panel Clientes (con derecho de pago y envío de invitados) proporciona información sobre su base de clientes, como su comportamiento de compra. Este tablero puede ayudarle a mejorar la retención de clientes y determinar qué clientes obtienen los mayores ingresos.

### Informes

| Nombre | Descripción |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Pedidos en los últimos 30 días de clientes que nunca han realizado un pedido anteriormente. |
| `Orders by Existing Customers (Past 30 Days)` | Pedidos en los últimos 30 días de clientes que han realizado al menos un pedido anteriormente. |
| `Total Unique Customers (Past 30 Days)` | Recuento de clientes únicos que han realizado pedidos en los últimos 30 días. |
| `Orders by New vs Existing Customers` | Número de pedidos de clientes sin pedidos anteriores frente a clientes con al menos un pedido anterior. |
| `Subsequent Order Probability (All Time)` | La probabilidad de que los clientes que hayan realizado un pedido realicen otro. |
| `% of Customers with Multiple Orders (All Time)` | Porcentaje de todos los clientes que han realizado más de un pedido. |
| `Median Time Between Orders (All Time)` | Cantidad media de tiempo que tarda cada cliente entre la realización de un pedido y el siguiente. |
| `Subsequent Order Probability` | La probabilidad de que los clientes que hayan realizado un pedido realicen otro pedido, desglosado por número de pedido. Es decir, el porcentaje de clientes con un pedido que colocan un segundo, el porcentaje con dos que colocan un tercero, y así sucesivamente. |
| `Time Between Orders` | El tiempo medio y medio que tardan los clientes entre pedidos, desglosado por número de pedido (es decir, el tiempo entre pedidos uno y dos, dos y tres, etc.). |
| `Number of Customers - Lifetime Orders` | Para un número determinado de pedidos realizados durante la vida útil de un cliente, el número de clientes que han realizado ese número de pedidos y el porcentaje de toda la base de clientes que representa ese número. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clientes que realizaron su primera y única compra entre hace tres y seis meses. |
| `Avg LTV by First Order` | Compara el promedio acumulado de ingresos por vida útil del cliente entre cohortes. Las cohortes se definen por el mes en el que un cliente realizó una compra por primera vez. Por ejemplo, una cohorte `Jan 2020` muestra el LTV promedio acumulado de los clientes cuya primera compra fue en enero de 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparación de los ingresos promedio de los clientes en los 30 días posteriores a su primera compra frente a durante toda su vida útil. Cada burbuja corresponde a una región de envío y el tamaño de cada burbuja representa el número de clientes adquiridos de esa región. |

## Clientes (no se permite el pago y envío de invitados)

El panel Clientes (no se permite el cierre de compra de invitados) proporciona información sobre su base de clientes, como su comportamiento de compra y las conversiones desde los registros de cuenta hasta las ubicaciones de pedidos. Este tablero puede ayudarle a mejorar la retención de clientes y determinar qué clientes obtienen los mayores ingresos.

### Informes

| Nombre | Descripción |
|---|---|
| `Account Registration (Past 30 Days)` | Número de personas que se registraron en una cuenta de su tienda en los últimos 30 días. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | El número de personas que se registraron para una cuenta en su tienda en los últimos 30 días, y también hicieron al menos un pedido. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Porcentaje de cuentas registradas en los últimos 30 días que han realizado un pedido. |
| `% Conversion from Registration to First Order` | Porcentaje de cuentas registradas que han realizado un pedido, por mes de registro. |
| `Orders by New vs Existing Customers` | Número de pedidos de clientes sin pedidos anteriores frente a clientes con al menos un pedido anterior. |
| `Subsequent Order Probability (All Time)` | La probabilidad de que los clientes que hayan realizado un pedido realicen otro. |
| `% of Customers with Multiple Orders (All Time)` | Porcentaje de todos los clientes que han realizado más de un pedido. |
| `Median Time Between Orders (All Time)` | Cantidad media de tiempo que tarda cada cliente entre la realización de un pedido y el siguiente. |
| `Subsequent Order Probability` | La probabilidad de que los clientes que hayan realizado un pedido coloquen otro, desglosado por número de pedido. Es decir, el porcentaje de clientes con un pedido que realizan un segundo, el porcentaje con dos que realizan un tercer pedido, etc. |
| `Time Between Orders` | El tiempo medio y medio que tardan los clientes entre pedidos, desglosado por número de pedido (es decir, el tiempo entre pedidos uno y dos, dos y tres, etc.). |
| `Number of Customers - Lifetime Orders` | Para un número determinado de pedidos realizados durante la vida útil de un cliente, el número de clientes que han realizado ese número de pedidos y el porcentaje de toda la base de clientes que representa ese número. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clientes que realizaron su primera y única compra entre hace tres y seis meses. |
| `Avg LTV by First Order` | Compara el promedio acumulado de ingresos por vida útil del cliente entre cohortes. Las cohortes se definen por el mes en el que un cliente realizó una compra por primera vez. Por ejemplo, una cohorte de enero de 2020 muestra el promedio acumulado de LTV para los clientes cuya primera compra fue en enero de 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparación de los ingresos promedio de los clientes en los 30 días posteriores a su primera compra frente a durante toda su vida útil. Cada burbuja corresponde a una región de envío y el tamaño de cada burbuja representa el número de clientes adquiridos de esa región. |

## Resumen ejecutivo (se permite el pago y envío de invitados)

El panel de control Resumen ejecutivo (se permite el pago de los huéspedes) le ofrece una imagen sucinta del rendimiento de la empresa en términos de pedidos e ingresos. Este tablero está diseñado para que los ejecutivos comprendan el rendimiento empresarial en general, pero también puede ser revelador para otros.

### Informes

| Nombre | Descripción |
|---|---|
| `Revenue (Current Month)` | Ingresos que ha generado su tienda en el mes actual. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `Revenue (Past 6 Months by Day)` | Ingresos diarios totales, superpuestos con los ingresos diarios medios de los siete días anteriores. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `% Change in Revenue (MoM MTD)` | Comparación de ingresos del mes actual (hasta ahora) frente a la misma porción del mes anterior. |
| `Revenue from New vs Existing Customers (Current Month)` | Ingresos del mes actual (hasta el momento) atribuidos a clientes nuevos (nuevos) frente a clientes existentes (segundo o posterior pedido). |
| `Average Order Value (Current Month)` | Valor medio diario de los pedidos realizados en el mes actual (hasta el momento). El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| `Orders (Current Month)` | Número de pedidos realizados en su tienda durante el mes actual (hasta el momento). |
| `% Change in Orders (MoM MTD)` | Comparación del número de pedidos del mes actual (hasta ahora) con la misma parte del mes anterior. |
| `Orders by New Customers (Current Month)` | Pedidos del mes actual de clientes que nunca han realizado un pedido anteriormente. |
| `Orders by Existing Customers (Current Month)` | Pedidos del mes actual de clientes que han realizado al menos un pedido anteriormente. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Número de pedidos de clientes sin pedidos anteriores frente a los de clientes con al menos un pedido anterior, para cada semana del año actual (hasta ahora). |

## Resumen ejecutivo (no se permite pagar)

El panel de resumen ejecutivo (no se permite el cierre de compra de invitados) le ofrece una imagen sucinta de cómo está funcionando la empresa en términos de pedidos, ingresos y registros de cuenta. Este tablero está diseñado para que los ejecutivos comprendan el rendimiento empresarial en general, pero también puede ser revelador para otros.

### Informes

| Nombre | Descripción |
|---|---|
| `Revenue (Current Month)` | Ingresos que ha generado su tienda este mes. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `Revenue (Past 6 Months by Day)` | Ingresos diarios totales, superpuestos con los ingresos diarios medios de los siete días anteriores. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `% Change in Revenue (MoM MTD)` | Comparación de ingresos en lo que va de mes frente a la misma porción del mes anterior. |
| `Revenue from New vs Existing Customers (Current Month)` | Ingresos del mes actual (hasta el momento) atribuidos a clientes nuevos (nuevos) frente a clientes existentes (segundo o posterior pedido). |
| `Average Order Value (Current Month)` | Valor medio diario de los pedidos realizados en el mes actual (hasta el momento). El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| `Orders (Current Month)` | Número de pedidos realizados en su tienda durante el mes actual (hasta el momento). |
| `% Change in Orders (MoM MTD)` | Comparación del número de pedidos del mes actual (hasta ahora) con la misma parte del mes anterior. |
| `Account Registrations (Current Month)` | Número de cuentas recién registradas en lo que va de mes. |
| `% Conversion from Registration to First Order (Current Month)` | Porcentaje de cuentas registradas en lo que va de mes que han realizado un pedido. |
| `% Conversion from Registration to First Order (Current Year by Week)` | El porcentaje de cuentas registradas cada semana en lo que va de año que han realizado un pedido. |

## Pedidos

El panel Pedidos proporciona información sobre el volumen transaccional de pedidos, su estado, los códigos de cupón utilizados, los ingresos generados y los métodos de pago utilizados. Por ejemplo, puede realizar un seguimiento del proceso de cumplimiento y asegurarse de que no haya problemas ni ocurrencias de cuellos de botella.

>[!NOTE]
>
>Los informes de este tablero están disponibles para cuentas conectadas a tiendas con cualquier tipo de configuración (cierre de compra de invitado, sin cierre de compra de invitado).

### Informes

| Nombre | Descripción |
|---|---|
| `Orders (Past 30 Days)` | El número de pedidos realizados con su tienda en los últimos 30 días. |
| `Revenue (Past 30 Days)` | Ingresos que su tienda ha generado en los últimos 30 días. Los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `Average Order Value (Past 30 Days)` | Valor medio de los pedidos realizados en los últimos 30 días. El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| `Orders` | El número de pedidos realizados en su tienda cada mes. |
| `Revenue by Payment Method` | Los ingresos que ha generado su tienda, divididos por método de pago. Los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| `AOV by New vs Existing Customers` | Valor medio mensual de los pedidos realizados en su tienda, dividido por los pedidos realizados por clientes sin pedidos anteriores frente a los clientes con al menos un pedido anterior. El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| `% Orders by Status (Past 30 Days)` | Porcentaje de pedidos de cada día en los últimos 30 días que están actualmente en cada estado de pedido. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Una lista de todos los pedidos realizados hace más de un día que aún están en estado incompleto (no cancelados o completados). |
| `Orders Per Hour (Past 7 Days)` | Ordene el volumen día a hora. |
| `Revenue Details (Past 30 Days)` | Desglose de ingresos diarios de los últimos 30 días en todos los componentes del valor de ingresos totales. |
| `Order Details by Coupon Code (Past 30 Days)` | Para cada código de cupón ofrecido por su tienda, detalles sobre cómo se utilizó ese código de cupón y qué devoluciones trajo durante los últimos 30 días. |
| `% Orders with Coupon (Past 30 Days)` | El porcentaje de pedidos realizados en los últimos 30 días que utilizaron un cupón frente a los que no lo hicieron. |

## Productos

El panel Productos muestra el rendimiento general del producto en términos de productos pedidos, su valor bruto de mercancía (GMV) y los principales productos comprados y reembolsados. Puede ayudarle a equilibrar las compras y las devoluciones, así como a determinar el éxito y la popularidad del producto. Su tienda debe estar [configurada para hacer un seguimiento de los reembolsos](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) para que se rellenen esos gráficos.

>[!NOTE]
>
>Los informes de este tablero están disponibles para cuentas conectadas a tiendas con cualquier tipo de configuración (cierre de compra de invitado, sin cierre de compra de invitado).

### Informes

| Nombre | Descripción |
|---|---|
| `GMV (Past 30 Days)` | El valor bruto de mercancía de todos los productos vendidos en los últimos 30 días. GMV se define como la cantidad pedida multiplicada por el precio base de cada producto. |
| `% GMV (Past 30 Days) Refunded` | Porcentaje de GMV para productos comprados en los últimos 30 días que tuvieron como resultado un reembolso. |
| `Product Quantity Ordered (Past 30 Days)` | Cantidad total de artículos pedidos en los últimos 30 días. |
| `% Purchased Products (Past 30 Days) Refunded` | Porcentaje de artículos comprados en los últimos 30 días que resultaron en un reembolso. |
| `Gross Merchandise Value` | El valor bruto de mercancía de todos los productos vendidos, por mes. GMV se define como la cantidad pedida multiplicada por el precio base de cada producto. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Para cada producto, una comparación del número total pedido en los últimos 30 días frente a la tasa a la que se reembolsó el producto. El tamaño de cada burbuja representa la tasa de reembolso. |
| `Product Performance Details (Past 30 Days)` | Información detallada sobre las ventas y los reembolsos posteriores en los últimos 30 días, por SKU del producto y nombre del producto. |
| `Top Purchased Products by GMV (Past 30 Days)` | Productos vendidos en los últimos 30 días que generaron la mayor cantidad de ingresos (los 10 principales). |
| `Top Refunded Products by GMV (Past 30 Days)` | Productos comprados en los últimos 30 días que resultaron en la mayor cantidad de GMV perdidos debido a reembolsos (top 10). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Productos vendidos en los últimos 30 días en los mayores números (top 10). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Productos comprados en los últimos 30 días que tuvieron como resultado la mayor cantidad reembolsada (top 10). |
