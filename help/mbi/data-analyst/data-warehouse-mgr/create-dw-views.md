---
title: Creación y uso de vistas de Data Warehouse
description: Obtenga información sobre un método para crear nuevas tablas almacenadas mediante la modificación de una tabla existente o la unión o consolidación de varias tablas mediante SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# Uso de vistas de Data Warehouse

Este documento describe el propósito y los usos de `Data Warehouse Views` accesible navegando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. A continuación se explica qué hace y cómo crear vistas, así como un ejemplo de cómo utilizar `Data Warehouse Views` para consolidar [!DNL Facebook] y [!DNL AdWords] gastar datos.

## Finalidad general

El `Data Warehouse Views` Esta función es un método para crear nuevas tablas almacenadas mediante la modificación de una tabla existente o la unión o consolidación de varias tablas mediante SQL. Una vez al `Data Warehouse View` se ha creado y procesado mediante un ciclo de actualización, se rellena en la Data Warehouse como una nueva tabla en el `Data Warehouse Views` , como se muestra a continuación:

![](../../assets/Data_Warehouse.png)

Desde aquí, la nueva vista funciona como cualquier otra tabla, lo que le permite crear nuevas columnas calculadas o crear métricas e informes sobre ella.

`Data Warehouse Views` se utilizan principalmente para consolidar varias tablas similares pero dispares, de modo que todos los informes se puedan crear en una sola tabla nueva. Algunos ejemplos comunes incluyen la consolidación de las tablas de una base de datos heredada y una base de datos activa para combinar datos históricos y actuales, o la combinación de varias fuentes de publicidad como Facebook y AdWords en un singular `Consolidated ad spend` tabla.

Si está familiarizado con SQL, ambos ejemplos de consolidación utilizan el `UNION` , pero puede utilizar cualquier sintaxis y función de PostgreSQL al crear una nueva vista.

## Creación y administración de vistas de Data Warehouse

Nuevo `Data Warehouse Views` se pueden crear y las vistas existentes se pueden eliminar navegando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, como se muestra a continuación:

![](../../assets/Data_Warehouse_Views.png)

Desde aquí puede crear una vista siguiendo las instrucciones de ejemplo siguientes:

1. Si observa una vista existente, haga clic en **[!UICONTROL New Data Warehouse View]** para abrir una ventana de consulta en blanco. Si ya está abierta una ventana de consulta en blanco, continúe con el paso siguiente.
1. Asigne un nombre a la vista escribiendo en `View Name` field. El nombre proporcionado aquí determina el nombre para mostrar de la vista en la Data Warehouse. `View names` se limitan a letras minúsculas, números y guiones bajos (_). Todos los demás caracteres están prohibidos.
1. Introduzca la consulta en la ventana titulada `Select Query`, usando la sintaxis estándar de PostgreSQL.

   >[!NOTE]
   >
   >La consulta debe hacer referencia a nombres de columna específicos. El uso del `*`no se permite seleccionar todas las columnas.

1. Cuando haya terminado, haga clic en **[!UICONTROL Save]** para guardar la vista. La vista tiene temporalmente un `Pending` estado hasta que se procese en el siguiente ciclo de actualización completo, momento en el que el estado cambia a `Active`. Después de ser procesada por una actualización, la vista está lista para utilizarse en los informes.

Es importante mencionar que, después de guardar, la consulta subyacente utilizada para generar una `Data Warehouse View` no se puede editar. Si necesita ajustar la estructura de un `Data Warehouse View`Además, debe crear una vista y migrar manualmente cualquier columna, métrica o informe calculado de la vista original a la nueva. Una vez completada la migración, puede eliminar con seguridad la vista original. Porque `Data Warehouse Views` no son editables, Adobe recomienda probar el resultado de la consulta utilizando `SQL Report Builder` antes de guardar la consulta como vista de Data Warehouse.

## Ejemplo: [!DNL Facebook] y [!DNL Google AdWords] datos

Examine con más detalle uno de los ejemplos mencionados anteriormente en este artículo: consolidación [!DNL Facebook] y [!DNL AdWords] gastar datos en una nueva tabla de anuncios consolidados. Normalmente, esto implica la consolidación de dos tablas, con conjuntos de datos de ejemplo a continuación:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

Para crear una sola tabla de gasto de publicidad que contenga ambos [!DNL Facebook] y [!DNL Google AdWords] campañas, debe escribir una consulta SQL y utilizar el complemento `UNION ALL` función. A `UNION ALL` La instrucción se utiliza generalmente para combinar varias consultas SQL distintas mientras se anexan los resultados de cada consulta a un único resultado.

Hay algunos requisitos de un `UNION` declaración que vale la pena mencionar, como se describe en PostgreSQL [documentación](https://www.postgresql.org/docs/8.3/queries-union.html):

* Todas las consultas deben devolver el mismo número de columnas
* Las columnas correspondientes deben tener tipos de datos idénticos

Al ejecutar un `UNION` o `UNION ALL` , los nombres de las columnas en el resultado final reflejan el nombre de las columnas en la primera consulta.

Normalmente, consolidando su [!DNL Facebook] y [!DNL Google AdWords] gastar datos en una `Data Warehouse View` requieren la creación de una tabla con siete columnas, con una consulta similar a la siguiente:

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

Un par de puntos importantes sobre lo anterior:

* Para mayor claridad, todas las columnas están suavizadas arriba de modo que los nombres coinciden en todas las consultas. Sin embargo, esto no es un requisito. El orden en el que se llama a las columnas en las consultas SELECT dicta cómo se alinean.
* Una nueva columna llamada `ad_source` se crea para facilitar el filtrado de [!DNL AdWords] o [!DNL Facebook] datos. Recuerde que esta consulta combina todos los datos de ambas tablas. Si no crea una columna como `ad_source`Sin embargo, no hay una manera fácil de identificar el gasto de una fuente en particular.

Guardar la consulta anterior como `Data Warehouse View` crea una tabla con ambos [!DNL Facebook] y [!DNL AdWords] Pase, similar al siguiente:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

En lugar de crear un conjunto independiente de métricas de marketing para cada fuente de publicidad, puede crear un único conjunto de métricas utilizando la tabla anterior para capturar todos los anuncios.

**¿Busca ayuda adicional?**

Escribir SQL y crear `Data Warehouse Views` no se incluye con el soporte técnico. Sin embargo, la variable [Equipo de servicios](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) ofrece asistencia en la creación de vistas. El equipo de asistencia puede ayudarle con todo tipo de tareas, desde migrar una base de datos heredada con una nueva base de datos para crear una única vista de Data Warehouse con el fin de realizar un análisis específico.

Generalmente, la creación de un nuevo `Data Warehouse View` a los efectos de consolidar 2-3 tablas de estructura similar requiere cinco horas de tiempo de servicios, lo que se traduce en aproximadamente $ 1.250 de trabajo. Sin embargo, a continuación se presentan algunos factores comunes que pueden aumentar la inversión esperada requerida:

* Consolidación de más de tres tablas en una sola vista
* Creación de más de una vista de Data Warehouse
* Lógica de unión compleja o condiciones de filtrado
* Consolidación de dos o más tablas con estructuras de datos diferentes
