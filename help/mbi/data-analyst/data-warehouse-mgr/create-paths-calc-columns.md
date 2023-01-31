---
title: Crear o eliminar rutas para columnas calculadas
description: Aprenda a definir una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Crear o eliminar rutas para columnas calculadas

## Actualización de columnas calculadas

When [creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) en la Data Warehouse, se le pedirá que defina una ruta que describa cómo la tabla en la que está creando una columna está relacionada con la tabla de la que está extrayendo información. Para crear correctamente una ruta, debe saber dos cosas:

1. Relación entre las tablas de las bases de datos
1. Las claves principal y externa que definen esta relación

Si conoce esta información, podrá crear fácilmente una ruta siguiendo las instrucciones de este artículo. Hemos proporcionado información general sobre estos conceptos si no está seguro, pero puede que desee preguntar a un experto técnico de su organización o ponerse en contacto con nuestro equipo de asistencia.

## Actualizaciones en las relaciones de tabla y los tipos de claves {#refresher}

### Relaciones de tabla {#relationships}

Hemos cubierto este concepto en profundidad en nuestra [Artículo Explicación y evaluación de las relaciones de tabla](../../data-analyst/data-warehouse-mgr/table-relationships.md), pero un breve resumen nunca hirió a nadie, ¿verdad?

Las tablas se pueden relacionar entre sí de una de las tres maneras siguientes:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | Relación entre personas y números de licencia de conducir. Una persona puede tener un número de licencia de conducir y un número de licencia de conducir pertenece a una sola persona. |
| **`one-to-many`** | La relación entre pedidos y artículos: un pedido puede contener muchos artículos, pero un artículo pertenece a un único pedido. En este caso, la tabla de pedidos es de una parte y la tabla de artículos es de muchas. |
| **`many-to-many`** | Relación entre productos y categorías: un producto puede pertenecer a muchas categorías y una categoría puede contener muchos productos. |

{style=&quot;table-layout:auto&quot;}

Una vez entendida la relación entre dos tablas, se puede utilizar para determinar qué ruta se debe crear para llevar la información de una tabla a otra. Este paso siguiente requiere conocer las claves principal y externa que facilitan la relación de tabla.

### Claves principales y extranjeras {#keys}

A `Primary Key` es una columna o conjunto de columnas que no cambia y que produce valores únicos dentro de una tabla. Por ejemplo, cuando un cliente realiza un pedido en un sitio web, se agrega una fila nueva al `orders` en el carro de compras, con un `order_id`. Esta `order_id` permite al cliente y a la empresa realizar un seguimiento del progreso de ese pedido específico. Como el id de pedido es único, suele ser el `Primary Key` de un `orders` tabla.

A `Foreign Key` es una columna creada dentro de una tabla que está vinculada a la variable `Primary Key` de otra tabla. Las claves externas crean referencias entre tablas, lo que permite a los analistas buscar y vincular registros fácilmente. Digamos que queríamos saber qué pedidos pertenecían a cada uno de nuestros clientes. La variable `customer id` columna (`Primary Key` del `customers` ) y `order_id` columna (`Foreign Key` en el `customers` tabla, que hace referencia a la variable `Primary Key` del `orders` ) nos permite vincular y analizar esta información. Al crear una ruta, se le pedirá que defina ambas opciones de `Primary Key` y `Foreign Key`.

## Creación de una ruta {#createpath}

Al crear una columna en el almacén de datos, debe definir la ruta que lleva la información de una tabla a otra. A veces, las rutas se rellenan previamente porque ya existe una ruta entre tablas, pero si no ocurre esto, tendrá que crear una.

Utilizamos la relación entre **clientes** y **pedidos** para mostrarle cómo se hace. Desglosado:

* La relación es `one-to-many` : un cliente puede tener muchos pedidos, pero un pedido solo puede tener un cliente. Esto nos indica la dirección de la relación o dónde se debe crear la columna calculada. En este caso, significa información del `orders` puede introducirse en la variable `customers` tabla.
* La variable `primary key` queremos usar es `customers.customerid`o `customer ID` en la columna `customers` tabla.
* La variable `foreign key` queremos usar es `orders.customerid`o `customer ID` en la columna `orders` tabla.

Ahora, los guiamos a través de la creación del camino.

1. Haga clic en **[!UICONTROL Data > Data Warehouse]**.
1. En la lista de la tabla, haga clic en la tabla en la que desea crear la columna. En nuestro ejemplo, es el `customers` tabla.
1. Se mostrará el esquema de tabla. Haga clic en **[!UICONTROL Create New Column]**.
1. Asigne un nombre a la columna (por ejemplo, `Customer's orders`.
1. Seleccione la definición de la columna. Consulte la [Guía de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) para una útil hoja de trucos.
1. En el [!UICONTROL Select table and column] menú desplegable, haga clic en la **[!UICONTROL Create new path]** .

   ![Creación de rutas para el modal de columnas calculadas](../../assets/Creating_Paths_modal.png)

1. Con los menús desplegables, seleccione las claves principal y externa de cada tabla.

   En el `Many` lado, seleccionamos `orders.customerid` - recuerde, los clientes pueden tener muchos pedidos.

   En el `One` lado, seleccionamos `customers.customerid` - un pedido solo puede tener un cliente.

1. Haga clic en **[!UICONTROL Save]** para guardar la ruta y terminar de crear la columna.

### Limitaciones de la creación de rutas {#limits}

* **[!DNL MBI]no puede adivinar las relaciones de clave principal/externa**. No queremos introducir datos incorrectos en su cuenta, por lo que la creación de rutas debe realizarse manualmente.
* **Actualmente, las rutas solo se pueden especificar entre dos tablas diferentes**. ¿La lógica que intenta recrear implica más de dos tablas? Luego podría tener sentido (1) unir las columnas a una tabla intermediaria primero, luego a la tabla de &quot;destino final&quot;, o (2) consultar con nuestro equipo para encontrar el mejor enfoque para sus objetivos.
* **Una columna solo puede ser la referencia de clave externa para una ruta de acceso única a la vez**. Por ejemplo, si `order_items.order_id` señala a `orders.id`, luego `order_items.order_id` no puede señalar nada más.
* **`Many-to-many`técnicamente, se pueden crear rutas, pero muy a menudo producirán datos incorrectos porque ninguno de los lados es un verdadero `one-to-many` clave externa**. La mejor manera de enfocar estas rutas siempre depende del análisis deseado específico. Consulte al equipo de analistas RJ para descubrir la mejor solución.

Si no puede crear una columna calculada debido a una o varias de las limitaciones anteriores, póngase en contacto con el servicio de asistencia técnica con una descripción de la columna que está utilizando

## Eliminar una ruta de columna calculada {#delete}

¿Se ha creado una ruta incorrecta en la Data Warehouse? ¿O tal vez estás haciendo una pequeña limpieza de primavera y quieres arreglar? Si necesita eliminar una ruta de su cuenta, puede [enviar un ticket a nuestros analistas de soporte](../../guide-overview.md). **Asegúrese de incluir el nombre de la ruta.**

## Ajuste {#wrapup}

Ahora debería sentirse cómodo creando rutas para las columnas calculadas en su Data Warehouse. Si sigue sin estar seguro de una ruta determinada, recuerde que siempre puede hacer clic en **[!UICONTROL Support]** en su [!DNL MBI] para obtener ayuda.

## Relacionado

* [Explicación y evaluación de las relaciones de tabla](../data-warehouse-mgr/table-relationships.md)
* [Creación de rutas para columnas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) intentando crear.
