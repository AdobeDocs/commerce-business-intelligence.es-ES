---
title: Conectar los datos
description: Obtenga información sobre cómo examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Conectar los datos

Entrada [!DNL Adobe Commerce Intelligence], las fuentes de datos se llaman `integrations`. Después de un `integration` se ha conectado correctamente, podrá examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.

Las integraciones se añaden y administran mediante `Connections` , a la que se puede acceder haciendo clic en **[!UICONTROL Manage Data** > **Connections]**. Aquí puede ver lo siguiente:

* una lista de todas las integraciones conectadas a su cuenta

* el tipo de integración

* estado ([!DNL Google Analytics] y [!DNL Data Import API] las conexiones tienen campos de estado en blanco)

* la última vez que una prueba de conexión (`Last Connection Started` column) se realizó

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipos de integraciones

Existen cuatro formas de introducir los datos en [!DNL Commerce Intelligence]: conecte una base de datos, conecte una integración de SaaS, cargue un `.csv` o utilice la API de Adobe.

## Integraciones de bases de datos

![Base de datos\_icon.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] admite bases de datos basadas en SQL y NoSQL como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), y [PostgreSQL](../integrations/postgresql.md).

Aunque puede conectar directamente la base de datos a [!DNL Commerce Intelligence] Con las credenciales de la base de datos, Adobe recomienda utilizar un método de encriptado de eficacia probada, como un túnel SSH. Esto garantiza que los datos estén seguros y protegidos a medida que avanzan hacia la Data Warehouse.

Según el método de conexión y el tipo de base de datos, puede ser necesario contar con algunos conocimientos técnicos para completar la configuración.

## `SaaS` Integraciones

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` Las integraciones son servicios como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), y [[!DNL Zendesk]](../integrations/zendesk.md). Como los datos de terceros residen en el servidor del proveedor, no puede acceder a ellos directamente como lo haría con los datos de la base de datos.

Normalmente, la configuración de una integración en [!DNL Commerce Intelligence] es tan fácil como simplemente introducir las credenciales de su cuenta. Algunos servicios pueden requerir una clave de API para completar la autorización. Consulte la [sección de integraciones](../integrations/integrations.md) para obtener instrucciones sobre cómo generar las credenciales que necesite.

## Carga de archivos

¿No está seguro de cómo obtener datos de una fuente complementaria en su Data Warehouse? [Uso del `File Upload` característica](../connecting-data/using-file-uploader.md) es una buena manera de extraer datos que no necesita para la toma de decisiones diaria. Siguiendo las reglas de formato, puede cargar rápidamente `.csv` archivos en la Data Warehouse y únalos a otras fuentes de datos.

## [!DNL Commerce Intelligence] `Import API`

Si prefiere automatizar la recuperación de datos de una de sus propias fuentes, puede utilizar el [!DNL Commerce Intelligence] `Import API`. Básicamente, si no está en una base de datos o en un `SaaS` integración, la `Import API` función es su mejor apuesta.

El uso de la API requiere un poco de experiencia técnica - alguien que se sienta cómodo con la escritura y el mantenimiento de un pequeño script Ruby o PHP es más que cualificado.

Para obtener más información sobre cómo empezar a utilizar `Import API`, consulte la [Sitio para desarrolladores](https://developer.adobe.com/commerce/services/reporting/) y [Cómo generar una clave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Añadir una integración

Para añadir una integración, haga clic en **[!UICONTROL Manage Data** > **Connections]** y luego haga clic en **[!UICONTROL Add a New Data Source]**. Haga clic en el icono de la integración que desee añadir y siga las instrucciones de los temas de ayuda para configurar las cosas:

* [Preguntas frecuentes sobre integración](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponible ](../integrations/integrations.md)
* [Consolidación de tablas](../../../best-practices/consolidating-your-tables.md)
* [Restricción del acceso a la base de datos](../../../administrator/account-management/restrict-db-access.md)

**¿No ve la integración que desea?** Algunas integraciones deben activarse para que sean visibles en su cuenta. Si está buscando algo como [!DNL Facebook] pero no aparece en la lista, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Si ve un estado de error para una integración**, consulte la [Sección Resolución de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obtener ayuda.
