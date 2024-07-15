---
title: Informe Probabilidad de Orden Repetido
description: Conozca y comprenda el Informe de Probabilidad de Pedidos Repetidos.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Informe Probabilidad de Orden Repetido

## ¿Cuándo está disponible la perspectiva `Incremental Event Probability`?

La perspectiva `incremental event probability` solo está disponible cuando los filtros utilizan dimensiones iguales para todos los pedidos (por ejemplo, `gender` del usuario, `age` del usuario o `source` del usuario).

Esto se debe a que esta perspectiva se basa en una dimensión denominada `User's order number` para la segmentación, que numera las compras de un usuario (por ejemplo, los pedidos primero, segundo y tercero de John).

Si agregó un filtro que utiliza una dimensión que no es igual para todos los pedidos (por ejemplo, `Order's Region`), la dimensión `User's order number` ya no sería precisa. Esto se debe a que no tiene en cuenta regiones específicas al numerar los pedidos de un usuario (por ejemplo, los pedidos primero, segundo y tercero de John siguen siendo los mismos, independientemente de su región).

## Conversión de una dimensión específica del pedido en una dimensión específica del usuario

En determinados casos, es posible que pueda convertir una dimensión `order-specific` en una dimensión `user-specific` para agregarla como filtro en el gráfico `Repeat Order Probability`. En estos casos, se devuelve el atributo order del primer pedido o del último pedido de un usuario (por ejemplo, el nombre de región de primer pedido del usuario).

Si desea crear una dimensión nueva de este tipo, [póngase en contacto con el soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Comparación de la probabilidad de repetición de pedidos con atributos diferentes

Para comparar el número de compras repetidas para diferentes atributos de pedidos (por ejemplo, `region` del pedido), Adobe recomienda crear un  similar a `Users by lifetime number of orders`. Esto muestra el número de usuarios que realizaron 1, 2, 3,... un número de duración de pedidos y agregan el filtro de nivel de pedido. (en otras palabras, Esto puede mostrar si los usuarios realizan compras más o menos repetidas en una región u otra).

Los números que componen un gráfico de este tipo se pueden exportar a Excel para calcular la proporción de probabilidad de pedidos repetidos. Para ver la probabilidad de que los clientes que realizaron `(x)` pedidos realicen `(x+1)`, simplemente ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Ejemplo:

| Categoría | Valor |
|---|---|
| Número de clientes que realizaron una compra en su vida útil | `90` |
| Número de clientes que realizaron dos compras en su vida útil | `30` |
| Número de clientes que realizaron 3 compras en su vida útil | `10` |
| La probabilidad de repetir un pedido de los clientes que han realizado una compra en su vida útil para realizar una segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
