---
title: Crear y utilizar vistas de Data Warehouse
description: Obtenga información sobre un método para crear nuevas tablas almacenadas mediante la modificación de una tabla existente o la unión o consolidación de varias tablas juntas mediante el uso de SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Uso de vistas de Data Warehouse

Este documento describe el propósito y los usos de `Data Warehouse Views` accesible navegando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. A continuación se explica qué hace y cómo crear nuevas vistas, así como un ejemplo de cómo utilizar `Data Warehouse Views` consolidar [!DNL Facebook] y [!DNL AdWords] gastar datos.

## Objetivo general

La variable `Data Warehouse Views` es un método para crear nuevas tablas almacenadas mediante la modificación de una tabla existente o uniendo o consolidando varias tablas mediante el uso de SQL. Una vez `Data Warehouse View` ha sido creado y procesado por un ciclo de actualización, se rellenará en la Data Warehouse como una nueva tabla en la sección `Data Warehouse Views` como se muestra a continuación:

![](../../assets/Data_Warehouse.png)

Desde aquí, la nueva vista funciona como cualquier otra tabla, lo que le da la capacidad de crear nuevas columnas calculadas o crear métricas e informes sobre ella.

`Data Warehouse Views` se utilizan principalmente para consolidar varias tablas similares pero diferentes juntas, de modo que todos los informes se puedan crear en una sola tabla nueva. Algunos ejemplos comunes incluyen la consolidación de tablas de una base de datos heredada y una base de datos activa para combinar datos actuales e históricos, o la combinación de varias fuentes de publicidad como Facebook y AdWords en un único `Consolidated ad spend` tabla.

Si está familiarizado con SQL, ambos ejemplos de consolidación utilizan la variable `UNION` , pero puede utilizar cualquier sintaxis y función PostgreSQL al crear una nueva vista.

## Creación y administración de vistas de Data Warehouse

Nuevo `Data Warehouse Views` se puede crear y eliminar las vistas existentes navegando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, como se muestra a continuación:

![](../../assets/Data_Warehouse_Views.png)

Desde aquí puede crear una nueva vista siguiendo las instrucciones de ejemplo que se indican a continuación:

1. Si observa una vista existente, haga clic en **[!UICONTROL New Data Warehouse View]** para abrir una ventana de consulta en blanco. Si ya se ha abierto una ventana de consulta en blanco, continúe con el paso siguiente.
1. Asigne un nombre a la vista al escribir en el `View Name` campo . El nombre proporcionado aquí determinará el nombre para mostrar de la vista en la Data Warehouse. `View names` se limitan a letras minúsculas, números y guiones bajos (_). Todos los demás caracteres están prohibidos.
1. Introduzca la consulta en la ventana titulada `Select Query`, utilizando la sintaxis estándar PostgreSQL.
   >[!NOTE]
   >
   >La consulta debe hacer referencia a nombres de columna específicos. El uso de `*`no está permitido seleccionar todas las columnas.

1. Cuando haya terminado, haga clic en **[!UICONTROL Save]** para guardar la vista. Tenga en cuenta que la vista tendrá temporalmente un `Pending` hasta que se procese en el siguiente ciclo de actualización completo, momento en el que el estado cambiará a `Active`. Una vez procesada por una actualización, la vista está lista para utilizarse en los informes.

Es importante mencionar que después de guardar, la consulta subyacente utilizada para generar un `Data Warehouse View` no se puede editar. Si, por alguna razón, es necesario ajustar la estructura de un `Data Warehouse View`, deberá crear una nueva vista y migrar manualmente cualquier columna, métrica o informe calculado de la vista original a la nueva. Una vez completada la migración, puede eliminar la vista original de forma segura. Porque `Data Warehouse Views` no son editables, se recomienda encarecidamente que pruebe el resultado de la consulta mediante la variable `SQL Report Builder` antes de guardar la consulta como vista de Data Warehouse.

## Ejemplo: [!DNL Facebook] y [!DNL Google AdWords] data

Echemos un vistazo a uno de los ejemplos mencionados anteriormente en este artículo: consolidación [!DNL Facebook] y [!DNL AdWords] gastar datos en una nueva tabla de anuncios consolidados. Normalmente, esto implica la consolidación de dos tablas, con conjuntos de datos de ejemplo a continuación:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 05-05-2017:00:00 | 2000 | 10,2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4,6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2,5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14 500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 01-05-2017:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2,5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1,2 |

Para crear una sola tabla de gasto de publicidad que contenga ambos [!DNL Facebook] y [!DNL AdWords] campañas, tendremos que escribir una consulta SQL y usar la variable `UNION ALL` función. A `UNION ALL` se utiliza generalmente para combinar varias consultas SQL distintas al anexar los resultados de cada consulta a un único resultado.

Hay algunos requisitos de un `UNION` , tal como se describe en PostgreSQL [documentación](https://www.postgresql.org/docs/8.3/queries-union.html):

* Todas las consultas deben devolver el mismo número de columnas
* Las columnas correspondientes deben tener tipos de datos idénticos

Al ejecutar un `UNION` o `UNION ALL` , los nombres de las columnas de la salida final reflejan el nombre de las columnas de la primera consulta.

En la mayoría de los casos, la consolidación de [!DNL Facebook] y [!DNL Google AdWords] gastar datos en un `Data Warehouse View` requerirá la creación de una tabla con siete columnas, con una consulta similar a la siguiente:

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

* En aras de la claridad, todas las columnas tienen un alias superior, de modo que los nombres coincidan en todas las consultas. Sin embargo, esto no es un requisito. El orden en que se llaman las columnas en las consultas SELECT dicta cómo están alineadas.
* Una nueva columna llamada `ad_source` se crea para facilitar el filtro de [!DNL AdWords] o [!DNL Facebook] datos. Recuerde que esta consulta combina todos los datos de ambas tablas. Si no crea una columna como `ad_source`, no habrá forma fácil de identificar el gasto de una fuente en particular.

Guardar la consulta anterior como un `Data Warehouse View` creará una nueva tabla con ambas [!DNL Facebook] y [!DNL AdWords] gastar, similar a lo que se muestra a continuación:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 01-05-2017:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 05-05-2017:00:00 | eee | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14 500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28,5 | 10200 | 280 |

En lugar de crear un conjunto separado de métricas de marketing para cada fuente de publicidad, ahora puede crear un solo conjunto de métricas usando la tabla anterior para capturar todas las publicidades.

**¿Busca ayuda adicional?**

Escritura de SQL y creación `Data Warehouse Views` no se incluye con el soporte técnico.  Sin embargo, el equipo de Servicios sí ofrece asistencia para la creación de vistas. Para todo, desde la migración y consolidación de una base de datos heredada con una nueva base de datos hasta la creación de una única vista de Data Warehouse para fines de análisis específicos, son expertos en depurar soluciones basadas en SQL para todos los desafíos de estructura de datos.

En la mayoría de los casos, la creación de un `Data Warehouse View` a los efectos de consolidar 2 a 3 cuadros de estructura similar requieren 5 horas de tiempo de servicios, lo que equivale a aproximadamente 1.250 dólares de trabajo. Sin embargo, a continuación se presentan algunos factores comunes que pueden aumentar la inversión esperada necesaria:

* Consolidación de más de 3 tablas en una sola vista
* Creación de más de una vista del almacén de datos
* Lógica de unión compleja o condiciones de filtrado
* Consolidación de dos o más tablas con estructuras de datos diferentes
