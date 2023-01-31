---
title: Tableros predeterminados
description: Obtenga información sobre los paneles integrados para proporcionar información sobre su empresa.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '2235'
ht-degree: 0%

---

# Tableros predeterminados

[!DNL MBI] incluye paneles integrados para proporcionar información sobre su empresa. Con los tableros, puede comprobar el estado de las métricas esenciales, como los ingresos de por vida del usuario, la cantidad de compras repetidas, los productos principales comprados durante un período de tiempo determinado, etc. Estos tableros preconfigurados se crearon para ayudarlo a tomar decisiones comerciales informadas.

>[!NOTE]
>
>El acceso a estos tableros depende del tipo de cuenta y del nivel de acceso. Si no ve estos tableros, póngase en contacto con [support](../../guide-overview.md).

## Disponibilidad de informes

Para la variable `Customers` y `Executive Summary` tableros, algunos informes solo están disponibles en función de la configuración de cierre de compra de la tienda. Específicamente, si su tienda permite el cierre de compra de los clientes o no permite el cierre de compra de los clientes.

## Clientes (se permite el cierre de compra del invitado)

El tablero Clientes (se permite el cierre de compra de los clientes) proporciona información sobre su base de clientes, como su comportamiento de compra. Este tablero puede ayudarle a mejorar la retención de clientes y a determinar qué clientes obtienen los mayores ingresos.

### Informes

| Nombre | Descripción |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Pedidos en los últimos 30 días de clientes que nunca antes habían realizado un pedido. |
| `Orders by Existing Customers (Past 30 Days)` | Pedidos en los últimos 30 días de clientes que han realizado anteriormente al menos un pedido. |
| `Total Unique Customers (Past 30 Days)` | Recuento de clientes únicos que han realizado pedidos en los últimos 30 días. |
| `Orders by New vs Existing Customers` | Número de pedidos de clientes sin pedidos anteriores frente a clientes con al menos un pedido anterior. |
| `Subsequent Order Probability (All Time)` | La probabilidad de que los clientes que hayan realizado un pedido hagan otro. |
| `% of Customers with Multiple Orders (All Time)` | Porcentaje de todos los clientes que han realizado más de un pedido. |
| `Median Time Between Orders (All Time)` | Cantidad media de tiempo que cada cliente tarda entre realizar un pedido y el siguiente. |
| `Subsequent Order Probability` | La probabilidad de que los clientes que hayan realizado un pedido hagan otro, desglosado por número de pedido (es decir, el porcentaje de clientes con un pedido que realizan un segundo, el porcentaje de dos que realizan un tercero, etc.). |
| `Time Between Orders` | El tiempo promedio y medio que los clientes tardan entre pedidos, desglosado por número de pedido (es decir, el tiempo entre los pedidos uno y dos, dos y tres, etc.). |
| `Number of Customers - Lifetime Orders` | Para un número determinado de pedidos realizados durante la vida útil de un cliente, el número de clientes que han realizado esos pedidos y el porcentaje de toda la base de clientes que ese número representa. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clientes que realizaron su primera y única compra hace entre tres y seis meses. |
| `Avg LTV by First Order` | Compara los ingresos medios acumulados de duración de clientes entre cohortes. Las cohortes se definen por el mes en el que un cliente realizó una compra por primera vez. Por ejemplo, una `Jan 2020` La cohorte muestra el promedio acumulado de LTV para los clientes cuya primera compra fue en enero de 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Comparación de los ingresos promedio de los clientes en los 30 días posteriores a su primera compra con respecto a durante toda su vida útil. Cada burbuja corresponde a una región de envío y el tamaño de cada burbuja representa el número de clientes adquiridos de esa región. |

## Clientes (no se permite el cierre de compra de invitado)

El tablero Clientes (no se permite el cierre de compra de invitado) proporciona información sobre su base de clientes, como el comportamiento de compra y las conversiones de registros de cuenta a colocaciones de pedidos. Este tablero puede ayudarle a mejorar la retención de clientes y a determinar qué clientes obtienen los mayores ingresos.

