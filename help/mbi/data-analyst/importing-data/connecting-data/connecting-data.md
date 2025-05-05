---
title: Conectar los datos
description: Obtenga información sobre cómo examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Conectar los datos

En [!DNL Adobe Commerce Intelligence], los orígenes de datos se llaman `integrations`. Una vez que un(a) `integration` se haya conectado correctamente, podrá examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.

Las integraciones se agregan y administran mediante la página `Connections`, a la cual se puede acceder haciendo clic en **[!UICONTROL Manage Data** > **Connections]**. Aquí puede ver lo siguiente:

* una lista de todas las integraciones conectadas a su cuenta

* el tipo de integración

* estado ([!DNL Google Analytics] y [!DNL Data Import API] conexiones tienen campos de estado en blanco)

* la última vez que se realizó una prueba de conexión (columna `Last Connection Started`)

![Datos\_Fuentes\_Tabla.png](../../../assets/Data_Sources_Table.png)

## Tipos de integraciones

Hay cuatro maneras de obtener los datos en [!DNL Commerce Intelligence]: conectar una base de datos, conectar una integración SaaS, cargar un archivo de `.csv` o usar la API de Adobe.

## Integraciones de bases de datos

![Base de datos\_icon.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] admite bases de datos basadas en SQL y NoSQL como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md) y [PostgreSQL](../integrations/postgresql.md).

Aunque puede conectar directamente la base de datos a [!DNL Commerce Intelligence] mediante las credenciales de la base de datos, Adobe recomienda utilizar un método de cifrado de eficacia comprobada como un túnel SSH. Esto garantiza que los datos estén seguros y protegidos a medida que avanzan hacia la Data Warehouse.

Según el método de conexión y el tipo de base de datos, puede ser necesario contar con algunos conocimientos técnicos para completar la configuración.

## Integraciones de `SaaS`

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` integraciones son servicios como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md) y [[!DNL Zendesk]](../integrations/zendesk.md). Como los datos de terceros residen en el servidor del proveedor, no puede acceder a ellos directamente como lo haría con los datos de la base de datos.

Normalmente, configurar una integración en [!DNL Commerce Intelligence] es tan fácil como simplemente escribir las credenciales de la cuenta. Algunos servicios pueden requerir una clave de API para completar la autorización. Consulte la [sección de integraciones](../integrations/integrations.md) para obtener instrucciones sobre cómo generar las credenciales que necesite.

## Carga de archivos

¿No está seguro de cómo obtener datos de una fuente complementaria en su Data Warehouse? [Usar la característica `File Upload`](../connecting-data/using-file-uploader.md) es una buena manera de extraer datos que no necesita para la toma de decisiones diaria. Siguiendo las reglas de formato, puede cargar rápidamente `.csv` archivos en su Data Warehouse y unirlos con otras fuentes de datos.

## [!DNL Commerce Intelligence] `Import API`

Si prefiere automatizar la recuperación de datos de uno de sus propios orígenes, puede utilizar [!DNL Commerce Intelligence] `Import API`. Básicamente, si no se encuentra en una base de datos o en una integración de `SaaS`, la función `Import API` es la mejor opción.

El uso de la API requiere un poco de experiencia técnica - alguien que se sienta cómodo con la escritura y el mantenimiento de un pequeño script Ruby o PHP es más que cualificado.

Para obtener más información sobre cómo empezar a usar `Import API`, consulte el [sitio para desarrolladores](https://developer.adobe.com/commerce/services/reporting/) y [cómo generar una clave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Añadir una integración

Para agregar una integración, haga clic en **[!UICONTROL Manage Data** > **Connections]** y luego en **[!UICONTROL Add a New Data Source]**. Haga clic en el icono de la integración que desee añadir y siga las instrucciones de los temas de ayuda para configurar las cosas:

* [Preguntas frecuentes sobre la integración](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponible ](../integrations/integrations.md)
* [Consolidación de tablas](../../../best-practices/consolidating-your-tables.md)
* [Restricción del acceso a la base de datos](../../../administrator/account-management/restrict-db-access.md)

**¿No ve la integración que desea?** Algunas integraciones deben activarse para que sean visibles en su cuenta. Si está buscando algo como [!DNL Facebook] pero no aparece en la lista, [envíe un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).

**Si ves un estado de error para una integración**, consulta la [sección de solución de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obtener ayuda.
