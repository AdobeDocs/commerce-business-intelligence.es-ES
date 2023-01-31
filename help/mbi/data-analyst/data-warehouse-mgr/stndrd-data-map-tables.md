---
title: Estandarización de datos con tablas de asignación
description: Aprenda a trabajar con tablas de asignación.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Estandarización de datos con tablas de asignación

Imagine esto: está en el `Report Builder`, creando un `Revenue by State` informe. Estás en la zona. Todo va a ir a toda velocidad hasta que vaya a agregar un `billing state` agrupado en el informe y verá esto:

![](../../assets/Messy_State_Segments.png)

## ¿Cómo pudo pasar esto?

Desafortunadamente, la falta de estandarización a veces puede llevar a complicados datos y dolores de cabeza al crear informes. En nuestro ejemplo, es posible que no haya habido un menú desplegable o una forma estandarizada para que nuestros clientes introduzcan su información de estado de facturación. Esto da lugar a una variedad de valores: `pa`, `PA`, `penna`, `pennsylvania`y `Pennsylvania` - todo por el mismo estado, lo que ciertamente llevará a algunos resultados extraños en el `Report Builder`.

Es posible que haya un recurso técnico que pueda ayudarle a limpiar los datos o insertar las columnas que necesita directamente en la base de datos, pero si no, tenemos otra solución: **la tabla de asignación**. Una tabla de asignación le permite limpiar y estandarizar de forma rápida y sencilla cualquier dato confuso asignando datos a un único resultado.

>[!NOTE]
>
>No puede crear una tabla de asignación para tablas consolidadas sin la ayuda de nuestro equipo de asistencia. Póngase en contacto con nosotros para obtener más información.

## ¿Cómo puedo crearlo? {#how}

**Actualización de formato de datos:**

* Asegúrese de que la hoja de cálculo tenga una fila de encabezado.
* ¡Evite utilizar comas! Esto provocará problemas al cargar el archivo.
* Usar el formato de fecha estándar `(YYYY-MM-DD HH:MM:SS)` para fechas.
* Los porcentajes deben introducirse como decimales.
* Asegúrese de que los ceros a la izquierda o a la derecha se conserven correctamente.

Antes de sumergirse, le recomendamos que [exportar los datos de la tabla sin procesar](../../tutorials/export-raw-data.md). Al mirar los datos sin procesar primero, puede explorar todas las combinaciones posibles de los datos que necesita limpiar, lo que garantiza que la tabla de asignación abarque todo.

Para crear una tabla de asignación, debe crear una hoja de cálculo de dos columnas que siga a la [reglas de formato para cargas de archivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

En la primera columna, introduzca los valores almacenados en la base de datos con **solo un valor en cada fila**. Por ejemplo, `pa` y `PA` no puede estar en la misma línea: cada entrada debe tener su propia fila. Consulte a continuación un ejemplo.

En la segunda columna, introduzca estos valores. **debe**. Continuación con nuestro ejemplo de estado de facturación, si queremos `pa`, `PA`, `Pennsylvania`y `pennsylvania` para `PA`, entraremos `PA` en esta columna para cada valor de entrada.

![](../../assets/Mapping_table_examples.jpg)

## ¿Qué debo hacer en [!DNL MBI] para usarlo? {#use}

Cuando haya terminado de crear la tabla de asignación, deberá [cargar el archivo](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] y [crear una columna unida](../../data-analyst/data-warehouse-mgr/calc-column-types.md) que reubica el nuevo campo en la tabla deseada. Puede hacerlo después de sincronizar el archivo con el almacén de datos.

En nuestro ejemplo, moveremos la columna que creamos en el `mapping_state` tabla (`state_input`) a la variable `customer_address` empleando una columna unida. Esto nos permitirá agruparnos por lo limpio `state_input` en nuestros informes en lugar de en la `state` para abrir el Navegador.

Para crear la variable `joined` , vaya a la tabla a la que se reubicará el campo en el Administrador de Datas Warehouse. En nuestro ejemplo, esta sería la variable `customer_address` tabla.

1. Haga clic en **[!UICONTROL Create a Column]**.
1. Select `Joined Column` de la variable `Definition` lista desplegable.
1. Asigne un nombre a la columna que la diferencie de la columna `state` en la base de datos. Iremos con `billing state (mapped)` de modo que podemos saber qué columna utilizar al segmentar en el creador de informes.
1. La ruta que necesitamos para conectar las tablas no existe, por lo que necesitamos crear una nueva. Haga clic en **[!UICONTROL Create new path]**  en el `Select a table and column` lista desplegable.

   Si no está seguro de cuál es la relación de tabla o de cómo definir correctamente las claves principal y externa, desproteja [nuestro tutorial](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) para obtener ayuda.

   * En el `Many` del lado, seleccione la tabla a la que está reubicando el campo (de nuevo, para nosotros es `customer_address`) y `Foreign Key` o `state` , en nuestro ejemplo.
   * En el `One` en el lado, seleccione `mapping` y `Primary key` para abrir el Navegador. En este caso, seleccionaríamos la variable `state_input` de `mapping_state` tabla.
   * A continuación se muestra un vistazo a cómo se ve nuestro camino:

      ![](../../assets/State_Mapping_Path.png)

1. Cuando termine, haga clic en **[!UICONTROL Save]** para crear la ruta.
1. Es posible que la ruta no se rellene inmediatamente después de guardarla. Si esto sucede, haga clic en el botón `Path` y seleccione la ruta que acaba de crear.
1. Haga clic en **[!UICONTROL Save]** para crear la columna.

¡Eso es!

## ¿Qué hago ahora? {#wrapup}

Una vez finalizado el ciclo de actualización, podrá utilizar la nueva columna unida para segmentar correctamente los datos en lugar de la columna desordenada de la base de datos. Eche un vistazo a nuestras opciones de agrupación ahora - no más desorden de estrés:

![](../../assets/Clean_State_Segments.png)

Las tablas de asignación son útiles para cualquier momento en el que desee limpiar algunos datos potencialmente confusos en el almacén de datos. Sin embargo, las tablas de asignación también se pueden utilizar para otros casos de uso interesantes, como [replicación de los canales de Google Analytics en MBI](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Relacionado

* [Explicación y evaluación de las relaciones de tabla](../data-warehouse-mgr/table-relationships.md)
* [Creación/eliminación de rutas para columnas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
