---
title: Informe Probabilidad de Orden Repetido
description: Conozca y comprenda el Informe de Probabilidad de Pedidos Repetidos.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Informe Probabilidad de Orden Repetido

## ¿Cuándo es el `Incremental Event Probability` ¿perspectiva disponible?

El `incremental event probability` La perspectiva solo está disponible cuando los filtros utilizan dimensiones iguales para todos los pedidos (por ejemplo, el del usuario `gender`, del usuario `age` o del usuario `source`)

Esto se debe a que esta perspectiva se basa en una dimensión denominada `User's order number` para la segmentación, que numera las compras de un usuario (por ejemplo, los pedidos primero, segundo y tercero de John).

Si ha añadido un filtro que utiliza una dimensión que no es igual para todos los pedidos (por ejemplo, `Order's Region`), el `User's order number` ya no sería precisa. Esto se debe a que no tiene en cuenta regiones específicas al numerar los pedidos de un usuario (por ejemplo, los pedidos primero, segundo y tercero de John siguen siendo los mismos, independientemente de su región).

## Conversión de una dimensión específica del pedido en una dimensión específica del usuario

En determinados casos, es posible que pueda convertir un `order-specific` dimensión en una `user-specific` dimensión para agregar como filtro en `Repeat Order Probability` gráfico. En estos casos, se devuelve el atributo order del primer pedido o del último pedido de un usuario (por ejemplo, el nombre de región de primer pedido del usuario).

Si desea crear una dimensión tan nueva, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Comparación de la probabilidad de repetición de pedidos con atributos diferentes

Para comparar el número de compras repetidas para diferentes atributos de pedido (por ejemplo, pedidos `region`), Adobe recomienda crear un gráfico similar a `Users by lifetime number of orders`. Esto muestra el número de usuarios que realizaron 1, 2, 3,... un número de duración de pedidos y agregan el filtro de nivel de pedido. (en otras palabras, Esto puede mostrar si los usuarios realizan compras más o menos repetidas en una región u otra).

Los números que componen un gráfico de este tipo se pueden exportar a Excel para calcular la proporción de probabilidad de pedidos repetidos. Para ver la probabilidad de que los clientes realicen `(x)` órdenes para hacer `(x+1)` pedidos, simplemente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Ejemplo:

|  |  |
|---|---|
| Número de clientes que realizaron una compra en su vida útil | `90` |
| Número de clientes que realizaron dos compras en su vida útil | `30` |
| Número de clientes que realizaron 3 compras en su vida útil | `10` |
| La probabilidad de repetir un pedido de los clientes que han realizado una compra en su vida útil para realizar una segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
