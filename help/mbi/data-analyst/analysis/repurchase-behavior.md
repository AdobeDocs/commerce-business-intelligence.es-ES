---
title: Análisis del comportamiento de recompra de clientes
description: Obtenga información sobre cómo analizar el comportamiento de recompra de clientes.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---

# Comportamiento de recompra de clientes

Si ofrece más de un producto, probablemente se pregunte cómo se comportan los clientes que compran un producto específico de forma diferente a lo largo del tiempo en comparación con otros clientes. En este artículo, exploramos análisis que pueden ayudarle a responder a las siguientes preguntas:

Entre los clientes que compran un *elemento específico*,

* ¿Cuál es la probabilidad de que realicen otra compra?
* ¿Cuánto tardarán en realizar otra compra?
* ¿Cuál es el número promedio de pedidos que los clientes realizan a corto y largo plazo?
* ¿Cuál es el ingreso promedio que generan los clientes a corto y largo plazo?

## Métricas recomendadas

Al crear análisis de actividad de recompra de clientes, se recomienda utilizar las siguientes métricas:

### Probabilidad de repetición de pedido

Esta medida se define como el número total de pedidos repetidos, como un porcentaje del total de pedidos. En otras palabras, esta es la probabilidad de que un pedido sea seguido por otro pedido. Esta medida identifica los artículos que probablemente inciten a los clientes a volver a su tienda.

### Número promedio de pedidos realizados

Esto expone el comportamiento de compra de los clientes, específicamente cuántos pedidos han realizado sus clientes durante un período de tiempo determinado. Puede optar por limitar esta medida para ver el comportamiento de los clientes a corto, medio o largo plazo. Algunos productos pueden animar a los clientes a realizar compras frecuentes a corto plazo, mientras que otros pueden influir en la lealtad de un cliente a largo plazo. Si este número es mayor para un artículo comparado con otros, esto sugeriría que las personas que compran este artículo son las que regresan a su tienda.

### Ingresos promedio de la vida del cliente

Esta métrica le permite comprender si los clientes que compran artículos específicos son más valiosos a lo largo de su vida útil. Si este número es mayor para un artículo en comparación con otros artículos a precios similares, esto sugeriría que los clientes de mayor valor tienden a comprar este artículo.

### Tiempo para el siguiente pedido

Esta medida muestra la frecuencia de pedidos del cliente o el tiempo que tarda el cliente en realizar el pedido de nuevo. Si el tiempo para el siguiente pedido es más corto para un artículo en comparación con otros, esto sugeriría que las personas que compran este artículo tienden a volver antes.

## Ejemplo de hoy: productos para café

Teniendo en cuenta las métricas anteriores, echemos un vistazo a un ejemplo que involucra productos de café.

| **Nombre del producto** | **Probabilidad de repetición de pedido** | **Promedio de pedidos acumulados** | **Promedio de ingresos de por vida** | **Mediana del tiempo hasta el siguiente pedido** |
|-----|-----|-----|-----|-----|
| Cafetera de una sola taza | 94.98% | 7.92 | $549.82 | 57,01 días |
| Cápsulas de café | 93.82% | 8.68 | $479.98 | 63,48 días |
| Vainas para café | 41.92% | 6.07 | $99.82 | 27,31 días |

{style=&quot;table-layout:auto&quot;}

Ahora que tenemos nuestros datos, echemos un vistazo a lo que esto podría significar para cada una de nuestras métricas.

### Probabilidad de repetición de pedido

En este ejemplo, la probabilidad de que se repita el pedido (o la probabilidad de que un pedido sea seguido por otro pedido) es mucho mayor para las cafeteras de una sola taza y las cápsulas de café que para los granos de café.

Como los clientes que compran la cervecería están &quot;comprometidos&quot; a comprar las cápsulas asociadas en adelante, esto tiene sentido. Del mismo modo, los clientes que compraron las cápsulas tienen una cervecería compatible con las cápsulas. Sin embargo, los granos de café no son específicos de ninguna cervecería en particular.

### Cantidad promedio de pedidos acumulados

Basándonos en los datos anteriores, podemos ver que las personas que compran la cervecería o las cápsulas han hecho más compras en su vida útil, en promedio, en comparación con los clientes que han comprado granos de café.

### Ingresos promedio de la vida del cliente

Los clientes que compran la cervecería tienen los ingresos promedio de duración más altos; que tiene sentido, dado que el coste de la cervecería está incluido en esta medida. Por el contrario, los clientes que compran granos de café generalmente solo compran artículos de bajo costo.

### Tiempo para el siguiente pedido

Entre los clientes que han comprado cápsulas de café, la mitad realiza un pedido repetido en unos 2 meses. Sin embargo, entre los clientes que han comprado granos de café, la mitad realiza un pedido repetido en aproximadamente 1 mes. Esto podría deberse a que las personas que piden cápsulas (1) no beben tanto café, o (2) realizan pedidos a granel (por ejemplo, compran café durante 2 meses en un solo pedido).

## ¿Qué otros análisis puedo generar?

Con las métricas que describimos en este artículo, también puede crear otros útiles análisis de recompras. Por ejemplo, también podemos ver cómo recompran los clientes **el mismo elemento** - por ejemplo, si compran recargas de forma regular. Las cápsulas y los granos de café pueden ser recomprados regularmente, pero sería inesperado ver a los clientes haciendo compras repetidas de la cafetera. Si su negocio se centra en recargas o repoblación, este análisis sería extremadamente útil.

Además de analizar el comportamiento de recompra de sus clientes, también puede crear análisis que miren la lealtad del cliente. Considere analizar los patrones en la pérdida de clientes: ¿dónde abandonan el sitio los clientes y dónde no regresan? ¿A qué ritmo ocurre esto?

Una vez que haya identificado el motivo por el que se está produciendo la pérdida, puede utilizar el análisis para crear un `reactivation` campaña. Con estos datos se puede identificar a los usuarios que se han vuelto inactivos, cuánto tiempo han transcurrido desde su última visita, cuál fue su última compra, etc. Esto le permitirá tomar decisiones útiles que incitarán a sus clientes a regresar.

Para obtener ayuda con el análisis, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
