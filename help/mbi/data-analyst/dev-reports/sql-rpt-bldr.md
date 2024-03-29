---
title: Uso del Report Builder SQL
description: Descubra los detalles de cómo utilizar el Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Uso de [!DNL SQL Report Builder]

>[!NOTE]
>
>Requiere [Permisos de administración](../../administrator/user-management/user-management.md) para crear y editar gráficos SQL. `Standard` los usuarios pueden reorganizar estos gráficos en paneles y `Read-only` Los usuarios de tienen la misma experiencia que tienen con los gráficos tradicionales. Además, `Read-only` Los usuarios de no tienen acceso al texto de la consulta.

Consulte la [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) para obtener más información.

[!DNL SQL], o Lenguaje de consulta estructurado, es un lenguaje de programación que se utiliza para comunicarse con bases de datos. Entrada [!DNL Commerce Intelligence], [!DNL SQL] se utiliza para consultar o recuperar datos de la Data Warehouse. Mire los informes en su tablero: entre bastidores, cada uno de ellos funciona con un [!DNL SQL] consulta.

Puede usar el complemento [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) para consultar directamente la Data Warehouse, ver los resultados y transformarlos en un gráfico. Puede empezar a crear un informe con las [!DNL SQL Report Builder] haciendo clic en **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Consulte la [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) para obtener más información.

El [!DNL SQL Report Builder] le permite consultar directamente la Data Warehouse, ver los resultados y transformarlos rápidamente en un gráfico. La mejor parte sobre el uso de [!DNL SQL] para generar informes, no es necesario esperar a que los ciclos de actualización iteren en las columnas que cree. Si los resultados no son correctos, puede editar y volver a ejecutar rápidamente la consulta hasta que las cosas coincidan con sus expectativas.

En este tema se explica el uso de la variable [!DNL SQL Report Builder]. Después de saber cómo llegar, echa un vistazo al [!DNL SQL] tutorial para visualizaciones o intente optimizar algunas de las consultas que ha escrito.

Se trata en este artículo:

