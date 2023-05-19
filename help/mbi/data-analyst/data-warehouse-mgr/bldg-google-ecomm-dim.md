---
title: Generar[!DNL Google ECommerce]dimensiones
description: Aprenda a crear dimensiones que vinculen los datos de comercio electrónico con los datos de pedidos y clientes.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Generar [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Requiere [Permisos de administración](../../administrator/user-management/user-management.md).

Ahora que ha terminado [conectar su[!DNL Google ECommerce] account](../../data-analyst/importing-data/integrations/google-ecommerce.md), ¿qué puede hacer con esos datos en [!DNL Commerce Intelligence]? En este tema se explica cómo crear dimensiones que vinculen los datos de comercio electrónico con los datos de pedidos y clientes.

Las dimensiones cubiertas le permiten crear análisis que [responda preguntas vitales sobre sus canales y campañas de marketing](../../data-analyst/analysis/most-value-source-channel.md). ¿Qué porcentaje de los ingresos proviene de cada fuente? ¿Cómo funciona el valor de duración de? [!DNL Facebook] los clientes adquiridos se comparan con los de [!DNL Google]?

## Requisitos previos e información general

Para crear las dimensiones en este tema, necesita un [!DNL Google ECommerce] tabla, un `orders` y una tabla `customers` tabla. Esas tablas deben ser [sincronizado con su Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes de poder crear las dimensiones. Las tablas sincronizadas se muestran en `Synced Tables` de la sección `Data Warehouse Manager`.

A continuación se muestra un vistazo rápido a la sincronización de tablas y columnas si necesita un repaso:

![](../../assets/Syncing_New_Columns.gif)

Después de crear una unión desde el `orders` a la tabla [!DNL Google eCommerce] , se crean las tres primeras dimensiones en la lista siguiente. A continuación, utilice esas dimensiones para crear tres dimensiones de usuario/cliente en la `customers` tabla. Para terminar, una esas columnas a la `orders` tabla.

Estas son las dimensiones que se tratan:

* **Tabla de pedidos**

* El pedido es [!DNL Google Analytics] origen
* El pedido es [!DNL Google Analytics] mediano
* El pedido es [!DNL Google Analytics]Una campaña
* El primer pedido del cliente [!DNL Google Analytics] origen
* El primer pedido del cliente [!DNL Google Analytics] mediano
* El primer pedido del cliente [!DNL Google Analytics] campaña

* **Tabla Customers**

* El primer pedido del cliente [!DNL Google Analytics] origen
* El primer pedido del cliente [!DNL Google Analytics] mediano
* El primer pedido del cliente [!DNL Google Analytics] campaña

## Creación de dimensiones

Para crear dimensiones, abra [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) haciendo clic en **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabla de pedidos, ronda 1

En este ejemplo se crea el **El pedido es [!DNL Google Analytics] Origen** dimensión.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en este caso, ). `orders`) que contiene la información de su pedido.
1. Clic **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna
1. Seleccionar `Joined Column` desde el [menú desplegable de definición](../data-warehouse-mgr/calc-column-types.md). Este ejemplo funciona con un [relación uno a uno](../data-warehouse-mgr/table-relationships.md), coincidiendo con el `eCommerce.transactionID` a exactamente una fila de la columna `orders` tabla.
1. A continuación, debe definir la ruta o cómo se conectan la tabla y la columna que se están utilizando. Haga clic en `Select a table and column` desplegable.
1. La ruta que necesita no está disponible, por lo que debe crear una nueva. Clic **[!UICONTROL Create new Path]**.
1. En la ventana que se muestra, configure las `Many` de lado a `orders.order\_id`, o la columna en la `orders` que contiene el ID de pedido.
1. En el `One` lado, encuentre el `Google ECommerce` tabla y, a continuación, establezca la columna en `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Clic **[!UICONTROL Save]** para crear la ruta.
1. Una vez añadida la ruta, haga clic en **[!UICONTROL Select table and column]** desplegable de nuevo.
1. Busque el `ECommerce` y haga clic en la tabla `Source` columna. Esto vincula los pedidos con la información de origen.
1. Una vez que vuelva al esquema de tabla, haga clic en **[!UICONTROL Save]** de nuevo para crear la dimensión.

A continuación se muestra un vistazo a todo el proceso:

![](../../assets/help_center.gif)

A continuación, intente crear **El pedido es [!DNL Google Analytics] mediano** y `campaign`. No hay muchos cambios en estas dimensiones, así que pruébelo. Pero si te quedas atascado, puedes revisar [al final de este artículo](#stuck) para ver qué es diferente.

### Tabla Customers {#customers}

En este ejemplo se crea el **El primer pedido del cliente [!DNL Google Analytics] origen** dimensión.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en este caso, ). `customers`) que contiene su información de cliente.
1. Clic **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna
1. Para este ejemplo, seleccione `is MAX` definición de desde el [menú desplegable de definición](../../data-analyst/data-warehouse-mgr/calc-column-types.md). El `is MIN` La definición también podría funcionar si se aplica a una columna de texto con un solo valor posible. La parte importante es garantizar que se establecen los filtros adecuados, cosa que hará más adelante.
1. Haga clic en **[!UICONTROL Select a table and column]** y seleccione la opción `orders` y luego la tabla `Order's [!DNL Google Analytics] source` columna.
1. Clic **[!UICONTROL Save]**.
1. Una vez que vuelva al esquema de tabla, haga clic en `Options` desplegable, entonces `Filters`.
1. Clic **[!UICONTROL Add Filter Set]** y luego seleccione la `Orders we count` set. Solo desea que se incluyan los pedidos incluidos en el conjunto de filtros que cuenta, por lo que es importante que se seleccione este conjunto de filtros.
1. Clic **[!UICONTROL Add Filter]**. Desea encontrar el primer pedido del cliente. [!DNL Google Analytics] fuente, por lo que debe añadir un filtro:

   _orders.Número de pedido del cliente = 1

   _
