---
title: Datos Commerce esperados
description: Explore las tablas de datos principales que los usuarios de Commerce importan en Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
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
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
