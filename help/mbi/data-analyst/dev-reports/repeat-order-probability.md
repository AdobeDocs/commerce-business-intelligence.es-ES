---
title: Informe Probabilidad de Orden Repetido
description: Conozca y comprenda el Informe de Probabilidad de Pedidos Repetidos.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
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

Para comparar el número de compras repetidas para diferentes atributos de pedido (por ejemplo, `region` de pedido), Adobe recomienda crear un gráfico similar a `Users by lifetime number of orders`. Esto muestra el número de usuarios que realizaron 1, 2, 3,... un número de duración de pedidos y agregan el filtro de nivel de pedido. (en otras palabras, Esto puede mostrar si los usuarios realizan compras más o menos repetidas en una región u otra).

Los números que componen un gráfico de este tipo se pueden exportar a Excel para calcular la proporción de probabilidad de pedidos repetidos. Para ver la probabilidad de que los clientes que realizaron `(x)` pedidos realicen `(x+1)`, simplemente ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` compras.

### Ejemplo:

| Categoría | Valor |
|---|---|
| Número de clientes que realizaron una compra en su vida útil | `90` |
| Número de clientes que realizaron dos compras en su vida útil | `30` |
| Número de clientes que realizaron 3 compras en su vida útil | `10` |
| La probabilidad de repetir un pedido de los clientes que han realizado una compra en su vida útil para realizar una segunda compra | `(30 + 10) / (30+10+90) = 30.77%` |
