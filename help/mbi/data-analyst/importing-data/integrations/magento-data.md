---
title: Datos de comercio esperados
description: Explorar las principales tablas de datos que los usuarios de Comercio importan en MBI
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Datos de comercio esperados

Después de [conectado a la tienda de comercio](../../../data-analyst/importing-data/integrations/magento.md), puede utilizar el Administrador de Datas Warehouse para rastrear fácilmente los campos de datos relevantes de la base de datos de Commerce para su análisis.

En este artículo, exploramos las principales tablas de datos en las que importan los usuarios de Comercio [!DNL MBI].

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| `Customers` | La variable `customer\_entity` y las tablas relacionadas describen la información asociada a cada *cliente registrado* en la base de datos, como su dirección de correo electrónico y la fecha de registro. Con esta información, puede empezar a segmentar por atributos y cohortes de nivel de cliente. |
| `Orders` | La variable `sales\_flat\_order` la tabla registra todos los pedidos, incluido el `created\_at` marca de tiempo de que se realizó el pedido y la variable `base\_grand\_total` que resume los ingresos. Estos campos constituyen la base de las métricas de nivel de pedido. Si el pedido fue realizado por un *cliente registrado*, el `customer\_id` se vinculará de nuevo al  `customer\_entity` para permitir un análisis del comportamiento de compra de los clientes. |
| `Order items` | La variable `sales\_flat\_order\_item` la tabla registra cada elemento que pertenece a un pedido. Esto incluye el `price` y `qty\_ordered` , así como los campos `order\_id` que se conecta a la función `sales\_flat\_order` tabla. Esta tabla es la base de métricas como `Item sold`, y le permite segmentar por `product` y `product type`. |
| `Products` | La variable `catalog\_product\_entity` la tabla almacena información sobre atributos de nivel de producto, como categoría, tamaño y color. |
| `Categories` | Sus productos pertenecerán a uno o varios `product categories`, según la configuración de la compilación de Commerce. La variable `catalog\_category\_entity` La tabla almacena la jerarquía de estas categorías (Apr > Tops > T-Shirts, por ejemplo) y la `catalog\_category\_product` registra las conexiones entre sus productos y esas categorías. |

{style=&quot;table-layout:auto&quot;}

## Relacionado

* [Conexión [!DNL Magento]](../integrations/magento.md)
* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
