---
title: Servicios de migración de datos
description: Aprenda todo lo que necesita para enviar una solicitud y comenzar la migración.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Migración de datos

La migración a un nuevo esquema de base de datos, servidor o base de datos de informes no tiene por qué ser estresante. El [[!DNL Adobe] equipo de servicios](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) ofrece asistencia para la migración.

Para garantizar que la transición sea lo más fluida posible, debe ser lo más detallado posible al enviar la solicitud de migración. Este tema tiene todo lo que necesita para enviar una solicitud y comenzar la migración. Proporcionarnos una imagen completa de sus necesidades garantiza que su proyecto tenga un alcance adecuado y que la estimación sea precisa.

## Primeros pasos {#started}

Antes de empezar, debe conocer las respuestas a estas preguntas:

* **¿La nueva base de datos se encuentra en un servidor nuevo?** Antes de enviar una solicitud, actualice la configuración de la conexión de datos en **[!UICONTROL Manage Data** > **Connections]**. Si necesita un actualizador sobre cómo hacerlo, vaya a la sección [`Integrations`](../integrations/integrations.md) y busque las instrucciones para el tipo de base de datos que está utilizando.

* **¿Todos los datos históricos existen en la nueva base de datos o es necesario migrarlos?**: puede consolidar los datos nuevos e históricos durante el proceso de migración. Aunque no necesite una consolidación, háganoslo saber en su solicitud.

Una vez que tenga las respuestas a lo anterior, debe saber el tipo de migración. ¿Tendrá la nueva base de datos el esquema [`same`](#sameschema) o tendrá un esquema [`different`](#newschema)? En las discusiones que se describen a continuación, encontrará instrucciones detalladas para cada tipo de migración.

## Migración a una nueva base de datos con el mismo esquema {#sameschema}

Al enviar la solicitud, indíquenos que el esquema de la base de datos no está cambiando y que la conexión ya está configurada en [!DNL Adobe Commerce Intelligence].

Si la base de datos tiene un nombre nuevo, inclúyalo en la solicitud para que se puedan migrar correctamente los paneles.

Si el nombre de la base de datos no cambia, la migración finaliza. Los paneles e informes se actualizarán cuando se complete la siguiente actualización completa.

## Migración a una nueva base de datos con un esquema diferente {#newschema}

>[!IMPORTANT]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

Para completar correctamente este tipo de migración, las columnas de datos existentes deben coincidir con sus equivalentes en la nueva base de datos. Esto no es obligatorio, pero hacer la coincidencia para nosotros ayuda a acelerar el tiempo de respuesta de su solicitud y a reducir el precio de la migración.

Si se siente cómodo haciendo la coincidencia usted mismo, siga estas instrucciones y adjunte la hoja de cálculo terminada a su solicitud:

1. Revise todas las tablas y columnas que se están sincronizando con su Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. En una hoja de cálculo, cree una pestaña para cada tabla que desee migrar a la nueva base de datos.

1. En cada pestaña, cree una columna para todas las columnas existentes que deban migrarse. Adobe recomienda ponerle un nombre similar a `Existing column name`.

1. También debe crear otra columna para los equivalentes de columna en la nueva base de datos en cada pestaña de la hoja de cálculo. Adobe recomienda que asigne a la columna un nombre similar a `New column name`.

1. Introduzca las columnas existentes y sus equivalentes. Si una columna existente no tiene un nuevo equivalente, escriba `N/A`.

   Además, si existe una nueva forma de calcular la misma información en la nueva base de datos, escríbala en la columna [`New column name`].

A continuación, se muestra un ejemplo:

![Plantilla de hoja de cálculo de migración con esquema de base de datos y estructura de tabla](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

## ¿Cómo envío una solicitud? {#submitreq}

Póngase en contacto con nosotros al [enviar una solicitud de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).

Si ha seguido los pasos de la sección anterior para crear la hoja de cálculo que coincide con la columna, no olvide adjuntarla.

## ¿Cuál es el siguiente paso? {#wrapup}

La determinación del ámbito del proyecto requiere cierta colaboración entre usted y el analista del equipo de servicios de Commerce que realiza la migración. La complejidad de los cambios y la capacidad de respuesta de usted y del analista afectan directamente a la cantidad de tiempo que puede tardar la migración. Una vez que haya analizado los detalles, se establecerá una cronología y se le enviará una declaración de trabajo.