1. [Escribir una consulta](#writing)

1. [Ejecución de la consulta y visualización de los resultados](#runquery)

1. [Creación de una visualización](#createviz)

1. [Guardado del informe](#save)

## [!DNL SQL Report Builder] Integraciones

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) es la única integración que no está disponible para su uso con [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Esta funcionalidad está en desarrollo.

Para empezar a crear un [!DNL SQL] informe, haga clic en **[!UICONTROL Report Builder]** o **[!UICONTROL Add Report]** en la parte superior de cualquier tablero. En el [!DNL Report Picker] , haga clic en **[!UICONTROL SQL Report Builder]** para abrir [!DNL SQL] editor.

## Primeros pasos

Para editar un informe, haga clic en el icono de engranaje (![](../../assets/gear-icon.png)) icono en la esquina superior derecha de una [!DNL SQL]y haga clic en **[!UICONTROL Edit]**.

## Escribir una consulta {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] Las consultas distinguen entre mayúsculas y minúsculas. Asegúrese de utilizar las mayúsculas y minúsculas correctas al escribir consultas o de que podría terminar con resultados o errores inesperados.

Siguiendo las [directrices para la optimización de consultas](../../best-practices/optimizing-your-sql-queries.md), escriba una consulta en [!DNL SQL] editor.

>[!IMPORTANT]
>
>**Métricas en [!DNL SQL] informes** : Al insertar una métrica en un informe SQL, la variable `current definition` de la métrica se utiliza.

Si la métrica se actualiza en el futuro, el informe SQL *no tiene* reflejar los cambios. Debe editar manualmente el informe para que los cambios surtan efecto.

Con los botones de la parte superior de la barra lateral, puede alternar entre listas de tablas y métricas disponibles para usar en [!DNL SQL Report Builder]. Si no ve lo que está buscando en la lista, intente buscarlo mediante la barra de búsqueda situada en la parte superior de la barra lateral.

También puede utilizar la barra lateral en la variable [!DNL SQL] editor para insertar métricas, tablas y columnas directamente en las consultas pasando el puntero sobre ellas y haciendo clic en **[!UICONTROL Insert]**:

![Inserción de una tabla en [!DNL SQL] editor.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Cualquiera [SELECT, función](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), o cualquier función que no mute datos, que sea compatible con PostgreSQL es compatible con el Report Builder SQL. Esto incluye, entre otros, AVG, COUNT, COUNT DISTINCT, MIN/MAX y SUM.

Además, cualquier `JOIN` es compatible, pero Adobe recomienda utilizar únicamente INNER JOIN, ya que es el menos costoso de los `JOIN` tipos.

## Ejecución de la consulta y visualización de los resultados {#runquery}

Cuando haya terminado de escribir la consulta, haga clic en **[!UICONTROL Run Query]**. Los resultados se muestran en una tabla debajo del editor SQL:

![Ejecución de la consulta y visualización de los resultados.](../../assets/SQL_Run_Query.gif)

Si falta algo en los resultados, puede editar la consulta y volver a ejecutarla hasta que esté satisfecho.

A veces puede ver [mensajes debajo del editor con EXPLAIN en ellos](../../best-practices/optimizing-your-sql-queries.md). Si ve uno de estos, significa que la consulta no se ha ejecutado y necesita un poco de ajuste.

Una vez que haya terminado de editar la consulta, puede pasar a crear una visualización o guardar el trabajo en un panel.

## Creación de una visualización {#createviz}

Para crear una visualización con los resultados de la consulta, haga clic en **[!UICONTROL Chart]** en la pestaña `Results` panel. En esta pestaña, selecciona:

* El `Series`o la columna que desee medir, como **Artículos vendidos**.
* El `Category`o la columna que desee utilizar para segmentar los datos, como **fuente de adquisición**.
* El `Labels`o valores del eje X.

A continuación se muestra un breve resumen del aspecto del proceso de visualización:

![](../../assets/SQL_RB_viz_overview.gif)

Para obtener una explicación detallada de cómo crear una visualización, consulte la [Tutorial sobre Creación de visualizaciones a partir de consultas SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Guardado del informe {#save}

Para poder guardar el trabajo, debe asignar un nombre al informe. Recuerde seguir las [directrices de prácticas recomendadas para la asignación de nombres](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} y elija algo que indique claramente cuál es el informe.

Clic **[!UICONTROL Save]** en la esquina superior derecha de la [!DNL SQL] editor y seleccione el informe `Type` (`Chart` o `Table`). Para ajustar las cosas, seleccione el tablero en el que desea guardar el informe y haga clic en **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analice sus datos

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) le permite consultar directamente la Data Warehouse, ver los resultados y transformarlos rápidamente en un informe. Uso de [!DNL SQL] también le permite [para utilizar [!DNL SQL] funciones que no están disponibles](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) en el `Visual` o `Cohort` Report Builder, lo que le proporciona un mayor control sobre los datos.

Columnas calculadas creadas mediante [!DNL SQL] no dependen de los ciclos de actualización, lo que significa que puede iterar en ellos como desee y ver los resultados inmediatamente.

>[!NOTE]
>
>Esto solo se aplica a la estructura de la columna, no a la actualización de los datos. Los datos nuevos siguen dependiendo de ciclos de actualización completados correctamente.

| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
|---|---|
| Analistas intermedios/avanzados | Principiantes - usted necesita saber [!DNL SQL]. |
| El [!DNL SQL] listo | Análisis sencillos: escribir una consulta puede ser más trabajo que simplemente usar el [!UICONTROL Visual Report Builder]. |
| Creación de columnas calculadas de un solo uso | Uso compartido con otros usuarios: tenga en cuenta su audiencia: ¿comprenden lo siguiente? [!DNL SQL]? Si no es así, es posible que se confundan por la forma en que se crea el informe. |
| Datos con `one-to-many` relaciones |  |
| Prueba de una nueva columna o análisis |  |

#### Resultados de base de datos frente a editor SQL

La mayoría de las veces, las diferencias en los resultados pueden atribuirse a ciclos de actualización. If [!DNL Commerce Intelligence] está replicando datos de la base de datos en la Data Warehouse, puede que vea resultados diferentes incluso cuando utilice la misma consulta.

Los problemas de conexión también pueden provocar discrepancias. Vaya a `Connections` haciendo clic en **[!DNL Manage Data** > **Connections]** para comprobarlo: ¿hay un error para la integración de la base de datos en cuestión? Si es así, es posible que tenga que [volver a autenticar la integración](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) para poner las cosas en marcha de nuevo.

Si todas las integraciones están conectadas correctamente y no se encuentra en medio de un ciclo de actualización, puede que haya algún otro problema.

#### ¿Eliminar un [!DNL SQL] informe ¿también se eliminan las columnas subyacentes de mi Data Warehouse?

No, no se pierde ninguna columna de la Data Warehouse, independientemente de cómo se haya creado.

Columnas creadas con `Data Warehouse Manager` no se ven afectados si elimina un informe o una consulta que los utiliza.

Columnas creadas con [!DNL SQL Report Builder] no se han guardado en su Data Warehouse.


#### `Report Builder` frente `SQL Report Builder`

El [!DNL SQL Report Builder] le proporciona más flexibilidad a la hora de crear y estructurar gráficos; por ejemplo, puede seleccionar qué valores deben mostrarse en la `X` y `Y` ejes. Para obtener más información sobre la creación de gráficos en [!DNL SQL Report Builder], consulte la [Creación de visualizaciones desde [!DNL SQL] consultas](../../tutorials/create-visuals-from-sql.md) tutorial.

#### `Cohort Report Builder` {#cohortrb}

A diferencia del [!DNL Visual Report Builder], el [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) está pensado para un único propósito: analizar e identificar las tendencias de comportamiento de grupos de usuarios similares a lo largo del tiempo. Uso del [!DNL Cohort Report Builder] no requiere ningún [!DNL SQL] inteligente, para que puedas sumergirte sin dudarlo si apenas estás empezando.

| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
|---|---|
| Analistas intermedios/avanzados | Principiantes: necesita cohortes que definan la práctica. |
| Identificación de tendencias de comportamiento a lo largo del tiempo | Análisis cualitativo: puede ser [terminado](../dev-reports/create-qual-cohort-analysis.md), pero requiere asistencia de Adobe. |

## Reconstrucción de Consultas después del Ciclo de Actualización

No es necesario que reconstruya las consultas. Informes creados con [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) se guardan como los creados en la versión tradicional `Report Builder`. El proceso de actualización para [!DNL SQL] los gráficos son los mismos: una vez actualizados los datos, los valores de los gráficos se vuelven a calcular y mostrar.

>[!NOTE]
>
>Al eliminar un [!DNL SQL] informe/consulta, no elimina las columnas subyacentes de la Data Warehouse. No pierda ninguna columna, independientemente de cómo la haya creado.

* Las columnas creadas con el Administrador de Datas Warehouse no se ven afectadas si se elimina un informe o una consulta que las utilice.

* Las columnas creadas con el Report Builder SQL no se guardan en la Data Warehouse.

## Ajuste {#wrapup}

Si desea intentar algo un poco más difícil, ¿por qué no intentar escribir una consulta optimizada para la visualización? Consulte la [Creación de visualizaciones desde [!DNL SQL] tutorial de consultas](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} para empezar.
