---
title: Creación y uso de una columna calculada SQL
description: Descubra cómo se pueden crear columnas avanzadas en forma de columnas de cálculo SQL en la nueva arquitectura de MBI.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Crear una columna calculada SQL

Este tema describe el propósito y los usos del `Calculation` tipo de columna: que se pueden agregar a tablas utilizando la variable [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md). A continuación se explica qué hacen los cálculos SQL, por qué se utilizan, el proceso para crear un cálculo SQL y dos ejemplos.

**Explicación**

En el pasado, las columnas que se consideraban `advanced` solo puede hacerlo un analista del equipo de éxito del cliente aquí en [!DNL MBI]. Ahora toda la potencia está en manos del usuario final, y las columnas avanzadas se pueden crear en forma de `SQL Calculation` columnas de la nueva [!DNL MBI] arquitectura.

La variable `Calculation` el tipo de columna, ahora disponible como opción en el Administrador de Datas Warehouse, es la misma operación de tabla que permite transformar las columnas en una tabla mediante la lógica PostgreSQL. Documentación sobre las funciones y los operadores que se pueden usar en la variable `Calculatio`Se puede encontrar un tipo de columna en el sitio web PostgreSQL [here](https://www.postgresql.org/docs/9.6/static/functions.html).

Las diferentes columnas que se pueden crear con la variable `Calculation` son casi ilimitadas, pero la mayoría de las columnas se pueden crear utilizando instrucciones IF-THEN y aritmética básica, que se utilizarán en los ejemplos siguientes.

**Ejemplo 1: ¿Es el último pedido del cliente?**

La mayoría de las cuentas tienen una columna denominada `Is customer's last order?` en su `orders` para realizar análisis sobre tasas de compra repetidas y clientes rechazados. Si la cuenta se encuentra en la nueva arquitectura, esta columna se crea mediante una `Calculation` y se puede ver en la captura de pantalla siguiente:

![](../../assets/Is_customer_s_last_order.png)

La variable `Is customer's last order?` utiliza las entradas `Customer's lifetime number of orders` y `Customer's order number` con alias `A` y `B` respectivamente.

Línea por línea, el significado de PostgreSQL es:

* caso: Esto inicia una serie de instrucciones If - Then
* when `A` es nulo o `B` es nulo y luego nulo: Si alguna de las entradas está vacía, la salida también debería estar vacía. Esto es para evitar errores SQL
* when `A=B` then `Yes`: If `Customer's lifetime number of orders` es igual que `Customer's order number` para esta fila, devuelva `Yes`. Por lo tanto, si un cliente ha realizado 4 pedidos, la fila de su cuarto pedido devolverá `Yes` para `Is customer's last order?`
* else `No`: Si no se cumple ninguna de las otras cuando se cumplen las instrucciones, devuelva `No`
* final: Esto finaliza con las instrucciones If - Then

Los valores posibles que puede devolver esta columna (`NULL`, `Yes`, `No`) contiene caracteres que no son numéricos, por lo que el tipo de datos aquí es String.

**Ejemplo 2: Valor total del artículo de pedido (cantidad * precio)**

A muchos de nuestros clientes les gusta analizar los ingresos a nivel de artículo, dividiéndolos por campos como `product name` o `category`. La mayoría de las bases de datos no proporcionan realmente los ingresos de un producto en un pedido; en su lugar, proporcionan la cantidad vendida en el pedido, y el precio del artículo.

Para habilitar los análisis de ingresos de productos, la mayoría de las cuentas tienen una columna denominada `Order item total value (quantity * price)` en su `Orders Items` tabla. Si la cuenta se encuentra en la nueva arquitectura, esta columna también se crea mediante una `Calculation` y se puede ver en la captura de pantalla siguiente:

![](../../assets/Order_item_total_value.png)

En el esquema Commerce , la variable `Order item total value (quantity * price)` utiliza las entradas `qty ordered` y `base price` con alias `A` y `B` respectivamente.

Los valores que devuelva esta nueva columna serán dólares y centavos, por lo que el tipo de datos correcto es `Decimal(10,2)`.

**Mecánicos**

Un nuevo `Calculation` para agregar una columna a una tabla, vaya a **[!DNL Manage Data > Data Warehouse]** como se muestra a continuación:

![](../../assets/blobid2.png)

Desde aquí puede crear un `Calculation` siguiendo los pasos a continuación:

1. Seleccione la tabla a la que desea agregar la variable `Calculation` para abrir el Navegador.
1. En la tabla correcta, haga clic en **[!UICONTROL Create New Column]** en la parte superior derecha de la pantalla.
1. En el `Select a definition` menú desplegable, seleccione `Same Table`.
1. Select `Calculation` como el `column definition equation`.
1. Introduzca el nombre de la columna.
1. Elija la `input` columnas de la tabla que se utilizarán en la lógica de la nueva columna. Cada columna que agregue tendrá un alias de letra, por lo que la primera columna será `A`, el segundo será `B` y así sucesivamente.
1. En la ventana , escriba la lógica PostgreSQL para la nueva columna utilizando los alias de letras de las entradas. El cálculo SQL debe limitarse a una definición de columna única, incluida toda la lógica entre las instrucciones SELECT y FROM de una consulta SQL. Tenga en cuenta que las palabras clave SQL que utilizan cualquiera de las letras de entrada deben estar en minúsculas. Por ejemplo, al usar la variable `CASE` , debe escribirse en minúscula - `case`. El sistema supone que hay una mayúscula `A` hace referencia a una de las entradas.
1. Elija el tipo de datos adecuado.
   * `Integer` - Número entero
   * `Decimal(10,2)` - un número decimal con 10 dígitos totales, de los cuales 2 están a la derecha del punto decimal
   * `String` - Cualquier tipo de texto o serie de caracteres que no sean números
   * `Datetime` - yyyy-MM-dd hh:mm:formato ss

1. Haga clic en **[!UICONTROL test column]**. Esto generará una lista de 5 valores de prueba para cada una de las entradas y mostrará el resultado de la lógica del paso 6 para cada conjunto de valores de prueba. Si alguna parte del SQL genera un error, se devuelve el mensaje de error correspondiente. Tenga en cuenta que los resultados de la muestra solo se pueden generar si todas las columnas de entrada son campos nativos. Si alguna de las columnas de entrada son columnas calculadas, deberá validar los resultados añadiendo la columna a una métrica y visualizándola en el Report Builder visual
1. Cuando esté satisfecho con los resultados, haga clic en **[!UICONTROL Save]**, y la columna estará disponible para su uso.
