---
title: Fórmulas en Report Builder
description: Descubra cómo se pueden utilizar las fórmulas en Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/XxqMoKRPIKcRgh8HKa6z2IMp6WkiCVp2jhIbXFqcraU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 544
ht-degree: 0%

---

# Fórmulas en `Report Builder`

En [`Report Builder`](../../tutorials/using-visual-report-builder.md), puede crear visualizaciones útiles usando las [métricas definidas](../../data-user/reports/ess-manage-data-metrics.md) de su cuenta. La combinación de estas métricas en una fórmula le permite obtener información adicional de los datos. Este tema explora cómo se pueden utilizar las fórmulas en `Report Builder`: ¡vamos a saltar!

## ¿Qué es un `formula`? {#what}

En `Report Builder`, un `formula` es solo una combinación de una o más métricas basadas en alguna lógica matemática. Un ejemplo típico tiene este aspecto:

![Ejemplo de fórmula que muestra el cálculo en Report Builder](../../assets/formula-example.png)

En este ejemplo, utilizas un `Number of orders metric (A)` y un `Distinct buyers metric (B)`, y el objetivo es responder a la pregunta: ¿cuál es el número promedio de pedidos que mis compradores realizan cada mes? Los parámetros de la fórmula son:

* `Definition`: aquí se aplican cálculos matemáticos a las métricas de entrada. En este ejemplo, dividir el número de pedidos por el número de compradores diferentes nos indica el número promedio de pedidos. Por lo tanto, la definición es (A/B).

* `Format`: ¿Su fórmula devuelve un número, un período de tiempo o una cantidad de moneda? Junto a la definición de la fórmula hay una lista desplegable, que puede utilizar para especificar el formato de la devolución. En este caso, es un número.

* `Miscellaneous`: las métricas de entrada heredan la marca de tiempo, las agrupaciones, las perspectivas y los filtros de la fórmula. ¡Aquí no hay nada que hacer!

## ¿Cómo puedo usar `formulas` en mis informes? {#how}

Ahora que ha cubierto los conceptos básicos, vea algunos ejemplos.

### Ejemplo: quiero averiguar qué porcentaje de mis ingresos se puede atribuir a pedidos que se realizaron por primera vez.

![Uso de fórmulas para encontrar el porcentaje de ingresos atribuido a pedidos que se realizaron por primera vez](../../assets/first_time_orders.gif)

En este ejemplo, utilizó las métricas `Revenue` y `Revenue (first time orders)`. Si divide la métrica `Revenue (first time orders)(B)` entre `Revenue metric (A)` y establece el formato de devolución en `Percent`, puede encontrar el porcentaje de ingresos que se pueden atribuir a los pedidos que se realizaron por primera vez.

### Ejemplo: quiero saber cuál es el promedio de ingresos por pedido cuando ofrezco y no ofrezco `promo code`.

![Uso de fórmulas para encontrar los ingresos promedio por pedido con y sin códigos de promoción](../../assets/promo_code.gif)

En este ejemplo, utilizó las métricas `Revenue` y `Number of orders`. La respuesta a esta pregunta implica dos pasos: dividir `Revenue (A)` por `Number of orders (B)` y establecer el formato devuelto en `Currency`. A continuación, solo permitió que se mostrara el resultado de la fórmula (`Avg. Revenue per order`) y agrupó los resultados por `Promo code`.

### Ejemplo: quiero saber la distribución de las fuentes de UTM de mis nuevos clientes.

![Usar fórmulas para encontrar la distribución de las fuentes de UTM de los nuevos clientes](../../assets/distro.gif)

Encontrar la respuesta a esta pregunta implica algunos pasos:

1. Primero agregó la métrica `New Customers` y después agrupó por `utm_source - all`. Esta es la métrica `A` o `New Customers (grouped)`.

1. A continuación, duplicó la métrica `New Customers (grouped)` y la configuró para usar una dimensión independiente. La métrica `B` - `New customers (ungrouped)` - muestra la cantidad total de clientes nuevos.

1. Después de ocultar ambas métricas, estableció la definición de la fórmula en `A/B`. Esto divide a `New customers (grouped)` entre `New Customers (ungrouped)`.

1. A continuación, establezca el formato de resultados en `Percent`.

En este ejemplo, utilizó la perspectiva `Stacked Columns` para mostrar los resultados por mes. Esto nos permite comparar la distribución de nuevos clientes mes a mes.

## Ajuste {#wrapup}

¿Ha notado en los ejemplos anteriores que `timestamp`, `groupings`, `perspectives` y `filters` de la fórmula se heredan de sus métricas de entrada? Tenga en cuenta que las fórmulas se pueden usar para usar `perspectives` y [opciones de tiempo independientes](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"}, al igual que las métricas.

Si tiene alguna pregunta adicional acerca del uso de fórmulas en `Report Builder`, [póngase en contacto con el soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).
