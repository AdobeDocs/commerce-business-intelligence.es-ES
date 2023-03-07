---
title: Servicios de migración de datos
description: Aprenda todo lo que necesita para enviar una solicitud y comenzar la migración.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Migración de datos

La migración a un nuevo esquema de base de datos, servidor o base de datos de informes no tiene por qué ser estresante. El **[!DNL Adobe Commerce Services - Analytics]** equipo de ofrece asistencia para la migración.

Para garantizar que la transición sea lo más fluida posible, debe ser lo más detallado posible al enviar la solicitud de migración. En este artículo encontrará todo lo que necesita para enviar una solicitud y comenzar la migración. Proporcionarnos una imagen completa de sus necesidades garantiza que su proyecto tenga un alcance adecuado y que la estimación sea precisa.

## Primeros pasos {#started}

Antes de empezar, debe conocer las respuestas a estas preguntas:

* **¿La nueva base de datos está en un servidor nuevo?** Antes de enviar una solicitud, actualice la configuración de la conexión de datos en **[!UICONTROL Manage Data** > **Connections]**. Si necesita un repaso sobre cómo hacerlo, vaya a la [`Integrations`](../integrations/integrations.md) y busque las instrucciones para el tipo de base de datos que está utilizando.
* **¿Todos los datos históricos existen en la nueva base de datos o es necesario migrarlos?** Puede consolidar los datos nuevos e históricos durante el proceso de migración. Aunque no necesite una consolidación, háganoslo saber en su solicitud.

Una vez que tenga las respuestas a lo anterior, debe conocer el tipo de migración: ¿tendrá la nueva base de datos el [`same`](#sameschema) esquema, o tendrá un esquema [`different`](#newschema) esquema? En las secciones siguientes, encontrará instrucciones detalladas para cada tipo de migración.

## Migración a una nueva base de datos con el mismo esquema {#sameschema}

Al enviar la solicitud, indíquenos que el esquema de la base de datos no está cambiando y que la conexión ya está configurada en [!DNL MBI].

Si la base de datos tiene un nombre nuevo, inclúyalo en la solicitud para que se puedan migrar correctamente los paneles.

Si el nombre de la base de datos no cambia, la migración finaliza. Los paneles e informes se actualizarán cuando se complete la siguiente actualización completa. Póngase en contacto con el Adobe de para poder adelantarse a los problemas que puedan derivarse de la migración.

## Migración a una nueva base de datos con un esquema diferente {#newschema}

>[!IMPORTANT]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

Para completar correctamente este tipo de migración, las columnas de datos existentes deben coincidir con sus equivalentes en la nueva base de datos. Esto no es obligatorio, pero hacer la coincidencia para nosotros ayuda a acelerar el tiempo de respuesta de su solicitud y a reducir el precio de la migración.

Si se siente cómodo haciendo la coincidencia usted mismo, siga estas instrucciones y adjunte la hoja de cálculo terminada a su solicitud:

1. Revise todas las tablas y columnas que se están sincronizando con su Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. En una hoja de cálculo, cree una pestaña para cada tabla que desee migrar a la nueva base de datos.
1. En cada pestaña, cree una columna para todas las columnas existentes que deban migrarse. Adobe recomienda ponerle un nombre similar al siguiente `Existing column name`.
1. También debe crear otra columna para los equivalentes de columna en la nueva base de datos en cada pestaña de la hoja de cálculo. El Adobe recomienda que la columna tenga un nombre similar al siguiente `New column name`.
1. Introduzca las columnas existentes y sus equivalentes. Si una columna existente no tiene un nuevo equivalente, introduzca `N/A`.

   Además, si existe una nueva forma de calcular la misma información en la nueva base de datos, indíquela en la [`New column name`] columna.

A continuación, se muestra un ejemplo:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

## ¿Cómo envío una solicitud? {#submitreq}

Puede ponerse en contacto con nosotros mediante [enviar una solicitud de asistencia](../../../guide-overview.md).

Si ha seguido los pasos de la sección anterior para crear la hoja de cálculo que coincide con la columna, no olvide adjuntarla.

## ¿Cuál es el siguiente paso? {#wrapup}

La determinación del ámbito del proyecto requiere cierta colaboración entre usted y el analista del equipo de Commerce Services que realiza la migración. La complejidad de los cambios y la capacidad de respuesta de usted y del analista afectan directamente a la cantidad de tiempo que puede tardar la migración. Una vez que haya analizado los detalles, se establecerá una cronología y se le enviará una declaración de trabajo.
