---
title: Conectar sus datos
description: Obtenga información sobre cómo examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Conectar los datos

En [!DNL MBI], las fuentes de datos se denominan `integrations`. Después de un `integration` se ha conectado correctamente, podrá examinar las tablas disponibles para sincronizar en el Administrador de Datas Warehouse.

Las integraciones se agregan y administran usando la variable `Connections` , a la que se puede acceder haciendo clic en **[!UICONTROL Manage Data** > **Connections]**. Aquí puede ver una lista de todas las integraciones conectadas a su cuenta, el tipo de integración, el estado ([!DNL Google Analytics] y [!DNL Data Import API] las conexiones tendrán campos de estado en blanco) y la última vez una prueba de conexión (`Last Connection` columna Started ).

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipos de integraciones

Existen cuatro maneras de incorporar los datos en [!DNL MBI]: conectar una base de datos, conectar una integración SaaS, cargar un `.csv` o use nuestra API.

## Integraciones de la base de datos

![Base de datos\_icon.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] admite bases de datos noSQL y basadas en SQL como [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)y [PostgreSQL](../integrations/postgresql.md).

Aunque puede conectar directamente la base de datos a [!DNL MBI] con las credenciales de la base de datos, le recomendamos que utilice un método de cifrado probado como un túnel SSH. Esto garantizará que los datos permanezcan seguros y seguros a medida que entren en el almacén de datos.

Según el método de conexión y el tipo de base de datos, es posible que se necesite cierta experiencia técnica para completar la configuración.

## `SaaS` Integraciones

![](../../../assets/SaaS_icons.jpg)

`SaaS` las integraciones son servicios como [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)y [[!DNL Zendesk]](../integrations/zendesk.md). Es importante tener en cuenta que, como los datos de terceros residen en el servidor del proveedor, no se puede acceder directamente a ellos como se puede con los datos de la base de datos.

En la mayoría de los casos, la configuración de una integración en [!DNL MBI] es tan fácil como simplemente introducir sus credenciales de cuenta. Algunos servicios pueden requerir una clave de API para completar la autorización. Consulte la [sección integraciones](../integrations/integrations.md) para obtener instrucciones sobre cómo generar las credenciales que necesite.

## Carga de archivo

¿No está seguro de cómo obtener datos de una fuente complementaria en el almacén de datos? [Al usar la variable `File Upload` función](../connecting-data/using-file-uploader.md) es una buena manera de incorporar datos que no necesita para la toma de decisiones diaria. Siguiendo nuestras reglas de formato, puede cargar rápidamente `.csv` en el almacén de datos y únela a otras fuentes de datos.

## [!DNL MBI] `Import API`

Si prefiere automatizar la recuperación de datos desde una de sus propias fuentes, puede usar la variable [!DNL MBI] `Import API`. Básicamente: si no está en una base de datos o en una `SaaS` integración, `Import API` es tu mejor apuesta.

El uso de la API requiere un poco de experiencia técnica - alguien que esté cómodo con escribir y mantener un pequeño script Ruby o PHP estará más que cualificado.

Para obtener más información sobre cómo empezar a usar el `Import API`, consulte la [Sitio para desarrolladores](https://developer.adobe.com/commerce/services/reporting/) y [cómo generar una clave de API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Añadir una integración

Para añadir una integración, haga clic en **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add a New Data Source]**. Haga clic en el icono de la integración que desea agregar y siga las instrucciones de nuestros artículos de ayuda para configurar las cosas:

* [Preguntas frecuentes sobre la integración](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponible ](../integrations/integrations.md)
* [Consolidar las tablas](../../../best-practices/consolidating-your-tables.md)
* [Restricción del acceso a la base de datos](../../../administrator/account-management/restrict-db-access.md)

**¿No ve una integración que desee?** Algunas integraciones deben activarse para que puedan verse en su cuenta. Si está buscando algo, por ejemplo, [!DNL Facebook] - pero no aparece en la lista, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

**Si ve un estado de error para una integración**, no entrar en pánico: consulte la [Sección Resolución de problemas](https://support.magento.com/hc/en-us/sections/360003078151) para obtener ayuda.
