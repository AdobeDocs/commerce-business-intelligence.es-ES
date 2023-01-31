---
title: Pedidos
description: Obtenga información sobre el impacto que los pedidos de los invitados tienen en los datos y las opciones que debe tener en cuenta para los pedidos de los clientes en su [!DNL MBI] almacén de datos.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Pedidos invitados

Mientras revisa sus pedidos, si nota que `customer\_id` los valores son nulos o no tienen un valor para unirse a la `customers` , esto suele indicar que su tienda permite pedidos de clientes. Esto significa que su `customers` es muy probable que la tabla no incluya a todos sus clientes.

En este tema analizamos el impacto que los pedidos de los clientes tienen en sus datos y las opciones que tiene para tener en cuenta adecuadamente los pedidos de los clientes en su [!DNL MBI] almacén de datos.

## Impacto de los pedidos de clientes en los datos

En la base de datos de comercio típica, hay un `orders` tabla que se une a un `customers` tabla. Cada fila del `orders` la tabla tiene un `customer\_id` que es única para una fila de la columna `customers` tabla.

* **Si todos los clientes están registrados** y los pedidos de invitado no están permitidos, lo que significa que cada registro de la variable `orders` tiene un valor en la variable `customer\_id` para abrir el Navegador. Como resultado, cada pedido se une de nuevo al `customers` tabla. Puede verlo en la imagen de abajo.

   ![](../../assets/guest-orders-4.png)

* **Si se permiten pedidos de invitado**, esto significa que algunos pedidos no tienen un valor en la variable `customer\_id` para abrir el Navegador. Solo los clientes registrados reciben un valor para la variable `customer\_id` en la columna `orders` tabla. Los clientes que no estén registrados recibirán un `NULL` (o en blanco) para esta columna. Como resultado, no todos los registros de pedidos tendrán registros coincidentes en la variable `customers` tabla.

   >[!NOTE]
   >
   >Para identificar al individuo único que realizó el pedido, debe haber otro atributo de usuario único al lado `customer\_id` se adjunta a un pedido. Normalmente, se utiliza la dirección de correo electrónico del cliente.

## Cómo contabilizar los pedidos de los clientes en la configuración del almacén de datos

Normalmente, el ingeniero de ventas que implementa su cuenta tendrá en cuenta los pedidos de los clientes al crear la base del almacén de datos.

La manera más óptima de contabilizar los pedidos de los clientes es basar todas las métricas de nivel de cliente en la variable `orders` tabla. Esta configuración utiliza un ID de cliente único que tienen todos los clientes, incluidos los clientes (normalmente se utiliza el correo electrónico del cliente). Esto ignora los datos de registro del `customers` tabla. Con esta opción, solo los clientes que hayan realizado al menos una compra se incluirán en los informes de nivel de cliente. Los usuarios registrados que aún no hayan realizado una compra no se incluirán. Con esta opción, su `New customer` se basará en la fecha de primer pedido del cliente en la variable `orders` tabla.

Puede notar que la variable `Customers we count` filtro configurado en este tipo de configuración tiene un filtro para `Customer's order number = 1`. Pensemos en por qué esto es así.

![](../../assets/guest-orders-filter-set.png)

En una situación sin pedidos de invitado, cada cliente existe como una fila única en la tabla del cliente (consulte la Imagen 1). Una métrica como `New customers` simplemente puede contar el id de esta tabla en función de `created\_at` fecha para comprender a los nuevos clientes según la fecha de registro.

En una configuración de pedidos de invitado en la que todas las métricas del cliente se basan en la variable `orders` para tener en cuenta los pedidos de los clientes, debe asegurarse de que `not counting customers twice`. Si cuenta el id de la tabla de pedidos, contará cada pedido. Si en su lugar cuenta el ID en la variable `orders` y utilice un filtro, `Customer's order number = 1`y, a continuación, va a contar cada cliente único `only one time`. Esto se aplica a todas las métricas de nivel de cliente, como `Customer's lifetime revenue` o `Customer's lifetime number of orders`.

En la imagen 2 anterior, puede ver que hay null `customer\_ids` en el `orders` tabla. Si usamos la variable `customer\_email` para identificar clientes únicos, puede ver que `erin@test.com` ha realizado tres (3) pedidos. Por lo tanto, podemos construir un `New customers` en su `orders` en función de las condiciones siguientes:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
