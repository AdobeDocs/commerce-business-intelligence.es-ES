---
title: Datos de Spree esperados
description: Explore las tablas de datos principales que puede importar de Spree a su cuenta de [!DNL Commerce Intelligence].
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%
---
# Se esperaban [!DNL Spree] datos

Después de haber [conectado tu [!DNL Spree] tienda](../../../data-analyst/importing-data/integrations/spree.md), puedes usar el [Administrador de Data Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes de tu plataforma [!DNL Spree] para su análisis.

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
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
