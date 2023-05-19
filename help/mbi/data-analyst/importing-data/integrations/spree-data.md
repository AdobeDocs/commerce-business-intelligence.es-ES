---
title: Datos de Spree esperados
description: Explore las principales tablas de datos que puede importar de Spree a su [!DNL Commerce Intelligence] cuenta.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Previsto [!DNL Spree] datos

Después de que tenga [conectó su [!DNL Spree] almacenar](../../../data-analyst/importing-data/integrations/spree.md), puede utilizar el [Administrador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes desde [!DNL Spree] plataforma de análisis.

En este tema se exploran las tablas de datos principales desde las que se puede importar [!DNL Spree] en su [!DNL Commerce Intelligence] cuenta de, incluidos los vínculos a [documentación adicional](https://guides.spreecommerce.org/developer/addresses.html#address) acerca de [!DNL Spree] datos.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Users` | El `users` La tabla incluye los detalles de la cuenta de los clientes registrados, incluido el correo electrónico, el nombre y la fecha de registro de la persona. Esto le permite analizar diferentes segmentos de clientes y sus comportamientos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | El `orders` sirve como base para todas las métricas de nivel de pedido. Aquí se registran todos los detalles del pedido de las compras a su [!DNL Spree] tienda, incluyendo `completed\_at` (la marca de tiempo del pedido), `user\_id` (id del usuario registrado que realizó el pedido). Si el pedido lo ha realizado un usuario registrado, la variable `user\_id` vínculos de nuevo a `users` para permitir el análisis del comportamiento de compra del usuario. |
| `Line items` | El `line\_items` es un elemento secundario de cualquiera de las `orders` tabla o `subscriptions`. Registra los detalles de elemento de línea de un pedido o una suscripción. Para pedidos con varios productos, cada producto tiene su propia fila de datos en esta tabla, incluido un `product\_id` que le permite vincularlo al `Products` tabla. |
| `Products` | El `products` registra todos los detalles del producto de un artículo que se puede vender en su catálogo Spree. Esto le permite segmentar las métricas de nivel de elemento de línea por atributos de producto. |
| `Subscriptions` | Si tiene un [!DNL Spree] extensión de suscripciones, la `subscriptions` contiene la información de cada suscripción individual, incluyendo `created\_at` (la fecha de inicio), `cancelled\_at` (la fecha en la que se canceló una suscripción) y `interval` de la suscripción. |

{style="table-layout:auto"}

## Relacionado:

* [Conectando [!DNL Spree]](../integrations/spree.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
