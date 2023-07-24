---
title: Estandarización de datos con tablas de asignación
description: Aprenda a trabajar con tablas de asignación.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Estandarización de datos con tablas de asignación

Imagina que estás en el `Report Builder` creación de una `Revenue by State` informe. Todo va bien hasta que intente agregar una `billing state` en el informe y verá lo siguiente:

![](../../assets/Messy_State_Segments.png)

## ¿Cómo pudo pasar esto?

Desafortunadamente, la falta de estandarización a veces puede generar problemas de datos y dolores de cabeza al crear informes. En este ejemplo, es posible que no haya un menú desplegable o una forma estandarizada para que los clientes introduzcan la información de estado de facturación. Esto lleva a varios valores: `pa`, `PA`, `penna`, `pennsylvania`, y `Pennsylvania` - todos para el mismo estado, lo que conduce a algunos resultados extraños en el `Report Builder`.

Es posible que haya un recurso técnico que pueda ayudarle a limpiar los datos o a insertar las columnas que necesite directamente en la base de datos. Si no es así, hay otra solución: **la tabla de asignación**. Una tabla de asignación le permite limpiar y estandarizar rápida y fácilmente cualquier dato desordenado asignando datos a una sola salida.

>[!NOTE]
>
>No se puede crear una tabla de asignación para tablas consolidadas sin la ayuda del equipo de soporte técnico de Adobe.

## ¿Cómo se crea? {#how}

**Actualizador de formato de datos:**

* Asegúrese de que la hoja de cálculo tenga una fila de encabezado.
* Evite utilizar comas. Esto causa problemas al cargar el archivo.
* Utilizar el formato de fecha estándar `(YYYY-MM-DD HH:MM:SS)` para fechas.
* Los porcentajes deben introducirse como decimales.
* Asegúrese de que se retienen correctamente los ceros a la izquierda y a la derecha.

Antes de sumergirse, Adobe recomienda que [exportar los datos de tabla sin procesar](../../tutorials/export-raw-data.md). Mirar primero los datos sin procesar significa que puede explorar todas las combinaciones posibles de los datos que necesita limpiar, asegurándose así de que la tabla de asignación cubra todo.

Para crear una tabla de asignación, debe crear una hoja de cálculo de dos columnas que siga al [reglas de formato para cargas de archivos](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

En la primera columna, introduzca los valores almacenados en la base de datos con **solo un valor en cada fila**. Por ejemplo, `pa` y `PA` no puede estar en la misma línea: cada entrada debe tener su propia fila. Consulte a continuación un ejemplo.

En la segunda columna, introduzca los valores **debería ser**. Continuando con el ejemplo del estado de facturación, si lo desea `pa`, `PA`, `Pennsylvania`, y `pennsylvania` para ser simplemente `PA`, debe introducir `PA` en esta columna para cada valor de entrada.

![](../../assets/Mapping_table_examples.jpg)

## ¿Qué debo hacer en? [!DNL Commerce Intelligence] para usarlo? {#use}

Una vez que haya terminado de crear la tabla de asignación, debe [cargar el archivo](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) en [!DNL Commerce Intelligence] y [crear una columna combinada](../../data-analyst/data-warehouse-mgr/calc-column-types.md) que reubica el nuevo campo en la tabla deseada. Puede hacerlo después de sincronizar el archivo con la Data Warehouse.

En este ejemplo, se mueve la columna que ha creado en el `mapping_state` tabla (`state_input`) a la `customer_address` mediante una columna combinada. Esto nos permite agruparnos por lo limpio `state_input` en los informes en lugar de en la columna `state` columna.

Para crear el `joined` , vaya a la tabla a la que se reubicará el campo en el Administrador de Datas Warehouse. En este ejemplo, este sería el `customer_address` tabla.

1. Clic **[!UICONTROL Create a Column]**.
1. Seleccionar `Joined Column` desde el `Definition` desplegable.
1. Asigne un nombre a la columna que la diferencie del `state` en la base de datos. Asignar un nombre a la columna `billing state (mapped)` por lo tanto, puede saber qué columna utilizar al segmentar en report builder.
1. La ruta que necesita para conectar las tablas no existe, por lo que debe crear una. Clic **[!UICONTROL Create new path]**  en el `Select a table and column` desplegable.

   Si no está seguro de cuál es la relación de tabla o de cómo definir correctamente las claves principal y externa, desprotéjase [el tutorial](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) para obtener ayuda.

   * En el `Many` Seleccione la tabla a la que está reubicando el campo (de nuevo, para nosotros es `customer_address`) y el `Foreign Key` o bien `state` en el ejemplo.
   * En el `One` lado, seleccione el `mapping` y la `Primary key` columna. En este caso, debe seleccionar la variable `state_input` de la columna `mapping_state` tabla.
   * Este es un vistazo a la apariencia de la ruta:

     ![](../../assets/State_Mapping_Path.png)

1. Cuando termine, haga clic en **[!UICONTROL Save]** para crear la ruta.
1. Es posible que la ruta no se rellene inmediatamente después de guardar. Si esto sucede, haga clic en el `Path` y seleccione la ruta que ha creado.
1. Clic **[!UICONTROL Save]** para crear la columna.

## ¿Qué hago ahora? {#wrapup}

Una vez completado el ciclo de actualización, podrá utilizar la nueva columna combinada para segmentar correctamente los datos en lugar de la columna desordenada de la base de datos. Mira tus opciones de agrupación ahora - no más líos de estrés:

![](../../assets/Clean_State_Segments.png)

Las tablas de asignación son útiles para cualquier momento en el que desee limpiar algunos datos potencialmente desordenados en la Data Warehouse. Sin embargo, las tablas de asignación también se pueden utilizar para algunos otros casos de uso interesantes, como [replicación de su [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Relacionado

* [Explicación y evaluación de las relaciones de tabla](../data-warehouse-mgr/table-relationships.md)
* [Creación/eliminación de rutas para columnas calculadas](../data-warehouse-mgr/create-paths-calc-columns.md)
