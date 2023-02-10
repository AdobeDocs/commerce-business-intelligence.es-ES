---
title: Análisis del impacto de cupones
description: Aprenda a analizar el impacto de los cupones en la adquisición y retención de clientes.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 2%

---

# Impacto de cupones

Analizar cómo los clientes utilizan sus cupones puede proporcionar una perspectiva significativa de su negocio. Específicamente, analizar cómo adquiere y retiene clientes a través de cupones. En este artículo, exploramos análisis que pueden ayudarle a responder a los siguientes tipos de preguntas:

* ¿Cuántos clientes adquiere a través de cupones?
* ¿Es más probable que los clientes que adquieren cupones hagan compras repetidas que los que no lo hacen mediante cupones?
* ¿En qué se diferencian los ingresos promedio de por vida entre los clientes que adquieren cupones y los que no se adquieren a través de cupones?
* ¿Los clientes adquiridos con cupones realizan compras repetidas con cupones?

Para responder a estas preguntas, nos centramos en [comparación de clientes adquiridos con cupones con clientes no adquiridos con cupones](#compare), [análisis de detalles de primer pedido de adquisiciones de cupones](#firstorder)y [observar los atributos de los clientes que utilizan cupones en su primer pedido.](#attributes)

¡Empecemos!

## Comparación de clientes adquiridos con cupones con clientes adquiridos sin cupones {#compare}

Cuando genere análisis que exploren la adquisición y retención de cupones, considere la posibilidad de utilizar las siguientes métricas:

### Número de clientes nuevos

Esta métrica muestra el número de clientes que han adquirido cupones y de clientes que no han recibido cupones durante todo el tiempo. Esto puede ayudarle a determinar la proporción de adquisiciones de clientes a través de cupones.

### Ingresos medios de duración

Esta métrica muestra los ingresos medios a lo largo de la vida de los clientes que han adquirido cupones y no cupones. Esto puede ayudar a determinar si el valor de duración de un cliente varía según su tipo de adquisición.

### Número de pedidos repetidos

Esta métrica muestra el número de pedidos repetidos realizados por ambos tipos de adquisiciones de clientes. Esto puede ayudar a determinar si se realizan más pedidos de seguimiento por parte de clientes que han adquirido cupones o que no han adquirido cupones.

### Número y porcentaje de pedidos repetidos con cupón

Esto muestra el número de pedidos repetidos realizados con un cupón aplicado y el porcentaje de pedidos repetidos realizados con un cupón. Esto puede ayudarle a determinar si los clientes con cupones adquiridos tienden a realizar más pedidos repetidos con un cupón que los clientes adquiridos sin cupones y si los clientes adquiridos con cupones utilizan cupones de forma desproporcionada en sus pedidos de seguimiento.

Veamos algunos datos de ejemplo para métricas de adquisición de cupones frente a métricas de adquisición sin cupones:

| **Adquisición de cliente** | **Número de clientes nuevos** | **Ingresos medios de duración** | **Número de pedidos repetidos** | **Número de pedidos repetidos con cupón** | **% de pedidos repetidos con cupón** |
|-----|-----|-----|-----|-----|-----|
| Cupón | 1,206 | $356.91 | 2,570 | 1,248 | 48.56% |
| No cupón | 11,561 | $498.30 | 20,145 | 3,251 | 16.14% |

{style=&quot;table-layout:auto&quot;}

¿Qué podemos quitar de esto? Echemos un vistazo:

### Número de clientes nuevos

En el ejemplo anterior, hay un número mucho mayor de adquisiciones sin cupones que de adquisiciones de cupones. Sin embargo, todavía hay 1,206 clientes adquiridos a través de un cupón que de otra manera podrían no haber llegado a ser clientes.

### Ingresos medios de duración

En este ejemplo, las adquisiciones que no son de cupones tienen un promedio de ingresos mayor que las adquisiciones de cupones. Esto implica que las adquisiciones que no son de cupones están haciendo más compras repetidas o están realizando compras de mayor valor.

### Número de pedidos repetidos

El número de pedidos repetidos para adquisiciones que no son de cupones es mucho mayor que el de adquisiciones de cupones. Esto se espera porque hay muchos más clientes que no tienen cupones adquiridos.

### Número de pedidos repetidos con cupón

Del mismo modo, el número de pedidos repetidos realizados con un cupón es mayor para las adquisiciones que no son de cupón.

## #Porcentaje de pedidos repetidos con cupón

Los clientes que no han adquirido cupones tienen un porcentaje mucho menor de pedidos repetidos con un cupón aplicado que los clientes que han adquirido cupones. Por lo tanto, para los clientes con cupones adquiridos, casi uno de cada dos pedidos repetidos tiene un cupón aplicado. En este ejemplo, los clientes con cupones adquiridos tienden a realizar compras repetidas con cupones.

## Análisis de los detalles de primer pedido de adquisiciones de cupones {#firstorder}

En esta sección, nos centramos únicamente en **primeros pedidos de adquisiciones de cupones, segmentados por cupones.** utilizamos estas métricas en nuestro análisis:

### Número de pedidos/clientes

Esta métrica muestra el número de pedidos nuevos para cada cupón o el número de clientes que usaron ese cupón en su primer pedido. Esto puede ayudar a determinar si un determinado cupón fomenta más compras por primera vez que otros cupones.

### Ingresos brutos

Esta métrica revela los ingresos que obtiene de un cupón en particular que se utilizó en el primer pedido de un cliente. Estos ingresos son un cálculo de los artículos vendidos antes de aplicar cualquier descuento.

### Descuentos de cupones

Esta métrica muestra la cantidad de descuento total aplicada de los cupones.

### Ingresos netos

Esta métrica revela los ingresos que obtiene de un cupón en particular que se utilizó en el primer pedido de un cliente. Estos ingresos son un cálculo de los artículos vendidos después de aplicar todos los descuentos. es importante tener en cuenta que los ingresos netos pueden no haberse producido sin los cupones.

### Valor de pedido promedio

Esta métrica revela el valor de pedido promedio de un cupón en particular.

### Cantidad promedio de pedidos acumulados

Esta métrica ayuda a evaluar la lealtad y el número promedio de pedidos generados por clientes que utilizan un determinado cupón.

### Ingresos medios de duración

Esta métrica ayuda a evaluar la lealtad y los ingresos promedio generados por los clientes que utilizan un determinado cupón. Al evaluar si los clientes que utilizan cupones tienen un valor mayor que otros, asegúrese de tener en cuenta el número de pedidos en los que se ha utilizado cada cupón para asegurarse de que tiene un tamaño de muestra significativo.

Ahora, veamos un ejemplo que implica tres cupones diferentes utilizados para los pedidos por primera vez de los clientes:

| **Cupón** | **Pedidos por primera vez (FTO)** | **Ingresos brutos procedentes de FTO** | **Descuentos aplicados a FTO** | **Ingresos netos de FTO** | **Valor de pedido promedio para FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% de descuento en $100 o más** | 56 | $8,531.04 | $2,132.76 | $6,398.28 | $152.34 |
| **$10 de descuento** | 87 | $3,707.07 | $426.10 | $3,280.97 | $42.61 |
| **20 % de descuento** | 145 | $10,975.05 | $2,195.01 | $8,780.04 | $75.69 |

{style=&quot;table-layout:auto&quot;}

¿Qué podemos quitar de esto? En primer lugar, el cupón de &quot;20% de descuento&quot; tenía la mayor cantidad de pedidos por primera vez. Sin embargo, el número de pedidos asociados a cada cupón puede variar en función de varios factores, entre ellos:

* la cantidad de publicidad de cada cupón.
* el periodo de tiempo durante el cual se ofrecieron los cupones.
* hora del día/semana/mes/año en que se ofrecieron los cupones.
* la temporada se ofrecieron los cupones, dependiendo del negocio.

   **Ejemplo:** el cupón de &quot;20% de descuento&quot; se ofreció durante los meses de verano, pero el negocio vende ropa de invierno.
* las restricciones sobre los cupones.

   **Ejemplo:** el cupón &quot;10% de descuento&quot; solo se ofrece a los clientes que compran un abrigo de invierno en el mismo pedido.

La variable **ingresos brutos** para el cupón de &quot;25% de descuento de $100 o más&quot; es mucho más alto que los ingresos brutos para el cupón de &quot;10 dólares de descuento&quot;. Sin embargo, el cupón de &quot;10 dólares de descuento&quot; tiene un valor mucho mayor **número de pedidos**. Análisis de la variable **valor de pedido promedio** proporciona una perspectiva de estas diferencias: aunque el cupón de &quot;25% de descuento de 100 dólares o más&quot; tenía menos pedidos, el valor promedio de pedido es más del triple que el del cupón de &quot;10 dólares de descuento&quot;. Por lo tanto, se atribuye un mayor ingreso bruto al cupón de &quot;25% de descuento de 100 dólares o más&quot;.

La variable **descuentos** y **ingresos netos** para los cupones &quot;25% de descuento en $100 o más&quot; y &quot;20% de descuento&quot; tienen un valor cercano. Aunque el valor de pedido promedio para &quot;25% de descuento en 100 dólares o más&quot; es casi el doble del valor de pedido promedio para &quot;20% de descuento&quot;, este último tiene un poco menos que el triple del número de pedidos.

## Atributos de los clientes que utilizan cupones en su primer pedido {#attributes}

Ahora que hemos visto los pedidos en sí, echemos un vistazo a los clientes que usan cupones en sus primeros pedidos:

| **Cupón de primer pedido del cliente** | **Número de clientes** | **Cantidad promedio de pedidos acumulados** | **Ingresos medios de duración** |
|-----|-----|-----|-----|
| **25% de descuento en $100 o más** | 56 | 2.8 | $554.54 |
| **$10 de descuento** | 87 | 1.9 | $115.50 |
| **20 % de descuento** | 145 | 1.3 | $103.75 |

{style=&quot;table-layout:auto&quot;}

notará que el número de pedidos nuevos es el mismo que el número de clientes para cada cupón. Esto tiene sentido porque cada cliente solo puede tener un primer pedido.

El mayor número de clientes se adquirió mediante el cupón del &quot;20 % de descuento&quot;. Sin embargo, estos clientes tienen el valor más bajo **número promedio de pedidos de duración** y **ingresos promedio de duración**; por lo general, la mayoría de los clientes que adquieren cupones no realizan pedidos repetidos. Además, los clientes adquiridos a través del cupón de &quot;25% de descuento de 100 dólares o más&quot; aumentan **número promedio de pedidos de duración** y, a su vez, más **ingresos promedio de duración**. Por lo general, los usuarios que se adquirieron mediante este cupón suelen regresar y realizar más compras repetidas.

## Ajuste {#wrapup}

Puede crear una multitud de análisis para comprender mejor cómo utilizan los cupones los clientes. ¿Alguna vez ha pensado en analizar cómo utilizan sus clientes sus cupones o el tiempo que tardan los cupones en utilizarse? ¿Qué sucede si se encuentra la cantidad de descuento óptima? ¿Qué cantidad fomenta la repetición de compradores, un mayor valor de pedido promedio y mayores ingresos de por vida? Para obtener ayuda con este tipo de preguntas, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
