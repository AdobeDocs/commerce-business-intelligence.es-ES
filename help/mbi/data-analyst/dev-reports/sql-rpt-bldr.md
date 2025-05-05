---
title: Uso del Report Builder SQL
description: Descubra los detalles de cómo utilizar el Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 0%

---

# Usando [!DNL SQL Report Builder]

>[!NOTE]
>
>Requiere [permisos de administración](../../administrator/user-management/user-management.md) para crear y editar gráficos SQL. `Standard` usuarios pueden reorganizar estos gráficos en los paneles y `Read-only` usuarios tienen la misma experiencia que tienen con los gráficos tradicionales. Además, `Read-only` usuarios no tienen acceso al texto de la consulta.

Vea el [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=es) para obtener más información.

[!DNL SQL], o Lenguaje de consulta estructurado, es un lenguaje de programación utilizado para comunicarse con bases de datos. En [!DNL Commerce Intelligence], [!DNL SQL] se usa para consultar o recuperar datos de su Data Warehouse. Observe los informes en su tablero; entre bastidores, cada uno de ellos funciona con una consulta [!DNL SQL].

Puede usar [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) para consultar directamente la Data Warehouse, ver los resultados y transformarlos en un gráfico. Puede empezar a crear un informe con [!DNL SQL Report Builder] haciendo clic en **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Vea el [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=es) para obtener más información.

El [!DNL SQL Report Builder] le permite consultar directamente su Data Warehouse, ver los resultados y transformarlos rápidamente en un gráfico. La mejor parte de usar [!DNL SQL] para generar informes es que no necesita esperar en ciclos de actualización para iterar en las columnas que cree. Si los resultados no son correctos, puede editar y volver a ejecutar rápidamente la consulta hasta que las cosas coincidan con sus expectativas.

Este tema lo guiará a través del uso de [!DNL SQL Report Builder]. Una vez que sepa cómo hacerlo, consulte el tutorial de [!DNL SQL] para visualizaciones o intente optimizar algunas de las consultas que ha escrito.

Se trata en este artículo:

