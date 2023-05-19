---
title: Crear o eliminar rutas para columnas calculadas
description: Aprenda a definir una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Crear o eliminar rutas para columnas calculadas

## Actualizador de columnas calculadas

Cuándo [creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) en la Data Warehouse, se le pedirá que defina una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información. Para crear correctamente una ruta, debe saber dos cosas:

1. Cómo se relacionan entre sí las tablas de las bases de datos
1. Las claves principales y externas que definen esta relación

Si conoce esta información, puede crear fácilmente una ruta siguiendo las instrucciones de este tema. Si lo desea, puede preguntar a un experto técnico de su organización o ponerse en contacto con el [Equipo de Professional Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Actualizadores en relaciones de tabla y tipos de clave {#refresher}

### Relaciones de tabla {#relationships}

Este concepto se trata en la [Explicación y evaluación del artículo de relaciones de tabla](../../data-analyst/data-warehouse-mgr/table-relationships.md), pero un resumen rápido nunca lastima a nadie, ¿verdad?

Las tablas se pueden relacionar entre sí de una de las tres maneras siguientes:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | La relación entre las personas y los números de licencia de conducir. Una persona sólo puede tener un número de licencia de conducir, y un número de licencia de conducir pertenece a una sola persona. |
| **`one-to-many`** | La relación entre pedidos y artículos: un pedido puede contener muchos artículos, pero un artículo pertenece a un único pedido. En este caso, la tabla pedidos es el lado uno y la tabla elementos es el lado varios. |
| **`many-to-many`** | La relación entre productos y categorías: un producto puede pertenecer a muchas categorías y una categoría puede contener muchos productos. |

{style="table-layout:auto"}

Cuando se entiende una relación entre dos tablas, se puede utilizar para determinar qué ruta se debe crear para llevar la información de una tabla a otra. El siguiente paso requiere conocer las claves principales y externas que facilitan una relación de tabla.

### Claves principales y externas {#keys}

A `Primary Key` es una columna o conjunto de columnas que no cambia y que produce valores únicos dentro de una tabla. Por ejemplo, cuando un cliente realiza un pedido en un sitio web, se agrega una nueva fila a la `orders` en el carro de compras, con una nueva `order_id`. Esta `order_id` permite al cliente y a la empresa realizar un seguimiento del progreso de ese pedido específico. Dado que el ID de pedido es único, suele ser el `Primary Key` de un `orders` tabla.

A `Foreign Key` es una columna creada dentro de una tabla que se vincula a la `Primary Key` de otra tabla. Las claves externas crean referencias entre tablas, lo que permite a los analistas buscar y vincular registros fácilmente. Supongamos que desea saber qué pedidos pertenecían a cada uno de sus clientes. El `customer id` column (`Primary Key` de la `customers` tabla) y el `order_id` column (`Foreign Key` en el `customers` tabla, haciendo referencia a `Primary Key` de la `orders` tabla) nos permite vincular y analizar esta información. Al crear una ruta, se le pide que defina ambas `Primary Key` y `Foreign Key`.

## Creación de una ruta {#createpath}

Al crear una columna en la Data Warehouse, debe definir la ruta que lleva la información de una tabla a otra. A veces, las rutas se rellenan previamente porque existe una ruta entre las tablas, pero si esto no sucede, debe crear una.

Usar la relación entre **clientes** y **pedidos** para mostrarle cómo se hace. Desglosado:

* La relación es `one-to-many` - un cliente puede tener muchos pedidos, pero un pedido solo puede tener un cliente. Esto indica la dirección de la relación o dónde se debe crear la columna calculada. En este caso, significa información del `orders` se puede introducir en la `customers` tabla.
* El `primary key` que desea utilizar es `customers.customerid`, o el `customer ID` en la columna `customers` tabla.
* El `foreign key` que desea utilizar es `orders.customerid`, o el `customer ID` en la columna `orders` tabla.

Ahora puede crear la ruta.

1. Clic **[!UICONTROL Data > Data Warehouse]**.
1. En la lista de la tabla, haga clic en la tabla en la que desea crear la columna. En este ejemplo, es el `customers` tabla.
1. Se muestra el esquema de tabla. Clic **[!UICONTROL Create New Column]**.
1. Asigne un nombre a la columna, por ejemplo, `Customer's orders`.
1. Seleccione la definición de la columna. Consulte la [Guía de columna calculada](../data-warehouse-mgr/creating-calculated-columns.md) para una práctica hoja de trucos.
1. En el [!UICONTROL Select table and column] , haga clic en el **[!UICONTROL Create new path]** opción.

   ![Creación de rutas para columnas calculadas modales](../../assets/Creating_Paths_modal.png)

1. En los menús desplegables, seleccione las claves principales y externas de cada tabla.

   En el `Many` lado, seleccione `orders.customerid` - recuerde, los clientes pueden tener muchos pedidos.

   En el `One` lado, seleccione `customers.customerid` - un pedido solo puede tener un cliente.

1. Clic **[!UICONTROL Save]** para guardar la ruta y terminar de crear la columna.

### Limitaciones de la creación de rutas {#limits}

* **[!DNL Commerce Intelligence]no se pueden adivinar las relaciones de clave principal/externa**. No desea introducir datos incorrectos en su cuenta, por lo que la creación de rutas debe realizarse manualmente.

* **Actualmente, las rutas solo se pueden especificar entre dos tablas diferentes**. ¿La lógica que intenta volver a crear implica más de dos tablas? A continuación, puede tener sentido (1) unir las columnas primero a una tabla intermedia y luego a la tabla de &quot;destino final&quot;, o (2) consultar con el [Equipo de Professional Services](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para encontrar el mejor enfoque para sus objetivos.

* **Una columna solo puede ser la referencia de clave externa para UNA ruta de acceso a la vez**. Por ejemplo, si `order_items.order_id` apunta a `orders.id`, entonces `order_items.order_id` no puede señalar a nada más.

* **`Many-to-many`técnicamente, las rutas se pueden crear, pero a menudo producen datos incorrectos porque ninguno de los lados es verdadero `one-to-many` clave externa**. La mejor manera de abordar estas rutas siempre depende del análisis deseado específico. Consulte al equipo de analistas de RJ para descubrir la mejor solución.

Si no puede crear una columna calculada debido a una o más de las limitaciones anteriores, póngase en contacto con el servicio de asistencia técnica proporcionando una descripción de la columna que está utilizando

## Eliminar una ruta de columna calculada {#delete}

¿Ha creado una ruta incorrecta en su Data Warehouse? ¿O tal vez estás haciendo una pequeña limpieza de primavera y quieres ordenarlo? Si necesita eliminar una ruta de acceso de su cuenta, puede [enviar un ticket a los analistas de soporte de Adobe](../../guide-overview.md#Submitting-a-Support-Ticket). **Asegúrese de incluir el nombre de la ruta.**

## Ajuste {#wrapup}

Ahora que se siente cómodo creando rutas para las columnas calculadas en su Data Warehouse. Si todavía no está seguro de una ruta en particular, recuerde que siempre puede hacer clic en **[!UICONTROL Support]** en su [!DNL Commerce Intelligence] cuenta para obtener asistencia.

## Relacionado

* [Explicación y evaluación de las relaciones de tabla](../data-warehouse-mgr/table-relationships.md)
* [Creación de rutas para columnas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) intentando crear.
