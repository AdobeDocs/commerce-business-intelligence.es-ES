---
title: Pedidos de invitado
description: Obtenga información sobre el impacto que tienen los pedidos de invitados en sus datos y qué opciones tiene para tener en cuenta correctamente los pedidos de invitados en su  [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/leSf21lcOaEbm1aehC8iZLdbtRJFKK9yVQwdvft-GKQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 566
ht-degree: 0%

---

# Pedidos de invitado

Al revisar sus pedidos, si observa que muchos valores de `customer\_id` son nulos o no tienen un valor para volver a unirse a la tabla `customers`, esto indica que su tienda permite pedidos de invitado. Esto significa que es muy probable que la tabla `customers` no incluya a todos los clientes.

En este tema se describe el impacto que tienen los pedidos de invitados en los datos y qué opciones tiene para tener en cuenta correctamente los pedidos de invitados en la Data Warehouse [!DNL Commerce Intelligence].

## Impacto de los pedidos de invitados en los datos

En la base de datos de comercio típica, hay una tabla `orders` que se une a una tabla `customers`. Cada fila de la tabla `orders` tiene una columna `customer\_id` que es única para una fila de la tabla `customers`.

* **Si todos los clientes están registrados** y no se permiten pedidos de invitado, significa que cada registro de la tabla `orders` tiene un valor en la columna `customer\_id`. Como resultado, cada pedido se vuelve a unir a la tabla `customers`.

  ![Tabla de datos de pedidos de invitado que muestra información de clientes](../../assets/guest-orders-4.png)

* **Si se permiten pedidos de invitado**, significa que algunos pedidos no tienen un valor en la columna `customer\_id`. Solo los clientes registrados reciben un valor para la columna `customer\_id` en la tabla `orders`. Los clientes que no están registrados reciben un valor `NULL` (o en blanco) para esta columna. Como resultado, no todos los registros de pedidos tienen registros coincidentes en la tabla `customers`.

  >[!NOTE]
  >
  >Para identificar al individuo único que realizó el pedido, debe haber otro atributo de usuario único junto a `customer\_id` adjunto a un pedido. Normalmente, se utiliza la dirección de correo electrónico del cliente.

## Cómo contabilizar pedidos de invitados en la configuración de Data Warehouse

Normalmente, el ingeniero de ventas que implementa su cuenta tiene en cuenta los pedidos de los invitados al crear la base de su Data Warehouse.

La forma más óptima de tener en cuenta los pedidos de invitados es basar todas las métricas de nivel de cliente en la tabla `orders`. Esta configuración utiliza un ID de cliente único que tienen todos los clientes, incluidos los invitados (normalmente se utiliza el correo electrónico del cliente). Esto ignora los datos de registro de la tabla `customers`. Con esta opción, solo se incluyen en los informes de nivel de cliente los clientes que han realizado al menos una compra. No se incluyen los usuarios registrados que aún no hayan realizado una compra. Con esta opción, la métrica `New customer` se basa en la primera fecha de pedido del cliente en la tabla `orders`.

Observará que el filtro `Customers we count` establecido en este tipo de configuración tiene un filtro para `Customer's order number = 1`.

![Configuración del conjunto de filtros para excluir pedidos de invitado](../../assets/guest-orders-filter-set.png)

En una situación sin pedidos de invitado, cada cliente existe como una fila única en la tabla de clientes (consulte la imagen 1). Una métrica como `New customers` puede simplemente contar el ID de esta tabla en función de la fecha `created\_at` para comprender a los nuevos clientes en función de la fecha de registro.

En una configuración de pedidos de invitado en la que todas las métricas de clientes se basen en la tabla `orders` para tener en cuenta los pedidos de invitado, debe asegurarse de que es `not counting customers twice`. Si cuenta el ID de la tabla de pedidos, contará todos los pedidos. Si en su lugar cuenta el identificador en la tabla `orders` y usa un filtro, `Customer's order number = 1`, entonces va a contar cada cliente único `only one time`. Esto es aplicable a todas las métricas de nivel de cliente, tales como `Customer's lifetime revenue` o `Customer's lifetime number of orders`.

Más arriba puede ver que hay `customer\_ids` nulos en la tabla `orders`. Si usa `customer\_email` para identificar clientes únicos, verá que `erin@test.com` ha realizado tres (3) pedidos. Por lo tanto, puede generar una métrica `New customers` en su tabla `orders` en función de las siguientes condiciones:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
