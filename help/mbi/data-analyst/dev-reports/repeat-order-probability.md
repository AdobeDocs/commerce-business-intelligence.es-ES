---
title: Informe de probabilidad de repetición de pedido
description: Conozca y comprenda el informe de probabilidad de repetición de pedido.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Informe de probabilidad de repetición de pedido

## Cuándo es la variable `Incremental Event Probability` perspectiva disponible?

La variable `incremental event probability` Perspectiva solo está disponible cuando los filtros utilizan dimensiones iguales para todos los pedidos (por ejemplo, el `gender`, user&#39;s `age` o del usuario `source`)

Esto se debe a que esta perspectiva se basa en una dimensión denominada `User's order number` para la segmentación, que indica las compras de un usuario (por ejemplo, el primer, el segundo y el tercer pedidos de John).

Si se agregara un filtro que utilice una dimensión que no sea igual para todos los pedidos (por ejemplo, `Order's Region`), el `User's order number` ya no sería precisa, ya que no tiene en cuenta regiones específicas a la hora de numerar los pedidos de un usuario (por ejemplo, el primer, el segundo, el tercer pedido de John siguen siendo iguales, independientemente de su región).

## Conversión de una dimensión específica de pedido en una dimensión específica del usuario

En algunos casos, es posible que podamos convertir un `order-specific` dimensión en un `user-specific` dimensión que se agregará como filtro en la `Repeat Order Probability` gráfico. En estos casos, se devolverá el atributo de pedido del primer pedido o del último pedido de un usuario (por ejemplo, el nombre de región de pedido del usuario).

Si desea crear una dimensión nueva de este tipo, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Comparación de la probabilidad de repetición de pedidos con atributos diferentes

Para comparar el número de compras repetidas para diferentes atributos de pedido (por ejemplo, el `region`), se recomienda crear un gráfico similar a `Users by lifetime number of orders` que muestra el número de usuarios que realizaron 1, 2, 3,... el número de pedidos acumulado y agrega el filtro de nivel de pedido. (es decir, esto puede mostrar si los usuarios realizan más o menos compras repetidas en una región u otra).

Los números que componen un gráfico de este tipo se pueden exportar a excel para calcular la relación de probabilidad de pedidos repetidos. Para ver la probabilidad de los clientes que `(x)` pedidos para realizar `(x+1)` pedidos, simplemente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Ejemplo:

|  |  |
|---|---|
| Número de clientes que han realizado una compra durante su vida útil | `90` |
| Número de clientes que han realizado dos compras durante su vida útil | `30` |
| Número de clientes que han realizado tres compras durante su vida útil | `10` |
| La probabilidad de pedido repetido de clientes que han realizado una compra durante su vida útil para realizar una segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
