---
title: Crear y usar una columna calculada de SQL
description: Descubra cómo se pueden crear columnas avanzadas en forma de columnas de cálculo SQL en la nueva arquitectura de Adobe Commerce Intelligence.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Crear una columna calculada SQL

Este tema describe el propósito y los usos del tipo de columna `Calculation`, que se puede agregar a las tablas mediante [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). A continuación se explica qué hacen los cálculos SQL, por qué se utilizan, el proceso para crear un cálculo SQL e incluye dos ejemplos.

**Explicación**

En el pasado, las columnas que se consideraban `advanced` solo las podía realizar un analista en el equipo de éxito del cliente aquí en [!DNL Adobe Commerce Intelligence]. Ahora todo el poder está en manos del usuario final y se pueden crear columnas avanzadas en forma de `SQL Calculation` columnas en la nueva arquitectura de [!DNL Commerce Intelligence].

El tipo de columna `Calculation`, ahora disponible como opción en el Administrador de Data Warehouse, es una misma operación de tabla que le permite transformar las columnas de una tabla mediante la lógica PostgreSQL. La documentación sobre las funciones y los operadores que se pueden usar en el tipo de columna `Calculation` se encuentra en el sitio web de PostgreSQL [aquí](https://www.postgresql.org/docs/9.6/functions.html).

Las diferentes columnas que se pueden crear con la columna `Calculation` son casi ilimitadas, pero la mayoría de las columnas se pueden crear con instrucciones IF-THEN y aritmética básica, que se utiliza en los ejemplos siguientes.

**Ejemplo 1: ¿Es el último pedido del cliente?**

La mayoría de las cuentas tienen una columna denominada `Is customer's last order?` en su tabla `orders` para realizar análisis sobre las tasas de compra repetidas y los clientes perdidos. Si su cuenta se encuentra en la nueva arquitectura, esta columna se crea usando una columna `Calculation` y se puede ver en la captura de pantalla siguiente:

![Definición de columna calculada SQL para identificar el último pedido del cliente](../../assets/Is_customer_s_last_order.png)

La columna `Is customer's last order?` utiliza las entradas `Customer's lifetime number of orders` y `Customer's order number` con los alias `A` y `B`, respectivamente.

Línea a línea, el significado de PostgreSQL es:

* caso: Esto inicia una serie de instrucciones If - Then
* cuando `A` es nulo o `B` es nulo, entonces nulo: si alguna de las entradas está vacía, la salida también debe estar vacía. Esto sirve para evitar errores de SQL
* cuando `A=B` entonces `Yes`: Si `Customer's lifetime number of orders` es igual a `Customer's order number` para esta fila, entonces se devuelve `Yes`. Por lo tanto, si un cliente ha realizado cuatro pedidos, la fila de su cuarto pedido devolverá `Yes` para `Is customer's last order?`
* else `No`: si no se cumple ninguna de las otras condiciones cuando se cumplen, devuelva `No`
* end: Esto finaliza las instrucciones If - Then

Los posibles valores que puede devolver esta columna (`NULL`, `Yes`, `No`) contienen caracteres que no son numéricos, por lo que el tipo de datos aquí es Cadena.

**Ejemplo 2: Valor total del artículo de pedido (cantidad * precio)**

A muchos clientes les gusta analizar los ingresos en el nivel de artículo, dividiéndolos por campos como `product name` o `category`. La mayoría de las bases de datos no proporcionan realmente los ingresos de un producto en un pedido; en su lugar, proporcionan la cantidad vendida en el pedido y el precio del artículo.

Para habilitar los análisis de ingresos de productos, la mayoría de las cuentas tienen una columna denominada `Order item total value (quantity * price)` en su tabla `Orders Items`. Si su cuenta se encuentra en la nueva arquitectura, esta columna también se crea usando una columna `Calculation` y se puede ver en la captura de pantalla siguiente:

![Definición de columna calculada SQL para el valor total del elemento de pedido](../../assets/Order_item_total_value.png)

En el esquema de Commerce, la columna `Order item total value (quantity * price)` utiliza las entradas `qty ordered` y `base price` con los alias `A` y `B` respectivamente.

Los valores devueltos por esta nueva columna se expresan en dólares y centavos, por lo que el tipo de datos correcto es `Decimal(10,2)`.

**Mecánica**

Se puede agregar una nueva columna `Calculation` a una tabla navegando a **[!DNL Manage Data > Data Warehouse]** como se muestra a continuación:

![Vista de tabla que muestra resultados de columnas calculadas](../../assets/blobid2.png)

Desde aquí puede crear una columna `Calculation` siguiendo los pasos a continuación:

1. Seleccione la tabla sobre la cual desea agregar la columna `Calculation`.
1. En la tabla correcta, haga clic en **[!UICONTROL Create New Column]** en la parte superior derecha de la pantalla.
1. En el menú desplegable `Select a definition`, seleccione `Same Table`.
1. Seleccione `Calculation` como `column definition equation`.
1. Introduzca el nombre de la columna.
1. Elija las `input` columnas de la tabla que se utilizan en la lógica de la nueva columna. Cada columna que agregue recibirá un alias de letra, por lo que la primera columna será `A`, la segunda será `B`, y así sucesivamente.
1. En la ventana, escriba la lógica PostgreSQL para la nueva columna utilizando los alias de letras de las entradas. El cálculo SQL debe limitarse a una sola definición de columna, incluida toda la lógica entre las instrucciones SELECT y FROM de una consulta SQL. Las palabras clave SQL que utilicen cualquiera de las letras de entrada deben estar en minúsculas. Por ejemplo, al usar la instrucción `CASE`, debe escribirse en minúsculas: `case`. El sistema supone que una `A` mayúscula hace referencia a una de las entradas.
1. Seleccione el tipo de datos adecuado.
   * `Integer` - Número entero
   * `Decimal(10,2)`: un número decimal con 10 dígitos totales, de los cuales 2 están a la derecha del separador decimal
   * `String`: cualquier tipo de texto o serie de caracteres que no utilicen números
   * Formato `Datetime` - `yyyy-MM-dd hh:mm:ss`

1. Haga clic en **[!UICONTROL test column]**. Esto genera una lista de cinco valores de prueba para cada una de las entradas y muestra el resultado de la lógica del paso 6 para cada conjunto de valores de prueba. Si alguna parte del SQL genera un error, se devuelve el mensaje de error correspondiente. Solo se pueden generar resultados de muestra si todas las columnas de entrada son campos nativos. Si alguna de las columnas de entrada es una columna calculada, debe validar los resultados agregando la columna a una métrica y visualizándola en Visual Report Builder

1. Cuando esté satisfecho con los resultados, haga clic en **[!UICONTROL Save]**. La columna habilita para su uso.
