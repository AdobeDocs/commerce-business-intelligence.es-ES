---
title: Fórmulas en el Report Builder
description: Descubra cómo se pueden utilizar las fórmulas en el Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Fórmulas en la `Report Builder`

En el [`Report Builder`](../../tutorials/using-visual-report-builder.md), puede crear potentes visualizaciones utilizando el [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) en su cuenta. La combinación de estas métricas en una fórmula le permite obtener información adicional de los datos. En este tema se explica cómo se pueden utilizar las fórmulas en `Report Builder` - vamos a saltar en!

## ¿Qué es un? `formula`? {#what}

En el `Report Builder`, a `formula` es solo una combinación de una o más métricas basadas en alguna lógica matemática. Un ejemplo típico tiene este aspecto:

![](../../assets/formula-example.png)

En este ejemplo, se utiliza un `Number of orders metric (A)` y una `Distinct buyers metric (B)`y el objetivo es responder a la pregunta: ¿cuál es el número promedio de pedidos que mis compradores realizan cada mes? Los parámetros de la fórmula son:

* `Definition`: Aquí puede aplicar matemáticas en las métricas de entrada. En este ejemplo, dividir el número de pedidos por el número de compradores diferentes nos indica el número promedio de pedidos. Por lo tanto, la definición es (A/B).

* `Format`: ¿La fórmula devuelve un número, un período de tiempo o una cantidad de moneda? Junto a la definición de la fórmula hay una lista desplegable, que puede utilizar para especificar el formato de la devolución. En este caso, es un número.

* `Miscellaneous`: la marca de tiempo, las agrupaciones, las perspectivas y los filtros de la fórmula se heredan en todas sus métricas de entrada. ¡Aquí no hay nada que hacer!

## ¿Cómo puedo usar `formulas` ¿en mis informes? {#how}

Ahora que ha cubierto los conceptos básicos, vea algunos ejemplos.

### Ejemplo: quiero averiguar qué porcentaje de mis ingresos se puede atribuir a pedidos que se realizaron por primera vez.

![Uso de fórmulas para encontrar el porcentaje de ingresos atribuido a pedidos que se realizaron por primera vez](../../assets/first_time_orders.gif)

En este ejemplo, utilizó el `Revenue` y `Revenue (first time orders)` métricas. Dividiendo el `Revenue (first time orders)(B)` métrica por el `Revenue metric (A)` y establecer el formato de retorno en `Percent`Además, puede encontrar el porcentaje de ingresos que se puede atribuir a los pedidos que se realizan por primera vez.

### Ejemplo: quiero saber cuál es el ingreso promedio por pedido cuando ofrezco y no ofrezco un `promo code`.

![Uso de fórmulas para encontrar los ingresos promedio por pedido con y sin códigos de promoción](../../assets/promo_code.gif)

En este ejemplo, utilizó el `Revenue` y `Number of orders` métricas. La respuesta a esta pregunta implica dos pasos: dividir `Revenue (A)` por el `Number of orders (B)` y establecer el formato de retorno en `Currency`. A continuación, solo permitió el resultado de la fórmula (`Avg. Revenue per order`) para mostrar y agrupar los resultados por `Promo code`.

### Ejemplo: quiero saber la distribución de las fuentes de UTM de mis nuevos clientes.

![Uso de fórmulas para encontrar la distribución de las fuentes de UTM de los nuevos clientes](../../assets/distro.gif)

Encontrar la respuesta a esta pregunta implica algunos pasos:

1. Primero agregó el `New Customers` y luego agrupadas por `utm_source - all`. Esto es una métrica `A`, o `New Customers (grouped)`.

1. A continuación, duplicó la variable `New Customers (grouped)` y configúrela para que utilice una dimensión independiente. Métrica `B` - `New customers (ungrouped)` - muestra la cantidad total de clientes nuevos.

1. Después de ocultar ambas métricas, debe establecer la definición de la fórmula en `A/B`. Esto divide el `New customers (grouped)` por el `New Customers (ungrouped)`.

1. A continuación, establezca el formato de resultados en `Percent`.

En este ejemplo, utilizó el `Stacked Columns` para mostrar los resultados por mes. Esto nos permite comparar la distribución de nuevos clientes mes a mes.

## Ajuste {#wrapup}

¿Se ha dado cuenta en los ejemplos anteriores de que la fórmula `timestamp`, `groupings`, `perspectives`, y `filters` se heredan de sus métricas de entrada? Tenga en cuenta que las fórmulas se pueden utilizar para `perspectives` y [opciones de tiempo independientes](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, igual que las métricas.

Si tiene alguna pregunta adicional acerca del uso de fórmulas en la `Report Builder`, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
