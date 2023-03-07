---
title: Análisis del uso de cupones
description: Obtenga información sobre cómo analizar el uso de cupones en la adquisición y retención de clientes.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 2%

---

# Uso de cupones

¿Alguna vez se ha preguntado cómo afecta la oferta de cupones a su negocio? ¿Quiere saber qué cupones ayudan o perjudican el rendimiento? Este artículo explora los análisis que le ofrecen una buena imagen del uso de cupones de sus clientes al responder a las siguientes preguntas:

* ¿Cuántos clientes utilizan cupones?
* ¿Cuántos cupones se están utilizando?
* ¿Cuáles son sus ingresos antes y después de que se apliquen los cupones?
* ¿Cuál es el valor de pedido promedio antes y después de aplicar los cupones?
* ¿Qué tipo de clientes atrae con cupones?

¡Empecemos!

## Métricas recomendadas {#metrics}

Al analizar el uso de cupones, considere la posibilidad de utilizar ([o edificio](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Número de pedidos

Esta métrica muestra el número de pedidos con y sin cupones a lo largo del tiempo. Esto muestra si los clientes utilizan los cupones y con qué frecuencia, y cómo cambia con el tiempo.

### Ingresos brutos

Esta métrica muestra los ingresos brutos que se obtienen de los pedidos que incluyen un cupón determinado. Los ingresos brutos son un cálculo del precio total de los artículos vendidos, antes de aplicar descuentos. Esto puede ayudar a determinar qué cupones están asociados con los ingresos brutos más altos y más bajos.

### Descuentos de cupones

Esta métrica puede mostrar el importe de descuento total aplicado desde los cupones. Es importante tener en cuenta que estos pedidos pueden no haberse producido sin los cupones.

### Ingresos netos

Esta métrica muestra los ingresos netos que se obtienen de los pedidos que incluyen un cupón determinado. Los ingresos netos son un cálculo del precio de los artículos vendidos después de aplicar todos los descuentos. Esto puede ayudar a determinar qué cupones están asociados con los ingresos netos más altos y más bajos.

### Porcentaje descontado

Muestra la proporción de ingresos brutos que se compensa con los descuentos. Para los cupones que ofrecen un descuento porcentual, este valor ya se conoce (por ejemplo, 10 % de descuento). A pesar de esto, esta medida proporciona una perspectiva y un método de comparación para los cupones que son un descuento en dólares fijos.

### Valor de pedido neto promedio

Esta medida muestra el valor de pedido promedio cuando se aplica un cupón. Puede analizar si los pedidos con cupones tienen de forma coherente un valor de pedido inferior al de los pedidos sin cupones.

### Descuento de pedido promedio

Esto muestra el valor en dólares promedio descontado de cada pedido donde se aplican cupones. Muestra la diferencia entre el valor de pedido neto promedio y el valor de pedido bruto promedio.

### Distintos compradores

Esta métrica muestra el número de compradores diferentes que utilizan un determinado cupón.

### Ingresos medios a largo plazo

Esta métrica ayuda a evaluar la lealtad y los ingresos promedio generados por los clientes que utilizan un cupón determinado. Al evaluar si los clientes que utilizan cupones tienen un valor mayor que otros, asegúrese de tener en cuenta la cantidad de compradores diferentes en cada categoría para asegurarse de que tiene un tamaño de muestra significativo.

## Ejemplo {#example}

Ahora que sabe qué métricas ver, observe un ejemplo que incluye tres cupones diferentes: 10 % de descuento, 20 dólares de descuento en 100 o más y 10 dólares de descuento.

| **Cupón** | **Número de pedidos** | **Ingresos brutos** | **Descuentos brutos de cupones** | **Ingresos netos** | **Porcentaje descontado** |
|-----|-----|-----|-----|-----|-----|
| **10 % de descuento** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **$20 de descuento en $100+** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **10 $ de descuento** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style="table-layout:auto"}


| **Cupón** | **El Promedio de valor de pedido neto** | **El Promedio de descuento por pedido** | **Distintos compradores** | **El Promedio de ingresos por duración** |
|-----|-----|-----|-----|-----|
| **10 % de descuento** | $225.08 | $25.01 | 79 | $361.50 |
| **$20 de descuento en $100+** | $117.91 | $20.00 | 95 | $218.76 |
| **10 $ de descuento** | $62.35 | $10.00 | 199 | $84.27 |

{style="table-layout:auto"}

## ¿Qué se puede sacar de esto?

Se realizaron alrededor de 80 pedidos con el cupón de &quot;10% de descuento&quot;, 100 pedidos con el cupón de &quot;$20 de descuento de $100 o más&quot; y 200 pedidos con el cupón de &quot;$10 de descuento&quot;. El **número de pedidos** asociadas a cada cupón pueden variar en función de varios factores, entre ellos:

* el periodo de tiempo durante el cual se ofrecieron los cupones.
* la hora del día/semana/mes/año en que se ofrecieron los cupones.
* la temporada en la que se ofrecieron los cupones, dependiendo del negocio. Por ejemplo:
* El cupón de &quot;10% de descuento&quot; se ofreció durante los meses de verano, pero el negocio vende ropa de invierno.

* las restricciones sobre los cupones. Por ejemplo:
* El cupón de &quot;$10 off&quot; solo se ofrece a los nuevos clientes.
* El cupón de &quot;10% de descuento&quot; solo se ofrece a los clientes que compren un abrigo de invierno en el mismo pedido.

* el comportamiento de compra típico del cliente.

Mientras que el **descuentos brutos** para los tres cupones son similares (alrededor de $2,000), el número de pedidos para cada cupón es diferente. El análisis de los descuentos por pedido ayuda a explicar las razones de estos números contrastantes. El cupón de &quot;10% de descuento&quot; tiene el menor número de pedidos, pero un **descuento de pedido promedio** de unos 25 dólares. Aunque este cupón tiene un número bajo de pedidos, su alto valor de descuento promedio hace que su importe de descuento bruto se acerque a los $2,000.

**Ingresos brutos y netos** proporciona una idea general del valor total de los pedidos asociados con cada cupón. Sin embargo, este panorama general no permite comprender los diferentes comportamientos relacionados con cada cupón. Una vez que consulta una base por pedido, puede ver que el cupón de &quot;10% de descuento&quot; tiene un alto **pedido neto promedio** valor, que a su vez conduce a su alto **ingresos netos**.

Por otro lado, el cupón de &quot;10% de descuento&quot; tiene un valor de descuento promedio alto ($25.01), pero el más bajo **porcentaje de descuento**. Esto tiene sentido cuando se contabiliza su valor de pedido neto promedio de 225,08 $. El cupón &quot;10% de descuento&quot; tiene un pequeño descuento porcentual de un gran valor de pedido neto promedio, por lo que el descuento de pedido promedio es una gran cantidad.

Consulte la **distintos compradores** y **ingresos medios a largo plazo** para cada cupón. El cupón de &quot;10% de descuento&quot; tiene el mismo número de pedidos que compradores diferentes. Esto podría deberse a que cada cliente se limita a un cupón. Por otro lado, los cupones de &quot;$20 de descuento de $100 o más&quot; y &quot;$10 de descuento&quot; tienen menos compradores distintos que el número de pedidos, lo que implica que algunos clientes utilizaron estos cupones varias veces.

Para los ingresos promedio por duración, puede ver que los ingresos promedio por duración de cada cupón son buenos que los respectivos **pedido neto promedio** valor. Esto implica que, o bien los clientes realizaron compras repetidas o bien el valor de su pedido fue mucho más alto que el valor neto promedio del pedido.

## ¿Qué más puedo analizar? {#otheranalyses}

Los análisis mencionados en este artículo pueden proporcionarle una valiosa perspectiva de cómo sus clientes utilizan sus cupones, pero hay una multitud de otros análisis que le permiten profundizar un poco más.

**Puede analizar las adquisiciones de clientes a partir de cupones.**

¿Qué cupones animan a los clientes a realizar pedidos? ¿Estos cupones atraen a compradores únicos o fomentan la lealtad del cliente (es decir, el cliente que realiza compras repetidas)?

**Puede analizar el tiempo que tardan los clientes en utilizar los cupones.**

¿Se utilizan los cupones el día en que se lanzan o transcurre una semana o dos antes de que la mayoría de los clientes los utilicen?

**Podría descubrir la cantidad de descuento óptima que aumenta la lealtad del cliente y el valor general.**

¿Qué cantidad de descuento fomenta la repetición de compradores, un valor de pedido promedio más alto y mayores ingresos por vida útil?

Responder a estas preguntas le ofrece información sobre sus clientes, su comportamiento y los cupones que proporcionan el mayor valor a su negocio.
