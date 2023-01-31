---
title: Servicios de migración de datos
description: Conozca todo lo que necesita para enviar una solicitud y comience con la migración.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Migración de datos

La migración a un nuevo esquema de base de datos, servidor o base de datos de informes no tiene que ser estresante. Nuestra **[!DNL Magento Services - Analytics]** El equipo ofrece asistencia para la migración - hacemos todo el trabajo pesado para que no tenga que hacerlo.

Para garantizar que la transición sea lo más fluida posible, le solicitamos que sea lo más detallada posible al enviar su solicitud de migración. En este artículo se muestra todo lo que se necesita para enviar una solicitud y comenzar la migración. Proporcionarnos una imagen completa de sus necesidades garantizará que su proyecto tenga un alcance adecuado y que la estimación sea precisa.

## Introducción {#started}

Antes de profundizar, debe conocer las respuestas a estas preguntas:

* **¿La nueva base de datos está en un nuevo servidor?** Antes de enviar una solicitud, actualice la configuración de la conexión de datos en **[!UICONTROL Manage Data** > **Connections]**. Si necesita actualizarse sobre cómo hacerlo, vaya a la [`Integrations`](../integrations/integrations.md) y busque las instrucciones para el tipo de base de datos que está utilizando.
* **¿Todos los datos históricos existen en la nueva base de datos o es necesario migrarlos?** Podemos consolidar los datos históricos y nuevos durante el proceso de migración. Incluso si no necesita una consolidación, le pedimos que nos informe en su solicitud.

Una vez que tenga las respuestas a lo anterior, necesitaremos saber el tipo de migración: la nueva base de datos tendrá la variable [`same`](#sameschema) esquema, o tendrá un [`different`](#newschema) esquema? En las secciones siguientes, encontrará instrucciones detalladas para cada tipo de migración.

## Migración a una nueva base de datos con el mismo esquema {#sameschema}

Al enviar la solicitud, indíquenos que el esquema de la base de datos no está cambiando y que la conexión ya está configurada en [!DNL MBI].

Si la base de datos tiene un nombre nuevo, inclúyalo en la solicitud para que los paneles se puedan migrar correctamente.

Si el nombre de la base de datos no cambia, la migración se completa. Los tableros y los informes se actualizarán una vez completada la siguiente actualización completa. Le pedimos que siga contactando con nosotros para que podamos mantenernos por delante de cualquier problema que pueda resultar de la migración.

## Migración a una nueva base de datos con un esquema diferente {#newschema}

>[!IMPORTANT]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

Para completar correctamente este tipo de migración, las columnas de datos existentes deben coincidir con sus equivalentes en la nueva base de datos. Esto no es obligatorio para usted, pero realizar la correspondencia para nosotros ayudará a acelerar el tiempo de respuesta de su solicitud y a reducir el precio de la migración.

Si se siente cómodo haciendo la coincidencia usted mismo, siga estas instrucciones y adjunte la hoja de cálculo finalizada a la solicitud:

1. Revise todas las tablas y columnas que estén sincronizadas con la Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. En una hoja de cálculo, cree una pestaña para cada tabla que desee migrar a la nueva base de datos.
1. En cada pestaña, cree una columna para todas las columnas existentes que deban migrarse. Se recomienda ponerle un nombre similar a `Existing column name`.
1. También es necesario crear otra columna para los equivalentes de columna en la nueva base de datos en cada pestaña de la hoja de cálculo. Se recomienda asignar un nombre a la columna como `New column name`.
1. Introduzca las columnas existentes y sus equivalentes. Si una columna existente no tiene un nuevo equivalente, simplemente introduzca `N/A`.

   Además, si hay una nueva forma de calcular la misma información en la nueva base de datos, indíquela en la [`New column name`] para abrir el Navegador.

A continuación se muestra un ejemplo:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Si determinadas columnas de datos no tienen columnas equivalentes en la nueva base de datos, existe la posibilidad de que se pierdan ciertos análisis en el proceso.

## ¿Cómo puedo enviar una solicitud? {#submitreq}

Puede ponerse en contacto con nosotros a través de [envío de una solicitud de asistencia](../../../guide-overview.md).

Si ha seguido los pasos de la sección anterior para crear la hoja de cálculo coincidente de columna, no olvide adjuntarla.

## ¿Qué sigue? {#wrapup}

La determinación del ámbito del proyecto requerirá cierta colaboración entre usted y el analista del equipo de servicios de comercio que realice la migración. La complejidad de los cambios y la capacidad de respuesta de usted y el analista afectan directamente a la cantidad de tiempo que puede tardar la migración. Después de detallar los detalles, se establecerá un cronograma y se le enviará una declaración de trabajo.
