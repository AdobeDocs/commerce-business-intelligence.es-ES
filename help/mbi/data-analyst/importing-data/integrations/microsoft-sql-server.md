---
title: Conectar Microsoft SQL Server
description: Aprenda a conectar su base de datos SQL de Microsoft a  [!DNL Commerce Intelligence] en un proceso de cuatro pasos.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/mJFBPJE334m7V8klJk-1xKAfsU4u4ObcwWDZzylJohM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 0%

---

# Conectar el servidor [!DNL Microsoft SQL]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![Logotipo de Microsoft SQL Server](../../../assets/MicrosoftSQLServer-logo.png)

En este tema se explica cómo conectar la base de datos [!DNL Microsoft SQL] a [!DNL Commerce Intelligence] en un proceso de cuatro pasos. Este proceso requiere cierta experiencia técnica relacionada con las conexiones de servidor y SQL, y puede requerir el apoyo de los desarrolladores de su equipo.

[!DNL Commerce Intelligence] admite [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure] y la mayoría de los demás proveedores de servidores en la nube. Si tiene alguna pregunta sobre su host en particular, [envíe un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) pidiéndonos que proporcionemos esta información.

El sistema debe ejecutar consultas SELECT en la base de datos. Esto se realiza inicialmente para obtener una instantánea de la estructura de la base de datos y, a continuación, con regularidad para mantener los datos actualizados. Las actualizaciones son graduales y Adobe restringe la frecuencia y el tiempo de las actualizaciones para evitar que se produzca una carga no deseada en el servidor.

La mejor manera de hacerlo es conectarnos al servidor de su base de datos a través de TCP/IP. Cree un usuario para que solo pueda ejecutar consultas SELECT (y, opcionalmente, solo pueda seleccionar datos de las tablas especificadas). Esto debe hacerse para cada uno de los servidores a los que se está conectando [!DNL Commerce Intelligence].

## Conectando `Microsoft SQL` a [!DNL Commerce Intelligence]:

1. Asegúrese de que el servidor permite conexiones a través de TCP/IP y autenticación de modo mixto.

1. Asegúrese de que el cortafuegos permita la conexión de la IP dedicada del servidor.

   Puede encontrar la dirección IP que se usa para conectarse al servidor en la sección conexiones de la página `Settings`.

1. Cree un usuario para iniciar sesión en el servidor de la base de datos. Tiene dos opciones; a través de `UI` o a través de `query`:
   * `UI`
   * `Query`

1. Escriba la dirección IP del servidor, el nombre de usuario y la contraseña en [!DNL Commerce Intelligence] en **[!UICONTROL Manage Data** > **Connections]**.

   ![Página Administrar conexiones de datos que muestra las integraciones de base de datos](../../../assets/manage-data-connections.png)

1. Haga clic en **[!UICONTROL Add a Data Source]**.

1. Seleccione para conectar una base de datos `Microsoft SQL` e introduzca sus credenciales en los campos de la nueva página `Connections`.

   Si usa `Windows Azure`, también debe especificar un nombre de base de datos.
