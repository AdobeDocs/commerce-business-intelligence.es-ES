---
title: Análisis del Comportamiento de Recompra del Cliente
description: Obtenga información sobre cómo analizar el comportamiento de las devoluciones de clientes.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Comportamiento de recompra del cliente

Si ofrece más de un producto, probablemente se pregunte cómo los clientes que compran un producto específico se comportan de forma diferente a lo largo del tiempo en comparación con otros clientes. En este tema se exploran los análisis que pueden ayudarle a responder las siguientes preguntas.

Entre los clientes que compran un *artículo específico*,

* ¿Cuál es la probabilidad de que realicen otra compra?
* ¿Cuánto tiempo les toma hacer otra compra?
* ¿Cuál es el número promedio de pedidos que realizan los clientes a corto/largo plazo?
* ¿Cuáles son los ingresos promedio que generan los clientes a corto/largo plazo?

## Métricas recomendadas

A la hora de crear análisis de actividad de recompra de clientes, Adobe recomienda utilizar las siguientes métricas:

### Probabilidad de orden repetido

Esta medida se define como el número total de pedidos repetidos, como un porcentaje del total de pedidos. En otras palabras, esta es la probabilidad de que un pedido vaya seguido de otro. Esta medida identifica los artículos que tienen probabilidades de atraer a los clientes para que regresen a su tienda.

### Número medio de pedidos realizados

Esto expone el comportamiento de compra de sus clientes, específicamente cuántos pedidos han realizado durante un período de tiempo determinado. Puede optar por limitar esta medida para ver el comportamiento de los clientes a corto, medio o largo plazo. Algunos productos pueden animar a los clientes a realizar compras frecuentes a corto plazo, mientras que otros pueden influir en la lealtad a largo plazo de un cliente. Si este número es mayor para un artículo en comparación con otros artículos, esto sugeriría que las personas que compran este artículo son las que regresan a su tienda.

### Ingresos medios por duración de clientes

Esta métrica le permite comprender si los clientes que compran artículos específicos son más valiosos a lo largo de su vida útil. Si este número es mayor para un artículo en comparación con otros artículos con precios similares, esto sugeriría que tus clientes de mayor valor tienden a comprar este artículo.

### Tiempo para el siguiente pedido

Esta medida muestra la frecuencia de pedido del cliente o el tiempo que tarda en volver a realizar el pedido. Si el tiempo para el siguiente pedido es más corto para un artículo en comparación con otros artículos, esto sugeriría que las personas que compran este artículo tienden a regresar antes.

## Ejemplo de hoy: productos de café

Con las métricas anteriores en mente, observe un ejemplo que implica productos de café.

| **Nombre del producto** | **Probabilidad de repetición de pedido** | **Número promedio de pedidos durante toda la vida** | **Ingresos promedio por duración** | **Mediana de tiempo hasta el siguiente pedido** |
|-----|-----|-----|-----|-----|
| Cervecero de una taza | 94,98 % | 7,92 | 549,82 $ | 57,01 días |
| Cápsulas de café | 93,82 % | 8,68 | 479,98 $ | 63,48 días |
| Granos de café | 41,92 % | 6,07 | 99,82 $ | 27,31 días |

{style="table-layout:auto"}

Ahora que tiene los datos, ¿qué significa esto para cada una de las métricas?

### Probabilidad de orden repetido

En este ejemplo, la probabilidad de que se repita un pedido (o la probabilidad de que un pedido vaya seguido de otro) es mucho mayor en las cafeteras de una sola taza y en las cápsulas de café que en los granos de café.

Dado que los clientes que compran la cervecería están &quot;comprometidos&quot; a comprar las cápsulas asociadas en el futuro, esto tiene sentido. Del mismo modo, los clientes que compraron cápsulas tienen una cerveza que es compatible con las cápsulas. Sin embargo, los granos de café no son específicos de una cervecera en particular.

### Número promedio de pedidos durante toda la vida

En base a los datos anteriores, se puede ver que las personas que compran la cerveza o las cápsulas han hecho más compras en su vida, en promedio, en comparación con los clientes que han comprado granos de café.

### Ingresos medios por duración de clientes

Los clientes que compran la cervecera tienen los ingresos promedio de por vida más altos, lo cual tiene sentido, dado que el costo de la cervecera está incluido en esta medida. Por el contrario, los clientes que compran granos de café generalmente solo compran artículos de bajo coste.

### Tiempo para el siguiente pedido

Entre los clientes que han comprado cápsulas de café, la mitad hacen un pedido repetido en aproximadamente dos meses. Sin embargo, entre los clientes que han comprado granos de café, la mitad hace un pedido repetido en aproximadamente un mes. Esto puede deberse a que las personas que ordenan cápsulas, ya sea (1) no beben tanto café, o (2) realizan pedidos a granel (por ejemplo, comprando café de dos meses en un pedido).

## ¿Qué otros análisis se pueden generar?

Con las métricas descritas en este tema, también puede crear otros análisis de recompra útiles. Por ejemplo, también puede ver cómo los clientes vuelven a comprar **el mismo artículo**, por ejemplo, si compran recargas con regularidad. Las cápsulas y los granos de café se pueden volver a comprar con regularidad, pero sería inesperado ver a los clientes haciendo compras repetidas de la cervecera. Si su negocio se centra en recargas o reabastecimiento, este análisis sería útil.

Además de analizar el comportamiento de recompra de sus clientes, también puede generar análisis que miren la lealtad de los clientes. Considere la posibilidad de analizar los patrones de pérdida de clientes. ¿Dónde abandonan el sitio los clientes y no regresan? ¿A qué ritmo ocurre esto?

Una vez que haya identificado por qué se produce la pérdida, puede utilizar el análisis para generar una campaña `reactivation`. Con estos datos, puede identificar a los usuarios que se han vuelto inactivos, cuánto tiempo ha pasado desde su última visita, cuál fue su última compra, etc. Esto le permite tomar decisiones procesables que atraen a sus clientes a regresar.

Para obtener ayuda con el análisis, [comuníquese con la atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
