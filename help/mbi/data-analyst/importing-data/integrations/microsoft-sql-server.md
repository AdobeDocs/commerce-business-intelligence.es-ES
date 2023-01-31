---
title: Conectar Microsoft SQL Server
description: Obtenga información sobre cómo conectar la base de datos SQL de Microsoft a [!DNL MBI] en un proceso de cuatro pasos.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Conectar Microsoft SQL Server

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Este artículo explica cómo conectar su `Microsoft SQL` a [!DNL MBI] en un proceso de cuatro pasos. Este proceso requiere cierta experiencia técnica relacionada con las conexiones de servidor y SQL, y puede requerir la asistencia de los desarrolladores de su equipo.

Apoyamos [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure], y la mayoría de los demás proveedores de servidores en la nube. Si tiene una pregunta en su host particular, [enviar un ticket de asistencia](../../../guide-overview.md) solicitándonos que proporcione esta información.

Nuestro sistema debe ejecutar consultas SELECT en su base de datos. Inicialmente, lo hacemos para obtener una instantánea de la estructura de su base de datos y, a continuación, hacer horas extras regularmente para mantener nuestros datos actualizados. Nuestras actualizaciones son incrementales y limitamos la frecuencia y el tiempo de actualización para evitar cualquier carga no deseada en su servidor.

La mejor manera de hacerlo es conectarnos a su servidor de base de datos a través de TCP/IP. Cree un usuario para nosotros que solo pueda ejecutar consultas SELECT (y, opcionalmente, que solo pueda seleccionar datos de las tablas que especifique). Esto debe hacerse para cada uno de los servidores a los que se conectará [!DNL MBI].

## Conexión `Microsoft SQL` a [!DNL MBI]:

1. Asegúrese de que el servidor permita conexiones a través de TCP/IP y autenticación en modo mixto.

1. Asegúrese de que su cortafuegos permita que la IP dedicada de nuestro servidor se conecte.

   Puede encontrar la dirección IP que usaremos para conectar con su servidor en la sección de conexiones de su `Settings` página.

1. Cree un usuario que usaremos para iniciar sesión en su servidor de base de datos.  Tiene dos opciones: mediante `UI` o a través de una `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (segundo ejemplo)

1. Introduzca la dirección IP del servidor, el nombre de usuario y la contraseña en [!DNL MBI] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Haga clic en **[!UICONTROL Add a Data Source]**.

1. Seleccione para conectar un `Microsoft SQL` e introduzca sus credenciales en los campos de la nueva `Connections` página.

   Si está utilizando `Windows Azure`, también debe especificar un nombre de base de datos.
