---
title: Formato e importación de datos de comercio electrónico
description: Conozca los formatos de datos ideales para utilizar para cargar datos de comercio electrónico.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Formato e importación de datos

Si utiliza una integración que actualmente no admite [!DNL MBI], puede seguir utilizando la variable [Función de carga de archivos](using-file-uploader.md) para introducir los datos en la Data Warehouse. Este artículo describe los formatos de datos ideales para utilizar en la carga de datos de comercio electrónico.

## `Orders` tabla

El `orders` debe contener una fila por cada transacción que la empresa haya realizado. Las columnas potenciales incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Order ID` | El ID de pedido debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer` | El cliente que realizó el pedido. |
| `Order total` | El total del pedido. Puede ser una columna basada en el cálculo, donde los valores de otras columnas, como subtotal y envío, constituyen el total de esta columna. |
| `Currency` | La divisa en la que se pagó el pedido. Incluya si es relevante. |
| ` Order status` | El estado del pedido, como `In Progress`, `Refunded`, o `Complete`. El valor de esta columna cambia (si no está completo). Los datos nuevos y actualizados se pueden importar mediante el [Función Anexar datos](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) en el `File Uploads` página. |
| `Acquisition/marketing channel` | El canal de adquisición o marketing desde el que se refirió el cliente que realizó el pedido. |
| `Order datetime` | La fecha y la hora de creación del pedido. |
| `Order updated at` | La fecha y la hora en que se realizó la última modificación en el registro de pedido. |

{style="table-layout:auto"}

## `Order detail/items` tabla {#itemstable}

El `order_detail / items` La tabla debe contener una fila para cada elemento distinto en cada orden. Las columnas potenciales incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Order item ID` | El ID de elemento de pedido debe ser único para cada fila de la tabla. Además, esto suele ser el `primary key` para la tabla. |
| `Order ID` | El ID del pedido. |
| `Product ID` | ID del producto. |
| `Product name` | El nombre del producto. |
| `Product's unit price` | El precio de una sola unidad del producto. |
| `Quantity` | La cantidad del producto en el pedido. |

## `Customers` tabla {#customerstable}

El `customers` debe contener una fila por cada cuenta de cliente. Las columnas potenciales incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Customer ID` | El ID de cliente debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer created at` | La fecha y hora de creación de la cuenta del cliente. |
| `Customer modified at` | La fecha y la hora de la última modificación de la cuenta del cliente. |
| `Acquisition/marketing channel source` | El canal de adquisición o marketing desde el que se refirió al cliente. |
| `Demographic info` | La información demográfica, como el intervalo de edad y el sexo, se puede utilizar para segmentar los informes. |
| `Acquisition/marketing channel` | El canal de adquisición o marketing desde el que se refirió el cliente que realizó el pedido. |

## `Subscription payments` tabla

El `subscriptions` La tabla debe contener una fila por cada pago de suscripción. Las columnas potenciales incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Subscription ID` | El ID de suscripción debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer ID` | El ID del cliente que realizó el pago. |
| `Payment amount` | El importe del pago de suscripción. |
| `Start date` | La fecha y hora de inicio del período que abarca el pago. |
| `End date` | La fecha y hora de finalización del período que abarca el pago. |
