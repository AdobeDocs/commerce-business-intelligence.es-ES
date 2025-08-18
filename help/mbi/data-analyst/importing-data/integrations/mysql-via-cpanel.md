---
title: Conectar MySQL a través de cPanel
description: Aprenda a conectar MySQL a través de cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Conectar [!DNL MySQL] a través de [!DNL cPanel]

* [Crear un usuario  [!DNL Commerce Intelligence] [!DNL MySQL] en  [!DNL cPanel]](#cpanel)
* [Escriba la conexión y la información de usuario en  [!DNL Commerce Intelligence]](#finish)

## Saltar a

* [[!DNL MySQL] a través de un túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] mediante conexión directa](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] recomienda usar SSH o algún otro tipo de cifrado para proteger los datos. Si no se trata de una opción, aún puede conectar directamente [!DNL Commerce Intelligence] a la base de datos siguiendo las instrucciones de este tema.

En este tema se explica cómo conectar directamente la base de datos de [!DNL MySQL] a [!DNL Commerce Intelligence] mediante [!DNL cPanel]. Este proceso también se puede usar para conectar [!DNL Adobe Commerce] y otras bases de datos de comercio electrónico basadas en MySQL a [!DNL Commerce Intelligence].

1. Crear un usuario [!DNL Commerce Intelligence] [!DNL MySQL] en [!DNL cPanel]
1. Escriba la conexión y la información de usuario en [!DNL Commerce Intelligence]

Empiece por.

## Creando un usuario [!DNL Commerce Intelligence] [!DNL MySQL] en [!DNL cPanel] {#cpanel}

1. Inicie sesión en [!DNL cPanel] a través de su proveedor de alojamiento.
1. Haga clic en **[!UICONTROL [!DNL MySQL] Databases]**, ubicado en la sección `Database`.
1. Desplácese hacia abajo hasta la sección `Add New User` y cree un usuario para [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Haga clic en **[!UICONTROL Create User]**.
1. Ahora que ha creado el usuario, debe asociarlo a una base de datos. Vuelva a la sección `Add New User` y vea la configuración de `Add User to Database?`, que es lo que necesita.
1. En el menú desplegable `User` de esta sección, seleccione el usuario que ha creado.
1. En el menú desplegable `Database` de esta sección, seleccione la base de datos a la que desea conectarse [!DNL Commerce Intelligence].
1. Haga clic en **[!UICONTROL Add]**.
1. Cuando aparezca la lista de comprobación de privilegios, marque la casilla junto a `SELECT`; esto es todo lo que [!DNL Commerce Intelligence] necesita para conectarse a la base de datos.

## Introduciendo la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página de credenciales de [!DNL MySQL]? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego en el icono [!DNL MySQL].

Escriba la siguiente información en esta página en la sección `Database Connection`:

* `Username`: el nombre de usuario para el usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: la contraseña del usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: la dirección pública del servidor `MySQL` [!DNL Commerce Intelligence] se conecta a. Suele ser la dirección URL que usa para iniciar sesión en `[!DNL cPanel]`.

Si usa un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), debe escribir la información de cifrado. Establezca el conmutador `Encrypted` en `Yes` para mostrar el formulario.

* `Connection Type`: establecer esto en `SSH Tunnel`
* `Remote Address`: la dirección IP o el nombre de host del servidor [!DNL Commerce Intelligence] se conectará mediante túnel a
* `Username`: el nombre de usuario para el usuario [!DNL Commerce Intelligence] `SSH (Linux)`, consulte [instrucciones](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre cómo hacerlo, si aún no lo ha hecho)
* `SSH Port`: puerto SSH en el servidor (`22` de forma predeterminada)

Cuando termine, haga clic en **[!UICONTROL Save & Test]** para completar la instalación.

## Relacionado:

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
