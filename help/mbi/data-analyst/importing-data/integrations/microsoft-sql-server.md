---
title: Conectar Microsoft SQL Server
description: Obtenga información sobre cómo conectar la base de datos SQL de Microsoft a [!DNL Commerce Intelligence] en un proceso de cuatro pasos.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connect [!DNL Microsoft SQL] Servidor

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

En este tema se explica cómo conectar su [!DNL Microsoft SQL] base de datos a [!DNL Commerce Intelligence] en un proceso de cuatro pasos. Este proceso requiere cierta experiencia técnica relacionada con las conexiones de servidor y SQL, y puede requerir el apoyo de los desarrolladores de su equipo.

[!DNL Commerce Intelligence] admite [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]y la mayoría de los demás proveedores de servidores en la nube. Si tiene alguna pregunta sobre su host en particular, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) solicitándonos que proporcionemos esta información.

El sistema debe ejecutar consultas SELECT en la base de datos. Esto se realiza inicialmente para obtener una instantánea de la estructura de la base de datos y, a continuación, con regularidad para mantener los datos actualizados. Las actualizaciones son graduales y el Adobe restringe la frecuencia y el tiempo de actualización para evitar cualquier carga no deseada en el servidor.

La mejor manera de hacerlo es conectarnos al servidor de su base de datos a través de TCP/IP. Cree un usuario para que solo pueda ejecutar consultas SELECT (y, opcionalmente, solo pueda seleccionar datos de las tablas especificadas). Esto debe hacerse para cada uno de los servidores a los que se está conectando [!DNL Commerce Intelligence].

## Conectando `Microsoft SQL` hasta [!DNL Commerce Intelligence]:

1. Asegúrese de que el servidor permite conexiones a través de TCP/IP y autenticación de modo mixto.

1. Asegúrese de que el cortafuegos permita la conexión de la IP dedicada del servidor.

   Puede encontrar la dirección IP que se utiliza para conectarse al servidor en la sección de conexiones de su `Settings` página.

1. Cree un usuario que utilice para iniciar sesión en el servidor de base de datos. Tiene dos opciones; ya sea mediante `UI` o a través de un `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (segundo ejemplo)

1. Introduzca la dirección IP del servidor, el nombre de usuario y la contraseña en [!DNL Commerce Intelligence] bajo **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Clic **[!UICONTROL Add a Data Source]**.

1. Seleccione para conectar un `Microsoft SQL` e introduzca sus credenciales en los campos del nuevo `Connections` página.

   Si está utilizando `Windows Azure`, también debe especificar un nombre de base de datos.
