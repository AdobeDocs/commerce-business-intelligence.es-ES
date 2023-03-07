---
title: Crear y usar una columna calculada de SQL
description: Descubra cómo se pueden crear columnas avanzadas en forma de columnas de cálculo SQL en la nueva arquitectura de MBI.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 0%

---

# Crear una columna calculada SQL

En este tema se describen el propósito y los usos del `Calculation` tipo de columna: que se puede añadir a las tablas utilizando la variable [Administrador de Datas Warehouse](../data-warehouse-mgr/tour-dwm.md). A continuación se explica qué hacen los cálculos SQL, por qué se utilizan, el proceso para crear un cálculo SQL y dos ejemplos.

**Explicación**

En el pasado, las columnas que se consideraban `advanced` solo lo ha podido realizar un analista del equipo de éxito del cliente aquí en [!DNL MBI]. Ahora todo el poder está en manos del usuario final, y se pueden crear columnas avanzadas en forma de `SQL Calculation` columnas en la nueva [!DNL MBI] arquitectura.

El `Calculation` El tipo de columna, ahora disponible como opción en el Administrador de Datas Warehouse, es una misma operación de tabla que le permite transformar las columnas de una tabla mediante la lógica PostgreSQL. Documentación sobre las funciones y operadores que se pueden utilizar en la `Calculatio`No se puede encontrar ningún tipo de columna en el sitio web PostgreSQL [aquí](https://www.postgresql.org/docs/9.6/functions.html).

Las diferentes columnas que se pueden crear con la variable `Calculation` Las columnas son casi ilimitadas, pero la mayoría de las columnas se pueden crear con instrucciones IF-THEN y aritmética básica, que se utiliza en los ejemplos siguientes.

**Ejemplo 1: ¿Es el último pedido del cliente?**

La mayoría de las cuentas tienen una columna denominada `Is customer's last order?` en su `orders` tabla para realizar análisis de tasas de compra repetidas y clientes perdidos. Si la cuenta se encuentra en la nueva arquitectura, esta columna se crea mediante una `Calculation` y se puede ver en la captura de pantalla siguiente:

![](../../assets/Is_customer_s_last_order.png)

El `Is customer's last order?` utiliza las entradas `Customer's lifetime number of orders` y `Customer's order number` con alias como `A` y `B` respectivamente.

Línea a línea, el significado de PostgreSQL es:

* caso: Esto inicia una serie de instrucciones If - Then
* cuando `A` es nulo o `B` es nulo y luego nulo: si alguna de las entradas está vacía, la salida también debe estar vacía. Esto sirve para evitar errores de SQL
* cuando `A=B` entonces `Yes`: Si `Customer's lifetime number of orders` igual a `Customer's order number` para esta fila y vuelva `Yes`. Por lo tanto, si un cliente ha realizado cuatro pedidos, se devolverá la fila del cuarto `Yes` para `Is customer's last order?`
* else `No`: Si no se cumple ninguna de las otras condiciones cuando, devuelva `No`
* end: Esto finaliza las instrucciones If - Then

Los posibles valores que puede devolver esta columna (`NULL`, `Yes`, `No`) contiene caracteres que no son numéricos, por lo que el tipo de datos aquí es Cadena.

**Ejemplo 2: Valor total del artículo del pedido (cantidad * precio)**

A muchos clientes les gusta analizar los ingresos en el nivel de artículo, dividiéndolos por campos como `product name` o `category`. La mayoría de las bases de datos no proporcionan realmente los ingresos de un producto en un pedido; en su lugar, proporcionan la cantidad vendida en el pedido y el precio del artículo.

Para habilitar los análisis de ingresos de productos, la mayoría de las cuentas tienen una columna denominada `Order item total value (quantity * price)` en su `Orders Items` tabla. Si la cuenta se encuentra en la nueva arquitectura, esta columna también se crea mediante una `Calculation` y se puede ver en la siguiente captura de pantalla:

![](../../assets/Order_item_total_value.png)

En el esquema de Commerce, la variable `Order item total value (quantity * price)` utiliza las entradas `qty ordered` y `base price` con alias como `A` y `B` respectivamente.

Los valores que devuelve esta nueva columna se expresan en dólares y céntimos, por lo que el tipo de datos correcto es `Decimal(10,2)`.

**Mecánica**

Un nuevo `Calculation` se puede agregar a una tabla navegando hasta **[!DNL Manage Data > Data Warehouse]** como se muestra a continuación:

![](../../assets/blobid2.png)

Desde aquí puede crear una `Calculation` siguiendo estos pasos:

1. Seleccione la tabla sobre la que desea agregar el `Calculation` columna.
1. En la tabla correcta, haga clic en **[!UICONTROL Create New Column]** en la parte superior derecha de la pantalla.
1. Desde el `Select a definition` menú desplegable, seleccione `Same Table`.
1. Seleccionar `Calculation` como el `column definition equation`.
1. Introduzca el nombre de la columna.
1. Elija la `input` columnas de la tabla que se utilizan en la lógica de la nueva columna. Cada columna que agregue recibirá un alias de letra, por lo que la primera columna será `A`, el segundo es `B` y demás.
1. En la ventana, escriba la lógica PostgreSQL para la nueva columna utilizando los alias de letras de las entradas. El cálculo SQL debe limitarse a una sola definición de columna, incluida toda la lógica entre las instrucciones SELECT y FROM de una consulta SQL. Las palabras clave SQL que utilicen cualquiera de las letras de entrada deben estar en minúsculas. Por ejemplo, al usar la variable `CASE` declaración, debe escribirse en minúsculas - `case`. El sistema supone que una `A` hace referencia a una de las entradas.
1. Seleccione el tipo de datos adecuado.
   * `Integer` - Número entero
   * `Decimal(10,2)` - un número decimal con 10 dígitos totales, de los cuales 2 están a la derecha del separador decimal
   * `String` - Cualquier tipo de texto o serie de caracteres que no utilicen números
   * `Datetime` - dd/MM/yyyy hh:mm:formato ss

1. Clic **[!UICONTROL test column]**. Esto genera una lista de cinco valores de prueba para cada una de las entradas y muestra el resultado de la lógica del paso 6 para cada conjunto de valores de prueba. Si alguna parte del SQL genera un error, se devuelve el mensaje de error correspondiente. Solo se pueden generar resultados de muestra si todas las columnas de entrada son campos nativos. Si alguna de las columnas de entrada es una columna calculada, debe validar los resultados agregando la columna a una métrica y visualizándola en el Report Builder visual
1. Cuando esté satisfecho con los resultados, haga clic en **[!UICONTROL Save]**. La columna habilita para su uso.
