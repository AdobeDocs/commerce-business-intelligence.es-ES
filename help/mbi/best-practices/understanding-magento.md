---
title: Comprenda su  [!DNL Commerce Intelligence] entorno
description: Aprenda a trabajar con su entorno  [!DNL Commerce Intelligence] y a mejorarlo.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Su entorno [!DNL Adobe Commerce Intelligence]

A medida que analiza los datos de comercio, tenga en cuenta estos factores y las ideas erróneas comunes. Si necesita ayuda para asegurarse de que está usando correctamente el esquema de Commerce, no dude en [ponerse en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

Muchas de las tablas contienen una columna denominada `entity\_id`. En cada tabla que contiene un `entity\_id`, esa columna se usa para identificar filas únicas.

Por ejemplo, cada fila de la tabla `sales\_order` es un orden único. La clave principal de esta tabla se llama `entity\_id`. Esta columna puede considerarse como `order\_id`. En una tabla independiente, `customer\_entity`, cada fila representa un cliente único. La clave principal de esta tabla también se denomina `entity\_id`, y se puede considerar como `customer\_id`.

En esas tablas, `sales\_order.entity\_id` no es igual a `customer\_entity.entity\_id`. Esto es válido para todos los conjuntos de tablas que contienen `entity\_id`: `table\_A.entity\_id` no es igual a `table\_B.entity\_id`.

## [!DNL Guest orders]

Si permite que los clientes hagan pedidos desde el sitio sin tener una cuenta (pedidos de invitado), esos clientes no se rellenarán como una fila en la tabla `customer\_entity`. Además, cada pedido realizado por un invitado tiene un valor `customer\_id` nulo en la tabla `sales\_order`.

Por lo tanto, si desea realizar un seguimiento del comportamiento de los invitados a lo largo del tiempo, todas las columnas de nivel de cliente deben calcularse en la tabla `sales\_order`, utilizando un identificador de cliente como `customer\_email`.

Si usa la tabla `sales\_order` como tabla de cliente, debe tener cuidado al crear métricas de nivel de cliente. Por ejemplo, considere una métrica de ingresos promedio por duración. Esta métrica se utiliza para identificar los ingresos promedio por duración en su base de clientes. Esto primero requiere una nueva columna que, para cada cliente, devuelva sus ingresos de duración. Luego debe promediar esta columna para obtener los ingresos promedio por vida útil de los clientes.

Si puede usar la tabla `customer\_entity`, cada fila es un solo cliente y cada cliente sólo existe en esa tabla una vez. Por lo tanto, cuando tenga la columna de ingresos por duración, todo lo que necesita es crear una métrica promedio. Sin embargo, si utiliza la tabla `sales\_order` como tabla de cliente, es posible que exista un cliente en varias filas. Después de configurar la columna de ingresos por duración, cada pedido (fila) realizado por un cliente determinado mostrará los ingresos por duración de ese cliente, pero solo desea incluir a ese cliente una vez en la métrica promedio general.

El truco aquí es que debe agregar un filtro a la métrica que garantice que solo incluya a cada cliente una vez. El Adobe le recomienda crear y utilizar un conjunto de filtros denominado **Clientes que contamos** que filtre por el número de pedido de **Cliente = 1** (entre otros filtros, es posible que necesite excluir a los clientes no deseados). Añadir este filtro garantiza que solo se incluya a cada cliente una vez en una métrica de nivel de cliente.

## Productos y categorías

Los productos pueden tener varias categorías y las categorías se pueden usar para más de un producto. Por lo tanto, al configurar análisis de nivel de categoría, debe tener cuidado de utilizar las definiciones correctas. ¿Desea la categoría de nivel superior? ¿Categoría de segundo nivel? ¿Qué sucede si el producto puede clasificarse en varias categorías de nivel superior?

Imagine un par de jeans que se clasifican en tres niveles de categoría diferentes, según se define en una implementación de Commerce: &quot;Clothing&quot; (nivel superior), &quot;Outerwear&quot; (nivel 2) y &quot;Pants&quot; (nivel 3). Quizás desee analizar el rendimiento de las categorías por número de unidades vendidas. La métrica que necesita para este análisis es _Artículos vendidos_, que se basa en la tabla `sales\_order\_item`. Por lo tanto, debe mover la información de nivel de categoría a la tabla de elementos. Cada fila de la tabla `sales\_order\_item` tiene un `product\_id` asociado, por lo que si conoce las categorías asociadas a un producto, puede llevar esa información a la tabla deseada.

Antes de mover datos, primero debe conocer las uniones y filtros adecuados para asegurarse de que obtiene la categoría correcta. Para algunos análisis, es posible que necesite conocer &quot;Pantalones&quot;, pero en otros análisis, &quot;Ropa&quot; puede ser más apropiado. Se trata de categorías distintas que se identifican por separado. Saber cómo se define cada nivel de categoría garantiza que puede atribuir ventas unitarias a la categoría adecuada para su análisis específico.

Ahora, imagine que también tiene una categoría de nivel superior `Our Favorites` en la página principal del sitio web. Tal vez haya implementado su tienda Commerce para incluir estos jeans tanto en la categoría `Clothing` como en la categoría `Our Favorites`. Si es así, este par de jeans tiene más de una categoría de nivel superior. En ese caso, no tiene sentido mover una sola categoría de nivel superior a la tabla `sales\_order\_item`, ya que hay varias opciones. Para tener en cuenta esto, el Adobe sugiere crear columnas sí/no que comprueben la existencia de categorías específicas. Por ejemplo, las columnas `Is product in Clothing category?` y `Is product in Our Favorites category?` le permiten comprobar si un producto se encuentra en esas categorías específicas.