### Informes

| Nombre | Descripción |
|---|---|
| Registro de cuentas (últimos 30 días) | El número de personas que se registraron en una cuenta en su tienda en los últimos 30 días. |
| Cuentas registradas (en los últimos 30 días) con uno o más pedidos | El número de personas que se registraron en una cuenta en su tienda en los últimos 30 días, y también realizaron al menos un pedido. |
| % de conversión de registro a primer pedido (últimos 30 días) | Porcentaje de cuentas registradas en los últimos 30 días que han realizado un pedido. |
| % de conversión de registro a primer pedido | Porcentaje de cuentas registradas que han hecho una orden, por mes de registro. |
| Pedidos de clientes nuevos frente a clientes existentes | Número de pedidos de clientes sin pedidos anteriores frente a clientes con al menos un pedido anterior. |
| Probabilidad de pedido posterior (todo el tiempo) | La probabilidad de que los clientes que hayan realizado un pedido hagan otro. |
| % de clientes con varios pedidos (todo el tiempo) | Porcentaje de todos los clientes que han realizado más de un pedido. |
| Mediana de tiempo entre pedidos (todo el tiempo) | Cantidad media de tiempo que cada cliente tarda entre realizar un pedido y el siguiente. |
| Probabilidad de pedido posterior | La probabilidad de que los clientes que hayan realizado un pedido hagan otro, desglosado por número de pedido (es decir, el porcentaje de clientes con un pedido que realizan un segundo, el porcentaje de dos que realizan un tercero, etc.). |
| Tiempo entre pedidos | El tiempo promedio y medio que los clientes tardan entre pedidos, desglosado por número de pedido (es decir, el tiempo entre los pedidos uno y dos, dos y tres, etc.). |
| Número de clientes: pedidos acumulados | Para un número determinado de pedidos realizados durante la vida útil de un cliente, el número de clientes que han realizado esos pedidos y el porcentaje de toda la base de clientes que ese número representa. |
| Clientes únicos que compraron hace 3-6 meses | Clientes que realizaron su primera y única compra hace entre tres y seis meses. |
| Promedio de LTV por orden | Compara los ingresos medios acumulados de duración de clientes entre cohortes. Las cohortes se definen por el mes en el que un cliente realizó una compra por primera vez. Por ejemplo, una cohorte de enero de 2020 muestra el promedio acumulativo de LTV para los clientes cuya primera compra fue en enero de 2020. |
| Primeros 30 días del cliente frente a ingresos acumulados | Comparación de los ingresos promedio de los clientes en los 30 días posteriores a su primera compra con respecto a durante toda su vida útil. Cada burbuja corresponde a una región de envío y el tamaño de cada burbuja representa el número de clientes adquiridos de esa región. |

## Resumen ejecutivo (se permite el cierre de compra del invitado)

El tablero Resumen Ejecutivo (cierre de compra para invitados permitido) le ofrece una imagen concisa de cómo está haciendo el negocio en términos de pedidos e ingresos. Este tablero está diseñado para que los ejecutivos puedan comprender el rendimiento del negocio en general, pero también puede ser útil para otros.

### Informes

