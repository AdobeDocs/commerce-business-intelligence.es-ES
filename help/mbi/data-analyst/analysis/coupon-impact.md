---
title: Análisis del impacto de cupones
description: Obtenga información sobre cómo analizar el impacto de los cupones en la adquisición y retención de clientes.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Impacto de cupón

Analizar cómo los clientes utilizan sus cupones puede proporcionar insight significativo en su negocio. Específicamente, analizando cómo adquiere y retiene clientes a través de cupones. En este tema se exploran los análisis que pueden ayudarle a responder a los siguientes tipos de preguntas:

* ¿Cuántos clientes adquiere mediante cupones?
* ¿Los clientes con cupones adquiridos tienen más probabilidades de realizar compras repetidas que los clientes no adquiridos a través de cupones?
* ¿En qué se diferencian los ingresos medios a largo plazo entre los clientes adquiridos con cupones y los clientes no adquiridos con cupones?
* ¿Los clientes adquiridos con cupones realizan compras repetidas con cupones?

Responda a estas preguntas centrándose en [comparar clientes adquiridos con cupones con clientes adquiridos sin cupones](#compare), [analizar los detalles del primer pedido de las adquisiciones de cupones](#firstorder) y [observar los atributos de los clientes que usan cupones en su primer pedido.](#attributes)

¡Empiece!

## Comparación entre clientes con cupones adquiridos y clientes sin cupones adquiridos {#compare}

Cuando cree análisis que exploren la adquisición y retención de cupones, considere la posibilidad de utilizar las métricas siguientes:

### Número de clientes nuevos

Esta métrica muestra el número de clientes adquiridos con cupones y clientes adquiridos sin cupones durante todo el tiempo. Esto puede ayudarle a determinar la proporción de adquisiciones de clientes a través de cupones.

### Ingresos medios a largo plazo

Esta métrica muestra los ingresos promedio por vida útil de los clientes adquiridos con cupones y sin cupones. Esto puede ayudar a determinar si el valor de duración de un cliente varía según el tipo de adquisición.

### Número de pedidos repetidos

Esta métrica muestra el número de pedidos repetidos realizados por ambos tipos de adquisiciones de clientes. Esto puede ayudar a determinar si se realizan más pedidos de seguimiento por clientes con o sin cupones adquiridos.

### Número y porcentaje de pedidos repetidos con cupón

Muestra el número de pedidos repetidos realizados con un cupón aplicado y el porcentaje de pedidos repetidos realizados con un cupón. Esto puede ayudarle a determinar si los clientes con cupones adquiridos tienden a hacer más pedidos repetidos con un cupón que los clientes sin cupones adquiridos y si los clientes con cupones adquiridos utilizan cupones de forma desproporcionada en sus pedidos de seguimiento.

Observe algunos datos de ejemplo para métricas de adquisición de cupones frente a métricas de adquisición no de cupones:

| **Adquisición de cliente** | **Número de clientes nuevos** | **Ingresos promedio de por vida** | **Número de pedidos repetidos** | **Número de pedidos repetidos con cupón** | **% de pedidos repetidos con cupón** |
|-----|-----|-----|-----|-----|-----|
| Cupón | 1.206 | 356,91 $ | 2.570 | 1.248 | 48,56 % |
| Sin cupón | 11.561 | 498,30 $ | 20.145 | 3.251 | 16,14 % |

{style="table-layout:auto"}

Mira lo que puedes quitar de esto:

### Número de clientes nuevos

En el ejemplo anterior, hay un número mucho mayor de adquisiciones sin cupones que de adquisiciones con cupones. Sin embargo, todavía hay 1.206 clientes adquiridos a través de un cupón que de otra manera podría no haberse convertido en clientes.

### Ingresos medios a largo plazo

En este ejemplo, las adquisiciones sin cupones tienen un ingreso promedio de por vida mayor que las adquisiciones de cupones. Esto implica que las adquisiciones sin cupones están haciendo compras más repetidas o están haciendo compras de mayor valor.

### Número de pedidos repetidos

El número de pedidos repetidos para adquisiciones sin cupones es mucho mayor que para adquisiciones con cupones. Esto se debe a que hay muchos más clientes adquiridos sin cupones.

### Número de pedidos repetidos con cupón

Del mismo modo, el número de pedidos repetidos realizados con un cupón es mayor en el caso de las adquisiciones sin cupón.

## Porcentaje de pedidos repetidos con cupón

Los clientes sin cupón adquirido tienen un porcentaje mucho menor de pedidos repetidos con un cupón aplicado que los clientes con cupón adquirido. Por lo tanto, para los clientes con cupones adquiridos, casi la mitad de los pedidos repetidos tienen un cupón aplicado. En este ejemplo, los clientes de cupones adquiridos tienden a realizar compras repetidas con cupones.

## Análisis de los detalles del primer pedido de las adquisiciones de cupones {#firstorder}

Esta sección se centra solamente en **primeros pedidos de adquisiciones de cupones, segmentados por cupón.** Use estas métricas en el análisis:

### Número de pedidos/clientes

Esta métrica muestra el número de pedidos por primera vez para cada cupón o el número de clientes que utilizaron ese cupón en su primer pedido. Esto puede ayudar a determinar si un determinado cupón anima a realizar más compras por primera vez que otros cupones.

### Ingresos brutos

Esta métrica revela los ingresos que obtiene de un cupón en particular que se utilizó en el primer pedido de un cliente. Estos ingresos son un cálculo de los artículos vendidos antes de aplicar cualquier descuento.

### Descuentos de cupones

Esta métrica muestra el importe de descuento total aplicado desde los cupones.

### Ingresos netos

Esta métrica revela los ingresos que obtiene de un cupón en particular que se utilizó en el primer pedido de un cliente. Estos ingresos son un cálculo de los artículos vendidos después de aplicar todos los descuentos. Es importante tener en cuenta que los ingresos netos pueden no haberse producido sin los cupones.

### Valor de pedido promedio

Esta métrica muestra el valor de pedido promedio de un cupón determinado.

### Número promedio de pedidos durante toda la vida

Esta métrica ayuda a evaluar la lealtad y el número promedio de pedidos generados por los clientes que utilizan un cupón determinado.

### Ingresos medios a largo plazo

Esta métrica ayuda a evaluar la lealtad y los ingresos promedio generados por los clientes que utilizan un cupón determinado. Al evaluar si los clientes que utilizan cupones tienen un valor mayor que otros, asegúrese de tener en cuenta el número de pedidos en los que se utilizó cada cupón para garantizar que tenga un tamaño de muestra significativo.

Ahora, observe un ejemplo que incluye tres cupones diferentes utilizados para el primer pedido de los clientes:

| **Cupón** | **Pedidos por primera vez (FTO)** | **Ingresos brutos de FTO** | **Descuentos aplicados a FTO** | **Ingresos netos de FTO** | **Valor de pedido promedio para FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% de descuento de $100 o más** | 56 | 8.531,04 $ | 2.132,76 $ | 6.398,28 $ | 152,34 $ |
| **$10 de descuento** | 87 | 3.707,07 $ | 426,10 $ | 3.280,97 $ | 42,61 $ |
| **20% de descuento** | 145 | 10.975,05 $ | 2.195,01 $ | 8.780,04 $ | 75,69 USD |

{style="table-layout:auto"}

¿Qué se puede sacar de esto? En primer lugar, el cupón de &quot;20% de descuento&quot; tuvo la mayor cantidad de pedidos por primera vez. Sin embargo, el número de pedidos asociados a cada cupón podría variar en función de varios factores, entre ellos:

* el importe del anuncio de cada cupón.
* el periodo de tiempo durante el cual se ofrecieron los cupones.
* la hora del día/semana/mes/año en que se ofrecieron los cupones.
* la temporada en la que se ofrecieron los cupones, dependiendo del negocio.

  **Ejemplo:** el cupón de &quot;20% de descuento&quot; se ofreció durante los meses de verano, pero el negocio vende ropa de invierno.
* las restricciones sobre los cupones.

  **Ejemplo:** el cupón de &quot;10% de descuento&quot; solo se ofrece a los clientes que compren un abrigo de invierno en el mismo pedido.

Los **ingresos brutos** del cupón &quot;25% de descuento de 100 dólares o más&quot; son mucho más altos que los ingresos brutos del cupón &quot;10 dólares de descuento&quot;. Sin embargo, el cupón de &quot;$10 off&quot; tiene un **número de pedidos** mucho mayor. Analizar el **valor de pedido promedio** proporciona a insight estas diferencias. A pesar de que el cupón de &quot;25% de descuento de 100 dólares o más&quot; tenía menos número de pedidos, el valor de pedido promedio es más del triple que el cupón de &quot;$10 de descuento&quot;. Por lo tanto, se atribuye un mayor ingreso bruto al cupón de &quot;25% de descuento de 100 dólares o más&quot;.

Los **descuentos** y **ingresos netos** para los cupones de &quot;25% de descuento en 100 dólares o más&quot; y &quot;20% de descuento&quot; tienen un valor cercano. Aunque el valor de pedido promedio para &quot;25% de descuento de 100 dólares o más&quot; está cerca del doble del valor de pedido promedio para &quot;20% de descuento&quot;, este último cupón tiene un poco menos del triple del número de pedidos.

## Atributos de los clientes que utilizan cupones en su primer pedido {#attributes}

Ahora que ha visto los pedidos en sí, observe a los clientes que utilizan cupones en sus primeros pedidos:

| **Cupón de primer pedido del cliente** | **Cantidad de clientes** | **Número promedio de pedidos durante toda la vida** | **Ingresos promedio de por vida** |
|-----|-----|-----|-----|
| **25% de descuento de $100 o más** | 56 | 2,8 | 554,54 $ |
| **$10 de descuento** | 87 | 1,9 | 115,50 $ |
| **20% de descuento** | 145 | 1,3 | 103,75 $ |

{style="table-layout:auto"}

Verá que el número de pedidos por primera vez es el mismo que el número de clientes para cada cupón. Esto tiene sentido porque cada cliente solo puede tener un primer pedido.

El mayor número de clientes se adquirió a través del cupón de &quot;20% de descuento&quot;. Sin embargo, estos clientes tienen el **número promedio de duración de pedidos** y **ingresos promedio de duración** más bajos; por lo general, la mayoría de los clientes con cupones adquiridos no realizan pedidos repetidos. Además, los clientes que obtuvieron a través del cupón de &quot;25% de descuento de 100 dólares o más&quot; obtienen un número de pedidos **promedio de por vida** más alto y, a su vez, **ingresos promedio de por vida** más altos. Por lo general, los usuarios que fueron adquiridos a través de este cupón generalmente regresan y hacen más compras repetidas.

## Ajuste {#wrapup}

Puede crear multitud de análisis para comprender mejor cómo utilizan los cupones sus clientes. ¿Ha pensado alguna vez en analizar cómo utilizan sus clientes los cupones o el tiempo que tardan en utilizarlos? ¿Qué sucede si se busca la cantidad de descuento óptima: qué cantidad anima a los compradores que repiten, un valor de pedido promedio más alto y mayores ingresos por duración? Para obtener ayuda con este tipo de preguntas, [comuníquese con la atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).
