---
title: Datos de Spree esperados
description: Explore las tablas de datos principales que puede importar desde Spree a su cuenta de  [!DNL Commerce Intelligence] name.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Se esperaban [!DNL Spree] datos

Después de haber [conectado tu [!DNL Spree] tienda](../../../data-analyst/importing-data/integrations/spree.md), puedes usar el [Administrador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes de tu plataforma [!DNL Spree] para su análisis.

En este tema se exploran las tablas de datos principales que puede importar de [!DNL Spree] a su cuenta de [!DNL Commerce Intelligence], incluidos los vínculos a [documentación adicional](https://guides.spreecommerce.org/developer/addresses.html#address) acerca de [!DNL Spree] datos.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Users` | La tabla `users` incluye los detalles de la cuenta de los clientes registrados, incluido el correo electrónico, el nombre y la fecha de registro de la persona. Esto le permite analizar diferentes segmentos de clientes y sus comportamientos de compra. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La tabla `orders` sirve como base para todas las métricas de nivel de pedido. Aquí se registran todos los detalles de pedidos de compras de su tienda [!DNL Spree], incluyendo `completed\_at` (la marca de tiempo del pedido), `user\_id` (id. del usuario registrado que realizó el pedido). Si el pedido lo realizó un usuario registrado, `user\_id` vuelve a vincular la tabla `users` para permitir el análisis del comportamiento de compra del usuario. |
| `Line items` | La tabla `line\_items` es secundaria de la tabla `orders` o de `subscriptions`. Registra los detalles de elemento de línea de un pedido o una suscripción. Para pedidos con varios productos, cada producto tiene su propia fila de datos en esta tabla, incluido un `product\_id` que le permite vincularla a la tabla `Products`. |
| `Products` | La tabla `products` registra todos los detalles del producto de un artículo que se puede vender en su catálogo Spree. Esto le permite segmentar las métricas de nivel de elemento de línea por atributos de producto. |
| `Subscriptions` | Si tiene una extensión de suscripciones [!DNL Spree], la tabla `subscriptions` contiene la información de cada suscripción individual, incluido `created\_at` (la fecha de inicio), `cancelled\_at` (la fecha en la que se canceló una suscripción) y `interval` de la suscripción. |

{style="table-layout:auto"}

## Relacionado:

* [Conectando [!DNL Spree]](../integrations/spree.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