| Nombre | Descripción |
|---|---|
| Ingresos (mes actual) | Los ingresos que ha generado su tienda durante el mes actual. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| Ingresos (últimos 6 meses por día) | Total de ingresos diarios, superpuestos con el promedio de ingresos diarios de los siete días anteriores. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| % de variación de ingresos (MoM MTD) | Comparación de ingresos en el mes actual (hasta ahora) con la misma porción del mes anterior. |
| Ingresos de clientes nuevos frente a clientes existentes (mes actual) | Ingresos del mes actual (hasta ahora) atribuidos a clientes nuevos (nuevos) frente a clientes existentes (que realizan un segundo pedido o más tarde). |
| Valor de pedido promedio (mes actual) | Valor promedio diario de los pedidos realizados en el mes actual (hasta ahora). El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| Pedidos (mes actual) | El número de pedidos realizados en la tienda durante el mes actual (hasta ahora). |
| % de cambio en pedidos (MoM MTD) | Comparación del número de pedidos del mes actual (hasta ahora) con la misma porción del mes anterior. |
| Pedidos de clientes nuevos (mes actual) | Pedidos para el mes actual de clientes que nunca antes habían realizado un pedido. |
| Pedidos por clientes existentes (mes actual) | Pedidos para el mes actual de clientes que hayan realizado anteriormente al menos un pedido. |
| Pedidos de clientes nuevos frente a clientes existentes (año actual por semana) | Número de pedidos de clientes sin pedidos anteriores frente a clientes con al menos un pedido anterior, para cada semana del año actual (hasta ahora). |

## Resumen ejecutivo (no se permite el cierre de compra de los invitados)

El tablero Resumen Ejecutivo (no se permite el cierre de compra de los clientes) le ofrece una imagen concisa de cómo está haciendo el negocio en términos de pedidos, ingresos y registros de cuentas. Este tablero está diseñado para que los ejecutivos puedan comprender el rendimiento del negocio en general, pero también puede ser útil para otros.

### Informes

| Nombre | Descripción |
|---|---|
| Ingresos (mes actual) | Los ingresos que ha generado su tienda este mes. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| Ingresos (últimos 6 meses por día) | Total de ingresos diarios, superpuestos con el promedio de ingresos diarios de los siete días anteriores. En este caso, los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| % de variación de ingresos (MoM MTD) | Comparación de ingresos hasta ahora este mes con la misma porción del mes anterior. |
| Ingresos de clientes nuevos frente a clientes existentes (mes actual) | Ingresos del mes actual (hasta ahora) atribuidos a clientes nuevos (nuevos) frente a clientes existentes (que realizan un segundo pedido o más tarde). |
| Valor de pedido promedio (mes actual) | Valor promedio diario de los pedidos realizados en el mes actual (hasta ahora). El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| Pedidos (mes actual) | El número de pedidos realizados en la tienda durante el mes actual (hasta ahora). |
| % de cambio en pedidos (MoM MTD) | Comparación del número de pedidos del mes actual (hasta ahora) con la misma porción del mes anterior. |
| Registros de cuenta (mes actual) | Número de cuentas recién registradas hasta ahora este mes. |
| % de conversión de registro a primer pedido (mes actual) | El porcentaje de cuentas registradas hasta ahora este mes que han realizado un pedido. |
| % de conversión de registro a primer pedido (año actual por semana) | El porcentaje de cuentas registradas cada semana de este año que han hecho un pedido. |

## Pedidos

El panel Pedidos proporciona perspectivas sobre el volumen transaccional de los pedidos, su estado, los códigos de cupones utilizados, los ingresos generados y los métodos de pago utilizados. Por ejemplo, puede realizar un seguimiento del proceso de cumplimiento y asegurarse de que no haya problemas ni ocurrencias de cuello de botella.

>[!NOTE]
>
>Los informes de este tablero están disponibles para cuentas conectadas a tiendas con cualquier tipo de configuración (cierre de compra de invitado, cierre de compra de invitado).

### Informes

