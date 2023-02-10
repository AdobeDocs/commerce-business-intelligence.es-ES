---
title: Datos de Spree esperados
description: Explore las tablas de datos principales que puede importar desde Spree a su [!DNL MBI] cuenta.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Esperado [!DNL Spree] data

Después de [conectado el [!DNL Spree] almacenar](../../../data-analyst/importing-data/integrations/spree.md), puede usar la variable [Administrador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes desde su [!DNL Spree] para análisis.

En este artículo, exploramos las principales tablas de datos desde las que puede importar [!DNL Spree] en el [!DNL MBI] cuenta, incluidos los vínculos a [documentación adicional](https://guides.spreecommerce.org/developer/addresses.html#address) about [!DNL Spree] datos.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Users` | La variable `users` incluye los detalles de la cuenta de los clientes registrados, incluido el correo electrónico, el nombre y la fecha de registro del individuo. Esto le permite analizar diferentes segmentos de clientes y sus comportamientos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La variable `orders` sirve como base para todas las métricas de nivel de pedido. Registrados aquí son todos los detalles de pedidos de sus compras [!DNL Spree] tienda, incluido `completed\_at` (la marca de tiempo del pedido), `user\_id` (id del usuario registrado que realizó el pedido). Si el pedido fue realizado por un usuario registrado, la variable `user\_id` volverá a vincularse a la `users` para permitir un análisis del comportamiento de compra de los usuarios. |
| `Line items` | La variable `line\_items` es un elemento secundario de `orders` tabla o `subscriptions`. Registra los detalles del elemento de línea de un pedido o de una suscripción. Para pedidos con varios productos, cada producto tendrá su propia fila de datos en esta tabla, incluido un `product\_id` que le permite vincularlo al `Products` tabla. |
| `Products` | La variable `products` registra todos los detalles del producto de un artículo vendible en su catálogo de Spree. Esto le permite segmentar las métricas de nivel de elemento de línea por atributos de producto. |
| `Subscriptions` | Si tiene una [!DNL Spree] extensión de suscripciones, la variable `subscriptions` contiene la información de cada suscripción individual, incluido el `created\_at` (la fecha de inicio), `cancelled\_at` (la fecha en la que se canceló una suscripción) y `interval` de la suscripción. |

{style=&quot;table-layout:auto&quot;}

## Relacionado:

* [Conexión [!DNL Spree]](../integrations/spree.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