1. Clic **[!UICONTROL Save]** para crear la dimensión.

A continuación, intente crear **El primer pedido del cliente [!DNL Google Analytics] mediano** y `campaign`. No hay muchos cambios en estas dimensiones, así que pruébelo. Pero si te quedas atascado, puedes revisar [al final de este artículo](#stuck) para ver qué es diferente.

### Bonus: mesa de pedidos, ronda 2

Puede detenerse aquí si lo desea, pero esta sección permite un análisis más detallado al traer el **El primer pedido del cliente [!DNL Google Analytics] dimensiones** que creó en la [última sección](#customers) en el `orders` tabla. La creación de las dimensiones en esta sección le permite analizar todas las métricas creadas en su `orders` tabla - `Revenue`, `Number of orders`, `Distinct buyers`, etc.: uso de [!DNL Google Analytics] atributos del primer pedido de un cliente.

Este ejemplo se une al `Customer's first order's [!DNL Google Analytics] source` dimensión a `orders` tabla.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en este caso, ). `orders`) que contiene la información de su pedido.
1. Clic **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna
1. Seleccionar `Joined Column` en el menú desplegable de definición. Esto une las dimensiones de cliente que creó en la sección anterior a `orders` tabla.
1. Haga clic en **[!UICONTROL Select a table and column]** y, a continuación, seleccione la `customers` y la `Customer's first order's [!DNL Google Analytics] source` columna.
1. Si una ruta no se rellena automáticamente, seleccione la ruta que mejor conecte las tablas de clientes y pedidos.
1. Clic **[!UICONTROL Save]** para crear la dimensión.

A continuación se muestra un vistazo a todo el proceso:

![](../../assets/help_center2.gif)

Termine uniéndose a la `Customer's first order's` medio y `campaign` dimensiones a la `orders` tabla. Una las dimensiones y, si hay problemas, compruebe lo siguiente [al final del artículo](#stuck) si necesita ayuda.

### Ajuste

Ha terminado de crear las dimensiones, lo que significa que ahora puede crear análisis completos que hagan un seguimiento del rendimiento de los distintos canales y campañas. Recuerde que la variable **las nuevas columnas no estarán disponibles hasta que se complete la siguiente actualización**.

Algunas de las dimensiones más populares se tratan en este tema, pero el cielo es el límite - intente crear su propio o no dude en hacernos ping si desea ayuda con la exploración de otras opciones. 

### Notas adicionales

**`Orders`#1 de tabla**: Al crear el `Order's [!DNL Google Analytics]` medio y `campaign` dimensiones, la diferencia son las columnas seleccionadas en el paso 12. En este ejemplo, la columna era `Source`.

**`Customers`tabla**: Al crear el `Customer's first order's [!DNL Google Analytics]` medio y `campaign` dimensiones, la diferencia son las columnas seleccionadas en el paso 5. En este ejemplo, la columna era `Order's [!DNL Google Analytics]` origen.

**`Orders`#2 de tabla**: Al unirse a `Customer's first order's [!DNL Google Analytics]` medio y `campaign` columnas a la `orders` tabla, la diferencia son las columnas seleccionadas en el paso 5. En este ejemplo, la columna era `Customer's first order's [!DNL Google Analytics]` origen.
