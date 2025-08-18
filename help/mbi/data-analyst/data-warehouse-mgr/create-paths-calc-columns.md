---
title: Crear o eliminar rutas para columnas calculadas
description: Aprenda a definir una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Crear o eliminar rutas para columnas calculadas

## Actualizador de columnas calculadas

Al [crear columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) en su Data Warehouse, se le pide que defina una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información. Para crear correctamente una ruta, debe saber dos cosas:

1. Cómo se relacionan entre sí las tablas de las bases de datos
1. Las claves principales y externas que definen esta relación

Si conoce esta información, puede crear fácilmente una ruta siguiendo las instrucciones de este tema. Es posible que desee preguntar a un experto técnico de su organización o ponerse en contacto con el [equipo de Servicios profesionales](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Actualizadores en relaciones de tabla y tipos de clave {#refresher}

### Relaciones de tabla {#relationships}

Este concepto se explica en el artículo [Comprensión y evaluación de las relaciones entre tablas](../../data-analyst/data-warehouse-mgr/table-relationships.md), pero un resumen rápido no lastimará a nadie, ¿no es así?

Las tablas se pueden relacionar entre sí de una de las tres maneras siguientes:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | La relación entre las personas y los números de licencia de conducir. Una persona sólo puede tener un número de licencia de conducir, y un número de licencia de conducir pertenece a una sola persona. |
| **`one-to-many`** | La relación entre pedidos y artículos: un pedido puede contener muchos artículos, pero un artículo pertenece a un único pedido. En este caso, la tabla pedidos es el lado uno y la tabla elementos es el lado varios. |
| **`many-to-many`** | La relación entre productos y categorías: un producto puede pertenecer a muchas categorías y una categoría puede contener muchos productos. |

{style="table-layout:auto"}

Cuando se entiende una relación entre dos tablas, se puede utilizar para determinar qué ruta se debe crear para llevar la información de una tabla a otra. El siguiente paso requiere conocer las claves principales y externas que facilitan una relación de tabla.

### Claves principales y externas {#keys}

Un(a) `Primary Key` es una columna o conjunto de columnas que no cambia y que produce valores únicos dentro de una tabla. Por ejemplo, cuando un cliente hace un pedido en un sitio web, se agrega una nueva fila a la tabla `orders` del carro de compras, con un nuevo `order_id`. Este(a) `order_id` permite que tanto el cliente como la empresa realicen un seguimiento del progreso de ese pedido específico. Como el id. de pedido es único, suele ser el `Primary Key` de una tabla `orders`.

Un `Foreign Key` es una columna creada dentro de una tabla que se vincula a la columna `Primary Key` de otra tabla. Las claves externas crean referencias entre tablas, lo que permite a los analistas buscar y vincular registros fácilmente. Supongamos que desea saber qué pedidos pertenecían a cada uno de sus clientes. La columna `customer id` (`Primary Key` de la tabla `customers`) y la columna `order_id` (`Foreign Key` en la tabla `customers`, que hace referencia a `Primary Key` de la tabla `orders`) nos permiten vincular y analizar esta información. Al crear una ruta de acceso, se le pide que defina `Primary Key` y `Foreign Key`.

## Creación de una ruta {#createpath}

Al crear una columna en Data Warehouse, debe definir la ruta que lleva la información de una tabla a otra. A veces, las rutas se rellenan previamente porque existe una ruta entre las tablas, pero si esto no sucede, debe crear una.

Use la relación entre **clientes** y **pedidos** para mostrarle cómo se hace. Desglosado:

* La relación es `one-to-many`: un cliente puede tener muchos pedidos, pero un pedido solo puede tener un cliente. Esto indica la dirección de la relación o dónde se debe crear la columna calculada. En este caso, significa que la información de la tabla `orders` se puede incluir en la tabla `customers`.
* El `primary key` que desea usar es `customers.customerid` o la columna `customer ID` de la tabla `customers`.
* El `foreign key` que desea usar es `orders.customerid` o la columna `customer ID` de la tabla `orders`.

Ahora puede crear la ruta.

1. Haga clic en **[!UICONTROL Data > Data Warehouse]**.
1. En la lista de la tabla, haga clic en la tabla en la que desea crear la columna. En este ejemplo, es la tabla `customers`.
1. Se muestra el esquema de tabla. Haga clic en **[!UICONTROL Create New Column]**.
1. Asigne un nombre a la columna, por ejemplo, `Customer's orders`.
1. Seleccione la definición de la columna. Consulte la [Guía de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) para ver una hoja de trucos práctica.
1. En el menú desplegable [!UICONTROL Select table and column], haga clic en la opción **[!UICONTROL Create new path]**.

   ![Creando rutas de acceso para las columnas calculadas modal](../../assets/Creating_Paths_modal.png)

1. En los menús desplegables, seleccione las claves principales y externas de cada tabla.

   En el lado `Many`, selecciona `orders.customerid`. Recuerde que los clientes pueden tener muchos pedidos.

   En el lado `One`, selecciona `customers.customerid`; un pedido solo puede tener un cliente.

1. Haga clic en **[!UICONTROL Save]** para guardar la ruta y terminar de crear la columna.

### Limitaciones de la creación de rutas {#limits}

* **[!DNL Commerce Intelligence]no puede adivinar las relaciones de clave principal/externa**. No desea introducir datos incorrectos en su cuenta, por lo que la creación de rutas debe realizarse manualmente.

* **Actualmente, las rutas sólo se pueden especificar entre dos tablas diferentes**. ¿La lógica que intenta volver a crear implica más de dos tablas? Entonces puede tener sentido (1) unir las columnas a una tabla intermedia primero, luego a la tabla de &quot;destino final&quot;, o (2) consultar con el equipo de [Servicios profesionales](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para encontrar el mejor enfoque a sus objetivos.

* **Una columna solo puede ser la referencia de clave externa para una ruta de acceso al mismo tiempo**. Por ejemplo, si `order_items.order_id` señala a `orders.id`, entonces `order_items.order_id` no puede señalar a nada más.

* Técnicamente, se pueden crear **`Many-to-many`rutas de acceso, pero a menudo producen datos incorrectos porque ninguno de los lados es una clave externa `one-to-many` verdadera**. La mejor manera de abordar estas rutas siempre depende del análisis deseado específico. Consulte al equipo de analistas de RJ para descubrir la mejor solución.

Si no puede crear una columna calculada debido a una o más de las limitaciones anteriores, póngase en contacto con el servicio de asistencia técnica proporcionando una descripción de la columna que está utilizando

## Eliminar una ruta de columna calculada {#delete}

¿Ha creado una ruta incorrecta en su Data Warehouse? ¿O tal vez estás haciendo una pequeña limpieza de primavera y quieres ordenarlo? Si necesitas eliminar una ruta de acceso de tu cuenta, [puedes enviar un ticket a los analistas de asistencia de Adobe](../../guide-overview.md#Submitting-a-Support-Ticket). **¡Asegúrese de incluir el nombre de la ruta de acceso!**

## Ajuste {#wrapup}

Ahora que se siente cómodo creando rutas para columnas calculadas en su Data Warehouse. Si aún no está seguro de una ruta de acceso determinada, recuerde que siempre puede hacer clic en **[!UICONTROL Support]** en su cuenta de [!DNL Commerce Intelligence] para obtener ayuda.

## Relacionado

* [Explicación y evaluación de las relaciones de tabla](../data-warehouse-mgr/table-relationships.md)
* [Creación de rutas para columnas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) que intentan crear.
