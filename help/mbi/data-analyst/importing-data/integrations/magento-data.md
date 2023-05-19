---
title: Datos de comercio esperados
description: Explore las principales tablas de datos que los usuarios de Commerce importan en Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Previsto [!DNL Adobe Commerce] Datos

Después de que tenga [conectó su [!DNL Adobe Commerce] almacenar](../../../data-analyst/importing-data/integrations/magento.md), puede utilizar el Administrador de Datas Warehouse para rastrear fácilmente los campos de datos relevantes de la base de datos de Commerce para su análisis.

En este tema se exploran las tablas de datos principales a las que se importan los usuarios de Commerce [!DNL Commerce Intelligence].

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Customers` | El `customer\_entity` y las tablas relacionadas describen la información asociada a cada uno *cliente registrado* en la base de datos, como su dirección de correo electrónico y fecha de registro. Con esta información, puede empezar a segmentar por atributos y cohortes de nivel de cliente. |
| `Orders` | El `sales\_flat\_order` registra todos los pedidos, incluido el `created\_at` marca de tiempo de realización del pedido y la `base\_grand\_total` que resume los ingresos. Estos campos son la base de las métricas de nivel de pedido. Si el pedido fue realizado por un *cliente registrado*, el `customer\_id` vínculos de campo de nuevo a  `customer\_entity` para permitir el análisis del comportamiento de compra de los clientes. |
| `Order items` | El `sales\_flat\_order\_item` registra cada elemento que pertenece a un pedido. Esto incluye el `price` y `qty\_ordered` y los campos de `order\_id` que se conecta al `sales\_flat\_order` tabla. Esta tabla es la base de métricas como `Item sold`y le permite segmentar por `product` y `product type`. |
| `Products` | El `catalog\_product\_entity` La tabla almacena información sobre atributos de nivel de producto, como categoría, tamaño y color. |
| `Categories` | Sus productos pertenecen a uno o varios productos diferentes `product categories`, según cómo esté configurada su compilación de Commerce. El `catalog\_category\_entity` La tabla almacena la jerarquía de estas categorías (Ropa > Parte superior > Camisetas, por ejemplo), y la variable `catalog\_category\_product` registra las conexiones entre sus productos y esas categorías. |

{style="table-layout:auto"}

## Relacionado

* [Conectando [!DNL Adobe Commerce]](../integrations/magento.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
