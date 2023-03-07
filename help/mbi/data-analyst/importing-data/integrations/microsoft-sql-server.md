---
title: Conectar Microsoft&reg;&reg; SQL Server
description: Aprenda a conectar su base de datos de Microsoft&reg; SQL a [!DNL MBI] en un proceso de cuatro pasos.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Conectar Microsoft® SQL Server

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Este artículo explica cómo conectar su `Microsoft SQL` base de datos a [!DNL MBI] en un proceso de cuatro pasos. Este proceso requiere cierta experiencia técnica relacionada con las conexiones de servidor y SQL, y puede requerir el apoyo de los desarrolladores de su equipo.

Compatibilidad con MBI [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]y la mayoría de los demás proveedores de servidores en la nube. Si tiene alguna pregunta sobre su host en particular, [enviar un ticket de asistencia](../../../guide-overview.md) solicitándonos que proporcionemos esta información.

El sistema debe ejecutar consultas SELECT en la base de datos. Esto se realiza inicialmente para obtener una instantánea de la estructura de la base de datos y, a continuación, con regularidad para mantener los datos actualizados. Las actualizaciones son graduales y el Adobe restringe la frecuencia y el tiempo de actualización para evitar cualquier carga no deseada en el servidor.

La mejor manera de hacerlo es conectarnos al servidor de su base de datos a través de TCP/IP. Cree un usuario para que solo pueda ejecutar consultas SELECT (y, opcionalmente, solo pueda seleccionar datos de las tablas especificadas). Esto debe hacerse para cada uno de los servidores a los que se está conectando [!DNL MBI].

## Conectando `Microsoft SQL` hasta [!DNL MBI]:

1. Asegúrese de que el servidor permite conexiones a través de TCP/IP y autenticación de modo mixto.

1. Asegúrese de que el cortafuegos permita la conexión de la IP dedicada del servidor.

   Puede encontrar la dirección IP que se utiliza para conectarse al servidor en la sección de conexiones de su `Settings` página.

1. Cree un usuario que utilice para iniciar sesión en el servidor de base de datos. Tiene dos opciones; ya sea mediante `UI` o a través de un `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (segundo ejemplo)

1. Introduzca la dirección IP del servidor, el nombre de usuario y la contraseña en [!DNL MBI] bajo **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Clic **[!UICONTROL Add a Data Source]**.

1. Seleccione para conectar un `Microsoft SQL` e introduzca sus credenciales en los campos del nuevo `Connections` página.

   Si está utilizando `Windows Azure`, también debe especificar un nombre de base de datos.
