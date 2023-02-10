---
title: Comprenda su [!DNL MBI] Entorno
description: Obtenga información sobre cómo trabajar con y mejorar su [!DNL MBI] entorno.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# Su [!DNL MBI] Entorno

Al analizar los datos de comercio, tenga en cuenta estos factores y las ideas erróneas comunes. Si necesita ayuda para asegurarse de que está utilizando el esquema Commerce correctamente, no dude en [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## [!DNL entity\_id]

Muchas de las tablas contienen una columna denominada `entity\_id`. En cada tabla que contenga una `entity\_id`, esa columna se usa para identificar filas únicas.

Por ejemplo, cada fila de la `sales\_order` es un orden único. La clave principal de esta tabla se llama `entity\_id`. Esta columna puede considerarse como `order\_id`. En una tabla independiente, `customer\_entity`, cada fila representa un cliente único. La clave principal de esta tabla también se denomina `entity\_id`, que pueden considerarse como `customer\_id`.

En esas tablas, `sales\_order.entity\_id` no es igual a `customer\_entity.entity\_id`. Esto se aplica a todos los conjuntos de tablas que contienen `entity\_id`: `table\_A.entity\_id` no es igual a `table\_B.entity\_id`.

## [!DNL Guest orders]

Si permite que los clientes realicen un pedido desde su sitio sin tener una cuenta (pedidos de clientes), esos clientes no se rellenarán como una fila en su `customer\_entity` tabla. Además, cada pedido realizado por un invitado tendrá un valor nulo `customer\_id` en la variable `sales\_order` tabla.

Por lo tanto, si desea realizar un seguimiento de los comportamientos de los clientes a lo largo del tiempo, todas las columnas de nivel de cliente deben calcularse en la variable `sales\_order` mediante un identificador de cliente como `customer\_email`.

Si utiliza la variable `sales\_order` como tabla de cliente, debe tener cuidado al crear métricas a nivel de cliente. Por ejemplo, considere una métrica de ingresos promedio de por vida. Esta métrica se utiliza para identificar el ingreso promedio de duración en la base de clientes. La primera requiere una nueva columna que, para cada cliente, devuelva sus ingresos de por vida. A continuación, debe calcular el promedio de esta columna para obtener los ingresos promedio de por vida de sus clientes.

Si puede usar la variable `customer\_entity` , cada fila es un cliente único y cada cliente solo existe en esa tabla una vez. Por lo tanto, cuando tiene la columna de ingresos de por vida, todo lo que necesita es crear una métrica promedio. Sin embargo, si usa la variable `sales\_order` como tabla de cliente, un cliente puede existir potencialmente en numerosas filas. Después de configurar la columna de ingresos acumulados, cada pedido (fila) realizado por un cliente determinado mostrará los ingresos acumulados por el cliente; pero solo desea incluir a ese cliente una vez en la métrica promedio general.

El truco aquí es que debe agregar un filtro a la métrica que garantice que solo incluya a cada cliente una vez. Le recomendamos que cree y use un conjunto de filtros denominado **Clientes que contamos** que filtrará por **Número de pedido del cliente = 1** (entre otros filtros, es posible que necesite excluir clientes no deseados). Añadir este filtro garantiza que solo incluirá cada cliente una vez en una métrica de nivel de cliente.

## Productos y categorías

Los productos pueden tener varias categorías y las categorías se pueden usar para más de un producto. Por lo tanto, al configurar los análisis de nivel de categoría, debe tener cuidado de usar las definiciones correctas. ¿Desea la categoría de nivel superior? ¿Categoría de segundo nivel? ¿Qué sucede si el producto puede clasificarse en varias categorías de nivel superior?

Imagine un par de tejanos que se encuentre en tres niveles de categoría diferentes, según se definen en la implementación de Commerce: &#39;Ropa&#39; (nivel superior), &#39;Ropa externa&#39; (segundo nivel) y &#39;Pantalones&#39; (tercer nivel). Puede que desee analizar el rendimiento de sus categorías por número de unidades vendidas. La métrica que necesitará para este análisis es _Artículos vendidos_, que se basa en la variable `sales\_order\_item` tabla. Por lo tanto, debe mover la información de nivel de categoría a la tabla de elementos. Cada fila del `sales\_order\_item` tendrá asociada una tabla `product\_id`, por lo que si conoce las categorías asociadas con un producto, puede llevar esa información a la tabla deseada.

Antes de mover cualquier dato, primero debe conocer las uniones y filtros adecuados para asegurarse de obtener la categoría correcta. Para algunos análisis, es posible que necesite conocer &quot;Pantalones&quot;, pero en otros, &quot;Ropa&quot; puede ser más apropiado. Se trata de categorías distintas que se identifican por separado. Saber cómo se define cada nivel de categoría le asegurará de poder atribuir las ventas unitarias a la categoría adecuada para su análisis específico.

Ahora, imaginemos que también tiene una categoría de nivel superior &quot;Nuestros favoritos&quot; en la página principal de su sitio web. Tal vez haya implementado su tienda de comercio para incluir estos vaqueros tanto en la categoría &quot;Ropa&quot; como en la categoría &quot;Nuestros favoritos&quot;. Si es así, este par de tejanos tendrá más de una categoría de nivel superior. En ese caso, se mueve una sola categoría de nivel superior a la categoría `sales\_order\_item` no tiene sentido, ya que hay múltiples opciones. Para tener en cuenta esto, sugerimos crear columnas sí/no que comprueben categorías específicas. Por ejemplo, `Is product in Clothing category?` y `Is product in Our Favorites category?` , podrá comprobar si un producto se encuentra dentro de esas categorías específicas.
