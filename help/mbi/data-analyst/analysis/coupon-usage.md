---
title: Análisis del uso de cupones
description: Aprenda a analizar el uso de cupones para adquirir y retener clientes.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Uso de cupones

¿Alguna vez te preguntas cómo la oferta de cupones afecta tu negocio? ¿Quiere saber qué cupones ayudan o dañan el rendimiento? En este artículo, exploramos análisis que le ofrecen una buena imagen del uso de los cupones de sus clientes respondiendo a estas preguntas:

* ¿Cuántos clientes utilizan cupones?
* ¿Cuántos cupones se están utilizando?
* ¿Cuáles son sus ingresos antes y después de aplicar los cupones?
* ¿Cuál es el valor de pedido promedio antes y después de aplicar los cupones?
* ¿Qué clase de clientes atrae con cupones?

¡Empecemos!

## Métricas recomendadas {#metrics}

Al analizar el uso de cupones, considere la posibilidad de utilizar ([o construcción](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Número de pedidos

Esta métrica muestra el número de pedidos con o sin cupones a lo largo del tiempo. Esto muestra si los clientes utilizan sus cupones y con qué frecuencia, y cómo cambia con el tiempo.

### Ingresos brutos

Esta métrica revela los ingresos brutos que obtiene de los pedidos que incluyen un cupón en particular. Los ingresos brutos son un cálculo del precio total de los artículos vendidos, antes de aplicar cualquier descuento. Esto puede ayudar a determinar qué cupones están asociados a los ingresos brutos más altos y más bajos.

### Descuentos de cupones

Esta métrica puede mostrar la cantidad de descuento total aplicada de los cupones. es importante tener en cuenta que estos pedidos pueden no haber ocurrido sin los cupones.

### Ingresos netos

Esta métrica muestra los ingresos netos que obtiene de los pedidos que incluyen un cupón en particular. Los ingresos netos son un cálculo del precio de los artículos vendidos después de aplicar todos los descuentos. Esto puede ayudar a determinar qué cupones están asociados con los ingresos netos más altos y más bajos.

### Porcentaje descontado

Se muestra la proporción de ingresos brutos compensada por descuentos. Para los cupones que ofrecen un descuento porcentual, este valor ya se conoce (por ejemplo, 10 % de descuento). A pesar de esto, esta medida proporciona una perspectiva y un método de comparación para cupones que son un descuento fijo en dólares.

### Valor de pedido neto promedio

Esta medida muestra el valor de pedido promedio cuando se aplica un cupón. Puede analizar si los pedidos con cupones tienen de manera consistente un valor de pedido menor que los pedidos sin cupones.

### Descuento promedio por pedido

Muestra el valor de dólar promedio descontado de cada pedido donde se aplican cupones. Esto muestra la diferencia entre el valor de pedido neto promedio y el valor de pedido bruto promedio.

### Compradores distintos

Esta métrica muestra el número de compradores diferentes que utilizan un cupón determinado.

### Ingresos medios de duración

Esta métrica ayuda a evaluar la lealtad y los ingresos promedio generados por los clientes que utilizan un determinado cupón. Al evaluar si los clientes que utilizan cupones tienen un valor mayor que otros, asegúrese de tener en cuenta el número de compradores distintos en cada categoría para asegurarse de que tiene un tamaño de muestra significativo.

## Ejemplo {#example}

Ahora que sabemos qué métricas analizar, veamos un ejemplo que involucra tres cupones diferentes: 10% de descuento, 20 dólares de descuento de 100 dólares o más y 10 dólares de descuento.

| **Cupón** | **N.º de pedidos** | **Ingresos brutos** | **Descuentos brutos de cupones** | **Ingresos netos** | **Porcentaje descontado** |
|-----|-----|-----|-----|-----|-----|
| **10 % de descuento** | 79 | 19.757,02 $ | 1.975,70 $ | 17.781,32 $ | 10,00 % |
| **$20 de $100+** | 101 | 13.928,91 $ | 2.020,00 $ | 11.908,91 $ | 14,50 % |
| **$10 de descuento** | 201 | 14.542,35 $ | 2.010,00 $ | 12.532,35 $ | 13,82 % |

{style=&quot;table-layout:auto&quot;}


| **Cupón** | **Promedio de valor de pedido neto** | **Promedio de descuento por pedido** | **Compradores distintos** | **Promedio de ingresos acumulados** |
|-----|-----|-----|-----|-----|
| **10 % de descuento** | 225,08 $ | 25,01 $ | 79 | 361,50 $ |
| **$20 de $100+** | 117,91 $ | 20,00 $ | 95 | 218,76 $ |
| **$10 de descuento** | 62,35 $ | 10,00 $ | 199 | 84,27 $ |

{style=&quot;table-layout:auto&quot;}

## ¿Qué podemos quitar de esto?

Se realizaron alrededor de 80 pedidos con el cupón &quot;10% de descuento&quot;, 100 pedidos con el cupón &quot;$20 de $100 o más&quot; y 200 pedidos con el cupón &quot;$10 de descuento&quot;. La variable **número de pedidos** asociados a cada cupón pueden variar en función de varios factores, entre ellos:

* el periodo de tiempo durante el cual se ofrecieron los cupones.
* hora del día/semana/mes/año en que se ofrecieron los cupones.
* la temporada se ofrecieron los cupones, dependiendo del negocio. Por ejemplo:
* El cupón de &quot;10% de descuento&quot; se ofreció durante los meses de verano, pero el negocio vende ropa de invierno.

* las restricciones sobre los cupones. Por ejemplo:
* El cupón de &quot;10$ de descuento&quot; solo se ofrece a los clientes nuevos.
* El cupón de &quot;10% de descuento&quot; solo se ofrece a los clientes que compran un abrigo de invierno en el mismo pedido.

* el comportamiento de compra típico del cliente.

Mientras que la variable **descuentos brutos** para los tres cupones son muy similares (alrededor de $2,000), el número de pedidos para cada cupón es significativamente diferente. El análisis de descuentos por pedido ayuda a explicar las razones de estos números de contraste. El cupón de &quot;10% de descuento&quot; tiene el menor número de pedidos, pero un **descuento de pedido promedio** de unos 25 dólares. Aunque este cupón tiene un número bajo de pedidos, su alto valor promedio de descuento hace que su importe bruto de descuento se aproxime a los $2,000.

**Ingresos brutos y netos** ofrece una idea general del valor total de los pedidos asociados a cada cupón. Sin embargo, esta imagen general no proporciona una comprensión de los diferentes comportamientos relacionados con cada cupón. Una vez que observe por pedido, puede ver que el cupón de &quot;10 % de descuento&quot; tiene un cupón muy alto **pedido neto promedio** que, a su vez, lleva a su valor **ingresos netos**.

Por otro lado, el cupón de &quot;10% de descuento&quot; tiene un valor de descuento promedio muy alto ($25.01), pero el más bajo **porcentaje descuento**. Esto tiene sentido cuando se tiene en cuenta su valor de pedido neto promedio de 225,08 $. El cupón &quot;10% de descuento&quot; tiene un pequeño descuento porcentual de un valor de pedido neto promedio grande, por lo que el descuento promedio de pedido es una cantidad grande.

Echemos un vistazo a la **compradores distintos** y **ingresos promedio de duración** para cada cupón. El cupón &quot;10% de descuento&quot; tiene el mismo número de pedidos que los compradores diferentes. Esto puede deberse a que cada cliente se ha limitado a un cupón. Por otro lado, los cupones de &quot;$20 de descuento de $100 o más&quot; y &quot;$10 de descuento&quot; tienen menos compradores diferentes que el número de pedidos, lo que implica que algunos clientes usaron estos cupones varias veces.

En el caso de los ingresos medios a lo largo de la vida, puede ver que los ingresos medios a lo largo de cada cupón son buenos que los correspondientes **pedido neto promedio** valor. Esto implica que los clientes realizaron compras repetidas o que su valor de pedido fue mucho mayor que el valor de pedido neto promedio.

## ¿Qué más puedo analizar? {#otheranalyses}

Los análisis a los que nos referimos en este artículo pueden proporcionarle una valiosa perspectiva de cómo sus clientes utilizan sus cupones, pero hay muchos otros análisis que le permiten profundizar un poco.

**Puede analizar las adquisiciones de clientes a partir de cupones.**

¿Qué cupones animan a los clientes a realizar pedidos? ¿Estos cupones atraen compradores únicos o fomentan la lealtad del cliente (es decir, clientes que realizan compras repetidas)?

**Puede analizar el tiempo que tardan sus clientes en utilizar sus cupones.**

¿Se utilizan los cupones el día en que se publican o transcurre una o dos semanas antes de que la mayoría de los clientes los usen?

**Podría descubrir la cantidad de descuento óptima que aumenta la lealtad del cliente y el valor general.**

¿Qué importe de descuento animará a los compradores habituales, a un mayor valor de pedido promedio y a mayores ingresos acumulados?

Responder a estas preguntas le proporcionará información sobre sus clientes, su comportamiento y los cupones que ofrecen el mayor valor para su negocio.
