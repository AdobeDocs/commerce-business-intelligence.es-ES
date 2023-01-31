---
title: Formato e importación de datos de comercio electrónico
description: Aprenda los formatos de datos ideales para su uso en la carga de datos de eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Formato e importación de datos

Si está utilizando una integración que actualmente no admite [!DNL MBI], aún puede usar la variable [Función de carga de archivos](using-file-uploader.md) para introducir los datos en el almacén de datos. En este artículo analizamos los formatos de datos ideales para su uso en la carga de datos de eCommerce.

## `Orders` tabla

La variable `orders` debe contener una fila por cada transacción que la empresa haya realizado. Las posibles columnas incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Order ID` | El ID de pedido debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer` | El cliente que realizó el pedido. |
| `Order total` | El total del pedido. Puede tratarse de una columna basada en cálculos, en la que los valores de otras columnas, como el subtotal y el envío, constituyen el total de esta columna. |
| `Currency` | La moneda en la que se pagó el pedido. Incluya si es relevante. |
| ` Order status` | El estado del pedido, como `In Progress`, `Refunded`o `Complete`. Es probable que el valor de esta columna cambie (si no se completa). Los datos nuevos y actualizados se pueden importar mediante la variable [Función Anexar datos](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) en el `File Uploads` página. |
| `Acquisition/marketing channel` | Canal de adquisición o marketing desde el que se derivó al cliente que realizó el pedido. |
| `Order datetime` | Fecha y hora en que se creó el pedido. |
| `Order updated at` | Fecha y hora en que se realizó la última modificación del registro de pedido. |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` tabla {#itemstable}

La variable `order_detail / items` debe contener una fila para cada elemento distinto en cada orden. Las posibles columnas incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Order item ID` | El ID del elemento de pedido debe ser único para cada fila de la tabla. Además, normalmente se usa la variable `primary key` para la tabla. |
| `Order ID` | ID del pedido. |
| `Product ID` | El ID del producto. |
| `Product name` | Nombre del producto. |
| `Product's unit price` | El precio de una sola unidad del producto. |
| `Quantity` | Cantidad del producto en el pedido. |

## `Customers` tabla {#customerstable}

La variable `customers` debe contener una fila por cada cuenta de cliente. Las posibles columnas incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Customer ID` | El ID de cliente debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer created at` | La fecha y hora en que se creó la cuenta del cliente. |
| `Customer modified at` | Fecha y hora en que se modificó la cuenta del cliente por última vez. |
| `Acquisition/marketing channel source` | Canal de adquisición o marketing desde el que se hizo referencia al cliente. |
| `Demographic info` | La información demográfica, como el intervalo de edad y el sexo, se puede utilizar para segmentar los informes. |
| `Acquisition/marketing channel` | Canal de adquisición o marketing desde el que se derivó al cliente que realizó el pedido. |

## `Subscription payments` tabla

La variable `subscriptions` debe contener una fila por cada pago de suscripción. Las posibles columnas incluyen:

| Nombre de columna | Descripción |
|----|----|
| `Subscription ID` | El ID de suscripción debe ser único para cada fila de la tabla. Además, esta suele ser la clave principal de la tabla. |
| `Customer ID` | ID del cliente que realizó el pago. |
| `Payment amount` | El importe del pago de suscripción. |
| `Start date` | La fecha de inicio del periodo que cubre el pago. |
| `End date` | La fecha y hora de finalización del período que cubre el pago. |