| Nombre | Descripción |
|---|---|
| Pedidos (últimos 30 días) | Número de pedidos que se realizaron en la tienda en los últimos 30 días. |
| Ingresos (últimos 30 días) | Los ingresos que ha generado su tienda en los últimos 30 días. Los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| Valor de pedido promedio (últimos 30 días) | Valor medio de los pedidos realizados en los últimos 30 días. El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| Pedidos | Número de pedidos realizados en la tienda cada mes. |
| Ingresos por método de pago | Los ingresos que ha generado su tienda, divididos por método de pago. Los ingresos se definen como el precio final pagado por un cliente en un pedido. |
| AOV de clientes nuevos frente a clientes existentes | Valor promedio mensual de los pedidos realizados en su tienda, dividido por los pedidos realizados por clientes sin pedidos anteriores frente a los clientes con al menos un pedido anterior. El valor del pedido se define como el precio final pagado por un cliente en un pedido. |
| % de pedidos por estado (últimos 30 días) | Porcentaje de pedidos de cada día en los últimos 30 días que están actualmente en cada estado de pedido. |
| Pedidos incompletos (creados hace más de 1 día) | Una lista de todos los pedidos realizados hace más de un día que aún están en estado incompleto (no cancelados o completados). |
| Pedidos por hora (últimos 7 días) | Volumen de pedidos de día en hora. |
| Detalles de ingresos (últimos 30 días) | Desglose de ingresos diarios de los últimos 30 días en todos los componentes del valor de ingresos total. |
| Detalles del pedido por código de cupón (últimos 30 días) | Para cada código de cupón ofrecido por su tienda, detalles sobre cómo se utilizó ese código de cupón y qué devuelve el código durante los últimos 30 días. |
| % de pedidos con cupón (últimos 30 días) | El porcentaje de pedidos realizados en los últimos 30 días que usaron un cupón frente a los que no lo hicieron. |

## Productos

El panel Productos muestra el rendimiento general del producto en términos de productos pedidos, su valor bruto de mercadotecnia (GMV), así como los productos principales comprados y reembolsados. Puede ayudarle a equilibrar compras y devoluciones, así como a determinar el éxito y la popularidad del producto. Su tienda debe ser [configurado para rastrear reembolsos](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) para que se rellenen esos gráficos.

>[!NOTE]
>
>Los informes de este tablero están disponibles para cuentas conectadas a tiendas con cualquier tipo de configuración (cierre de compra de invitado, cierre de compra de invitado).

### Informes

| Nombre | Descripción |
|---|---|
| GMV (últimos 30 días) | El valor bruto de las mercancías vendidas en los últimos 30 días. GMV se define como la cantidad solicitada multiplicada por el precio base para cada producto. |
| % de GMV (30 días anteriores) reembolsado | Porcentaje de GMV para productos comprados en los últimos 30 días que resultó en un reembolso. |
| Cantidad de producto solicitada (últimos 30 días) | Cantidad total de artículos pedidos en los últimos 30 días. |
| % de productos comprados (30 días más) reembolsados | Porcentaje de artículos comprados en los últimos 30 días que resultaron en un reembolso. |
| Valor bruto de las mercancías | El valor bruto de todas las mercancías vendidas, por mes. GMV se define como la cantidad solicitada multiplicada por el precio base para cada producto. |
| Compras frente a tasa de reembolso por producto (últimos 30 días) | Para cada producto, una comparación del número total solicitado en los últimos 30 días frente a la tasa a la que se reembolsó el producto. El tamaño de cada burbuja representa el tipo de reembolso. |
| Detalles de rendimiento del producto (últimos 30 días) | Información detallada sobre las ventas y los reembolsos subsiguientes en los últimos 30 días, por sku de producto y nombre de producto. |
| Principales productos comprados por GMV (últimos 30 días) | Productos vendidos en los últimos 30 días que reportaron la mayor cantidad de ingresos (los 10 primeros). |
| Principales productos reembolsados por GMV (últimos 30 días) | Productos comprados en los últimos 30 días que resultaron en la mayor pérdida de GMV debido a reembolsos (los 10 primeros). |
| Principales productos comprados por cantidad (últimos 30 días) | Productos vendidos en los últimos 30 días en números buenos (los primeros 10). |
| Principales productos reembolsados por cantidad (últimos 30 días) | Productos comprados en los últimos 30 días que resultaron en la cantidad buena reembolsada (los primeros 10). |
