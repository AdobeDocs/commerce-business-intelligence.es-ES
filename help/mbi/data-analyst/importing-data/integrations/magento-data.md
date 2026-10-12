---
title: Datos Commerce esperados
description: Explore las tablas de datos principales que los usuarios de Commerce importan en Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630'
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
source-wordcount: '254'
ht-degree: 0%
---
# Se esperaban [!DNL Adobe Commerce] datos

Una vez que hayas [conectado tu [!DNL Adobe Commerce] tienda](../../../data-analyst/importing-data/integrations/magento.md), puedes usar Data Warehouse Manager para rastrear fácilmente los campos de datos relevantes de tu base de datos de Commerce para su análisis.

En este tema se exploran las tablas de datos principales que los usuarios de Commerce importan en [!DNL Commerce Intelligence].

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Customers` | `customer\_entity` y las tablas relacionadas describen la información asociada con cada *cliente registrado* en la base de datos, como su dirección de correo electrónico y fecha de registro. Con esta información, puede empezar a segmentar por atributos y cohortes de nivel de cliente. |
| `Orders` | La tabla `sales\_flat\_order` registra todos los pedidos, incluida la marca de tiempo `created\_at` en la que se realizó el pedido y el campo `base\_grand\_total` que resume los ingresos. Estos campos son la base de las métricas de nivel de pedido. Si el pedido fue realizado por un *cliente registrado*, el campo `customer\_id` se vincula de nuevo a la tabla `customer\_entity` para permitir el análisis del comportamiento de compra de los clientes. |
| `Order items` | La tabla `sales\_flat\_order\_item` registra cada elemento que pertenece a un pedido. Esto incluye los campos `price` y `qty\_ordered`, y el campo `order\_id` que se conecta a la tabla `sales\_flat\_order`. Esta tabla es la base de métricas como `Item sold`, y le permite segmentar por `product` y `product type`. |
| `Products` | La tabla `catalog\_product\_entity` almacena información sobre atributos de nivel de producto, como categoría, tamaño y color. |
| `Categories` | Sus productos pertenecen a uno o varios `product categories` diferentes, según la configuración de la compilación de Commerce. La tabla `catalog\_category\_entity` almacena la jerarquía de estas categorías (Ropa > Parte superior > Camisetas, por ejemplo) y la tabla `catalog\_category\_product` registra las conexiones entre sus productos y esas categorías. |

{style="table-layout:auto"}

## Relacionado

* [Conectando [!DNL Adobe Commerce]](../integrations/magento.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
