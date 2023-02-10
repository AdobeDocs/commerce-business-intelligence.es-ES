---
title: Fórmulas en el Report Builder
description: Descubra cómo se pueden utilizar las fórmulas en el Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Las fórmulas de `Report Builder`

En el [`Report Builder`](../../tutorials/using-visual-report-builder.md), puede crear visualizaciones potentes mediante el [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) en su cuenta. La combinación de estas métricas en una fórmula le permite obtener perspectivas adicionales de sus datos. En este artículo, profundizamos en cómo se pueden utilizar las fórmulas en la variable `Report Builder` - ¡saltemos!

## ¿Qué es un `formula`? {#what}

En el `Report Builder`, `formula` es solo una combinación de una o más métricas basadas en alguna lógica matemática. Un ejemplo típico tiene este aspecto:

![](../../assets/formula-example.png)

En este ejemplo se usa un `Number of orders metric (A)` y `Distinct buyers metric (B)`, y nuestro objetivo es responder a la pregunta: ¿cuál es el número promedio de pedidos que mis compradores realizan cada mes? Los parámetros de la fórmula son:

* `Definition`: Aquí se aplican cálculos sobre las métricas de entrada. En este ejemplo, dividir el número de pedidos por el número de compradores distintos nos dirá el número promedio de pedidos. Por lo tanto, la definición es (A/B).

* `Format`: ¿La fórmula devuelve un número, un período de tiempo o una cantidad de moneda? Junto a la definición de la fórmula hay una lista desplegable, que puede utilizar para especificar el formato del retorno. En este caso, es un número.

* `Miscellaneous`: La marca de tiempo, las agrupaciones, las perspectivas y los filtros de la fórmula se heredan mediante sus métricas de entrada. ¡Aquí no hay nada que hacer!

## ¿Cómo puedo usar `formulas` en mis informes? {#how}

Ahora que hemos cubierto lo básico, veamos algunos ejemplos.

### Ejemplo: Quiero averiguar qué porcentaje de mis ingresos se puede atribuir a pedidos nuevos.

![Uso de fórmulas para encontrar el porcentaje de ingresos atribuido a pedidos nuevos](../../assets/first_time_orders.gif)

En este ejemplo, utilizamos la variable `Revenue` y `Revenue (first time orders)` métricas. Dividiendo el `Revenue (first time orders)(B)` por `Revenue metric (A)` y estableciendo el formato de retorno en `Percent`, podemos encontrar el porcentaje de ingresos que se puede atribuir a pedidos por primera vez.

### Ejemplo: Quiero saber cuál es el ingreso promedio por pedido cuando ofrezco y no ofrezco una `promo code`.

![Uso de fórmulas para encontrar el ingreso promedio por pedido con y sin códigos de promoción](../../assets/promo_code.gif)

En este ejemplo, utilizamos la variable `Revenue` y `Number of orders` métricas. La respuesta a esta pregunta implica dos pasos: dividir `Revenue (A)` por `Number of orders (B)` y estableciendo el formato de retorno en `Currency`. A continuación, solo permitimos el resultado de la fórmula (`Avg. Revenue per order`) para mostrar y agrupar los resultados por `Promo code`.

### Ejemplo: Quiero saber la distribución de las fuentes UTM de mis nuevos clientes.

![Uso de fórmulas para encontrar la distribución de las fuentes de UTM de los nuevos clientes](../../assets/distro.gif)

Encontrar la respuesta a esta pregunta implica algunos pasos:

1. En primer lugar, agregamos la variable `New Customers` y, a continuación, agrupadas por `utm_source - all`. Esta es una métrica `A`o `New Customers (grouped)`.

1. A continuación, duplicamos el `New Customers (grouped)` y configúrela para que utilice una dimensión independiente. Métrica `B` - `New customers (ungrouped)` : muestra el número total de clientes nuevos.

1. Después de ocultar ambas métricas, establecemos la definición de la fórmula en `A/B`. Esto divide el `New customers (grouped)` por `New Customers (ungrouped)`.

1. A continuación, establecemos el formato de resultados en `Percent`.

En nuestro ejemplo, usamos la variable `Stacked Columns` perspectiva para mostrar los resultados por mes. Esto nos permite comparar la distribución de nuevos clientes mes a mes.

## Ajuste {#wrapup}

¿Se ha dado cuenta en los ejemplos anteriores de que la fórmula `timestamp`, `groupings`, `perspectives`y `filters` ¿se heredan de sus métricas de entrada? Tenga en cuenta que las fórmulas se pueden aprovechar para utilizar `perspectives` y [opciones de tiempo independientes](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, tal como las métricas pueden hacerlo.

Si tiene alguna pregunta adicional sobre el uso de fórmulas en la variable `Report Builder`, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
