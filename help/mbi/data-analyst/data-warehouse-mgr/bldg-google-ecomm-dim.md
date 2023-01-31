---
title: Generar[!DNL Google ECommerce]dimensiones
description: Aprenda a crear dimensiones que vinculen sus datos de comercio electrónico con sus pedidos y los datos de los clientes.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Generar [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Requiere [Permisos de administrador](../../administrator/user-management/user-management.md).

Ahora ha terminado [conectando su[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), ¿qué puede hacer con esos datos en [!DNL MBI]? En este artículo, le explicamos cómo crear dimensiones que vinculen sus datos de comercio electrónico con sus pedidos y los datos de los clientes.

Las dimensiones que cubrimos le darán la capacidad de crear análisis que [responder preguntas vitales sobre sus canales y campañas de marketing](../../data-analyst/analysis/most-value-source-channel.md). ¿Qué porcentaje de ingresos proviene de cada fuente? ¿En qué se diferencia el valor de duración de los clientes adquiridos por Facebook de los de [!DNL Google]?

## Requisitos previos e información general

Para crear las dimensiones en este artículo, necesita un [!DNL Google ECommerce] tabla, una `orders` y una `customers` tabla. Esas mesas tienen que ser [sincronizados con el almacén de datos](../../data-analyst/data-warehouse-mgr/tour-dwm.md) antes de crear dimensiones. Las tablas sincronizadas se muestran en la `Synced Tables` de la sección `Data Warehouse Manager`.

A continuación, se muestra un breve vistazo a la sincronización de tablas y columnas si necesita actualizarlas:

![](../../assets/Syncing_New_Columns.gif)

Después de crear un vínculo desde el `orders` a [!DNL Google eCommerce] , creamos las tres primeras dimensiones en la lista siguiente. A continuación, utilizamos esas dimensiones para crear tres dimensiones de usuario/cliente en la variable `customers` tabla. Para terminar, unimos esas columnas al `orders` tabla.

Estas son las dimensiones que cubrimos:

* **Tabla de pedidos**

* del pedido [!DNL Google Analytics] source
* del pedido [!DNL Google Analytics] medium
* del pedido [!DNL Google Analytics]Una campaña
* del primer pedido del cliente [!DNL Google Analytics] source
* del primer pedido del cliente [!DNL Google Analytics] medium
* del primer pedido del cliente [!DNL Google Analytics] campaign

* **Tabla de clientes**

* del primer pedido del cliente [!DNL Google Analytics] source
* del primer pedido del cliente [!DNL Google Analytics] medium
* del primer pedido del cliente [!DNL Google Analytics] campaign

## Creación de las dimensiones

Para crear dimensiones, abra el [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md) haciendo clic en **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabla de pedidos, ronda 1

En este ejemplo, creamos la variable **del pedido [!DNL Google Analytics] Fuente** dimensión.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en nuestro caso, `orders`) que contiene su información de pedido.
1. Haga clic en **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna .
1. Select `Joined Column` de la variable [lista desplegable de definición](../data-warehouse-mgr/calc-column-types.md). En este ejemplo, estamos trabajando con un [relación uno a uno](../data-warehouse-mgr/table-relationships.md), coincidiendo con la variable `eCommerce.transactionID` exactamente en una fila del `orders` tabla.
1. A continuación, es necesario definir la ruta o cómo están conectadas la tabla y la columna utilizadas. Haga clic en el `Select a table and column` lista desplegable.
1. El camino que necesitamos no está disponible, por lo que necesitamos crear uno nuevo. Haga clic en **[!UICONTROL Create new Path]**.
1. En la ventana que aparece, configure la variable `Many` lado a `orders.order\_id`o la columna de la `orders` tabla que contiene el ID de pedido.
1. En el `One` del lado, busque el `Google ECommerce` tabla, luego establezca la columna en `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Haga clic en **[!UICONTROL Save]** para crear la ruta.
1. Una vez añadida la ruta, haga clic en el botón **[!UICONTROL Select table and column]** de nuevo.
1. Busque la variable `ECommerce` y, a continuación, haga clic en la `Source` para abrir el Navegador. Esto vincula los pedidos con la información de origen.
1. Una vez que vuelva al esquema de tabla, haga clic en **[!UICONTROL Save]** para crear la dimensión.

A continuación se muestra un vistazo a todo el proceso:

![](../../assets/help_center.gif)

A continuación, intente crear **del pedido [!DNL Google Analytics] medium** y `campaign`. No hay mucho que cambie para estas dimensiones, así que hágalo un intento. Pero si te atascas, puedes echar un vistazo [el final de este artículo](#stuck) para ver qué es diferente.

### Tabla de clientes {#customers}

En este ejemplo, creamos la variable **del primer pedido del cliente [!DNL Google Analytics] source** dimensión.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en nuestro caso, `customers`) que contiene la información del cliente.
1. Haga clic en **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna .
1. Para este ejemplo, seleccionamos la variable `is MAX` definición de [lista desplegable de definición](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La variable `is MIN` la definición también podría funcionar si se aplica a una columna de texto con un solo valor posible. La parte importante es garantizar que se establezcan los filtros adecuados, lo que hacemos más adelante.
1. Haga clic en el **[!UICONTROL Select a table and column]** lista desplegable y seleccione la `orders` y luego la variable `Order's [!DNL Google Analytics] source` para abrir el Navegador.
1. Haga clic en **[!UICONTROL Save]**.
1. Una vez que vuelva al esquema de tabla, haga clic en el `Options` lista desplegable, `Filters`.
1. Haga clic en **[!UICONTROL Add Filter Set]** y, a continuación, seleccione `Orders we count` configurado. Solo queremos que se incluyan los pedidos incluidos en el filtro de pedidos que contamos, por lo que es importante que este conjunto de filtros esté seleccionado.
1. Haga clic en **[!UICONTROL Add Filter]**. Queremos encontrar el pedido inicial del cliente [!DNL Google Analytics] , por lo que necesitamos añadir un filtro:

   _orders.Número de pedido del cliente = 1

   _
1. Haga clic en **[!UICONTROL Save]** para crear la dimensión.

A continuación, intente crear **del primer pedido del cliente [!DNL Google Analytics] medium** y `campaign`. No hay mucho que cambie para estas dimensiones, así que hágalo un intento. Pero si te atascas, puedes echar un vistazo [el final de este artículo](#stuck) para ver qué es diferente.

### Bonos: Tabla de pedidos, ronda 2

Puede detener aquí si lo desea, pero esta sección permite un análisis más profundo al traer la variable **del primer pedido del cliente [!DNL Google Analytics] dimensiones** hemos creado en el [última sección](#customers) en el `orders` tabla. La creación de las dimensiones en esta sección le permite analizar todas las métricas creadas en su `orders` tabla - `Revenue`, `Number of orders`, `Distinct buyers`y así sucesivamente, usando la variable [!DNL Google Analytics] atributos del primer pedido de un cliente.

En este ejemplo, nos unimos al `Customer's first order's [!DNL Google Analytics] source` a la dimensión `orders` tabla.

1. En la lista de tablas de la Data Warehouse, haga clic en la tabla (en nuestro caso, `orders`) que contiene su información de pedido.
1. Haga clic en **[!UICONTROL Create a Column]**.
1. Asigne un nombre a la columna .
1. Select `Joined Column` en el menú desplegable de definición. Esto unirá las dimensiones de cliente que ha creado en la sección anterior al `orders` tabla.
1. Haga clic en el **[!UICONTROL Select a table and column]** lista desplegable y, a continuación, seleccione la `customers` y `Customer's first order's [!DNL Google Analytics] source` para abrir el Navegador.
1. Si una ruta no se rellena automáticamente, seleccione la ruta que mejor conecta las tablas de clientes y pedidos.
1. Haga clic en **[!UICONTROL Save]** para crear la dimensión.

A continuación se muestra un vistazo a todo el proceso:

![](../../assets/help_center2.gif)

Para terminar, una a la `Customer's first order's` medium y `campaign` dimensiones al `orders` tabla. Pruébelo, y como mencionamos antes, véyase [final del artículo](#stuck) si necesita ayuda.

### Ajuste

Terminamos de crear las dimensiones, lo que significa que ahora podemos crear análisis potentes que hagan un seguimiento del rendimiento de nuestros diversos canales y campañas. Sabemos que estás ansioso por empezar, pero recuerda el **las columnas nuevas no estarán disponibles hasta que se complete la siguiente actualización**.

Hemos cubierto algunas de las dimensiones más populares de este artículo, pero el cielo es el límite - intenta crear tu propio o siéntete libre de lanzarnos si quieres ayudar a explorar otras opciones. 

### ¡Estoy atascado! ¿qué es diferente? {#stuck}

**`Orders`tabla 1:** Al crear la variable `Order's [!DNL Google Analytics]` medium y `campaign` , la diferencia serán las columnas seleccionadas en el paso 12. En nuestro ejemplo, la columna era `Source`.

**`Customers`tabla:** Al crear la variable `Customer's first order's [!DNL Google Analytics]` medium y `campaign` , la diferencia serán las columnas seleccionadas en el paso 5. En nuestro ejemplo, la columna era `Order's [!DNL Google Analytics]` fuente.

**`Orders`tabla 2:** Al unirse a la `Customer's first order's [!DNL Google Analytics]` medium y `campaign` a `orders` , la diferencia serán las columnas seleccionadas en el paso 5. En nuestro ejemplo, la columna era `Customer's first order's [!DNL Google Analytics]` fuente.