1. [Escribir una consulta](#writing)

1. [Ejecución de la consulta y visualización de los resultados](#runquery)

1. [Creación de una visualización](#createviz)

1. [Guardado del informe](#save)

## Integraciones de [!DNL SQL Report Builder]

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) es la única integración que no está disponible para usarse con [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Esta funcionalidad está en desarrollo.

Para empezar a crear un informe de [!DNL SQL], haga clic en **[!UICONTROL Report Builder]** o **[!UICONTROL Add Report]** en la parte superior de cualquier panel. En la pantalla [!DNL Report Picker], haga clic en **[!UICONTROL SQL Report Builder]** para abrir el editor [!DNL SQL].

## Primeros pasos

Para editar un informe, haga clic en el icono de engranaje (![](../../assets/gear-icon.png)) en la esquina superior derecha de un gráfico basado en [!DNL SQL] y haga clic en **[!UICONTROL Edit]**.

## Escribir una consulta {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] consultas distinguen entre mayúsculas y minúsculas. Asegúrese de utilizar las mayúsculas y minúsculas correctas al escribir consultas o de que podría terminar con resultados o errores inesperados.

Siguiendo las [directrices para la optimización de consultas](../../best-practices/optimizing-your-sql-queries.md), escriba una consulta en el editor [!DNL SQL].

>[!IMPORTANT]
>
>**Métricas en [!DNL SQL] informes**: al insertar una métrica en un informe SQL, se usa `current definition` de la métrica.

Si la métrica se actualiza en el futuro, el informe SQL *no* reflejará los cambios. Debe editar manualmente el informe para que los cambios surtan efecto.

Con los botones de la parte superior de la barra lateral, puede alternar entre listas de tablas y métricas disponibles para usar en [!DNL SQL Report Builder]. Si no ve lo que está buscando en la lista, intente buscarlo mediante la barra de búsqueda situada en la parte superior de la barra lateral.

También puede usar la barra lateral del editor [!DNL SQL] para insertar métricas, tablas y columnas directamente en las consultas pasando el puntero sobre ellas y haciendo clic en **[!UICONTROL Insert]**:

![Insertando una tabla en el editor [!DNL SQL].](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>El Report Builder SQL admite cualquier [función SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST) o cualquier función que no mute datos, que sea compatible con PostgreSQL. Esto incluye, entre otros, AVG, COUNT, COUNT DISTINCT, MIN/MAX y SUM.

Además, se admite cualquier tipo `JOIN`, pero Adobe recomienda usar únicamente INNER JOIN, ya que es el menos costoso de los tipos `JOIN`.

## Ejecución de la consulta y visualización de los resultados {#runquery}

Cuando termine de escribir la consulta, haga clic en **[!UICONTROL Run Query]**. Los resultados se muestran en una tabla debajo del editor SQL:

![Ejecutando la consulta y viendo los resultados.](../../assets/SQL_Run_Query.gif)

Si falta algo en los resultados, puede editar la consulta y volver a ejecutarla hasta que esté satisfecho.

Es posible que a veces vea [mensajes debajo del editor con EXPLAIN en ellos](../../best-practices/optimizing-your-sql-queries.md). Si ve uno de estos, significa que la consulta no se ha ejecutado y necesita un poco de ajuste.

Una vez que haya terminado de editar la consulta, puede pasar a crear una visualización o guardar el trabajo en un panel.

## Creación de una visualización {#createviz}

Para crear una visualización con los resultados de la consulta, haga clic en la ficha **[!UICONTROL Chart]** en el panel `Results`. En esta pestaña, selecciona:

* El `Series` o la columna que desee medir, como **Artículos vendidos**.
* El `Category` o la columna que desee usar para segmentar los datos, como **origen de adquisición**.
* Los valores del eje X o `Labels`.

A continuación se muestra un breve resumen del aspecto del proceso de visualización:

![](../../assets/SQL_RB_viz_overview.gif)

Para obtener una explicación detallada de cómo crear una visualización, consulte el [tutorial Creación de visualizaciones a partir de consultas SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Guardado del informe {#save}

Para poder guardar el trabajo, debe asignar un nombre al informe. Recuerde seguir las [directrices de prácticas recomendadas de asignación de nombres](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} y elegir algo que indique claramente cuál es el informe.

Haga clic en **[!UICONTROL Save]** en la esquina superior derecha del editor [!DNL SQL] y seleccione el informe `Type` (`Chart` o `Table`). Para ajustar las cosas, seleccione el tablero donde guardar el informe y haga clic en **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analice sus datos

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) le permite consultar directamente su Data Warehouse, ver los resultados y transformarlos rápidamente en un informe. El uso de [!DNL SQL] también le permite [usar [!DNL SQL] funciones que no están disponibles](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) en los Report Builder `Visual` o `Cohort`, lo que le proporciona un mayor control sobre sus datos.

Las columnas calculadas creadas con [!DNL SQL] no dependen de los ciclos de actualización, lo que significa que puede iterar según le plazca y ver los resultados inmediatamente.

>[!NOTE]
>
>Esto solo se aplica a la estructura de la columna, no a la actualización de los datos. Los datos nuevos siguen dependiendo de ciclos de actualización completados correctamente.

| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
|---|---|
| Analistas intermedios/avanzados | Principiantes - necesita saber [!DNL SQL]. |
| El experto de [!DNL SQL] | Análisis sencillos: escribir una consulta puede ser más trabajo que usar simplemente [!UICONTROL Visual Report Builder]. |
| Creación de columnas calculadas de un solo uso | Compartir con otros: tenga en cuenta su audiencia: ¿comprenden [!DNL SQL]? Si no es así, es posible que se confundan por la forma en que se crea el informe. |
| Datos con relaciones de `one-to-many` |  |
| Prueba de una nueva columna o análisis |  |

#### Resultados de base de datos frente a editor SQL

La mayoría de las veces, las diferencias en los resultados pueden atribuirse a ciclos de actualización. Si [!DNL Commerce Intelligence] está replicando datos de la base de datos en la Data Warehouse, es posible que vea resultados diferentes incluso cuando utilice la misma consulta.

Los problemas de conexión también pueden provocar discrepancias. Vaya a la página `Connections` haciendo clic en **[!DNL Manage Data** > **Connections]** para desprotegerla. ¿Hay algún error en la integración de la base de datos en cuestión? Si es así, es posible que tenga que [volver a autenticar la integración](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es) para que las cosas se vuelvan a ejecutar.

Si todas las integraciones están conectadas correctamente y no se encuentra en medio de un ciclo de actualización, puede que haya algún otro problema.

#### ¿Eliminar un informe [!DNL SQL] también elimina las columnas subyacentes de mi Data Warehouse?

No, no se pierde ninguna columna de la Data Warehouse, independientemente de cómo se haya creado.

Las columnas creadas con `Data Warehouse Manager` no se ven afectadas si se elimina un informe o una consulta que las utilice.

Las columnas creadas con [!DNL SQL Report Builder] no se guardarán en la Data Warehouse.


#### `Report Builder` frente a `SQL Report Builder`

[!DNL SQL Report Builder] le proporciona más flexibilidad al crear y estructurar gráficos; por ejemplo, puede seleccionar los valores que deben mostrarse en los ejes `X` y `Y`. Para obtener más información sobre la creación de gráficos en [!DNL SQL Report Builder], consulte el tutorial [Creación de visualizaciones a partir de [!DNL SQL] consultas](../../tutorials/create-visuals-from-sql.md).

#### `Cohort Report Builder` {#cohortrb}

A diferencia de [!DNL Visual Report Builder], [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) está diseñado para un único propósito: analizar e identificar las tendencias de comportamiento de grupos de usuarios similares a lo largo del tiempo. El uso de [!DNL Cohort Report Builder] no requiere ningún conocimiento de [!DNL SQL], por lo que puede sumergirse directamente en él sin dudarlo si acaba de comenzar.

| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
|---|---|
| Analistas intermedios/avanzados | Principiantes: necesita cohortes que definan la práctica. |
| Identificación de tendencias de comportamiento a lo largo del tiempo | Análisis cualitativo: se puede [hacer](../dev-reports/create-qual-cohort-analysis.md), pero requiere asistencia de Adobe. |

## Reconstrucción de Consultas después del Ciclo de Actualización

No es necesario que reconstruya las consultas. Los informes creados con [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) se guardan como los creados en la versión tradicional `Report Builder`. El proceso de actualización de [!DNL SQL] gráficos es el mismo: una vez actualizados los datos, los valores de los gráficos se recalcularán y se volverán a mostrar.

>[!NOTE]
>
>Al eliminar un informe o una consulta [!DNL SQL], no se eliminan las columnas subyacentes de la Data Warehouse. No pierda ninguna columna, independientemente de cómo la haya creado.

* Las columnas creadas con el Administrador de Datas Warehouse no se ven afectadas si se elimina un informe o una consulta que las utilice.

* Las columnas creadas con el Report Builder SQL no se guardan en la Data Warehouse.

## Ajuste {#wrapup}

Si desea intentar algo un poco más difícil, ¿por qué no intentar escribir una consulta optimizada para la visualización? Consulte el [Tutorial sobre creación de visualizaciones a partir de [!DNL SQL] consultas](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} para empezar.
