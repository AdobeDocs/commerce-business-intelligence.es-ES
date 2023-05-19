---
title: Conectar MySQL a través de cPanel
description: Aprenda a conectar MySQL a través de cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Connect [!DNL MySQL] mediante [!DNL cPanel]

* [Crear un [!DNL Commerce Intelligence] [!DNL MySQL] usuario en [!DNL cPanel]](#cpanel)
* [Especifique la conexión y la información de usuario en [!DNL Commerce Intelligence]](#finish)

## Saltar a

* [[!DNL MySQL] a través del túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] mediante conexión directa](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] recomienda utilizar SSH o cualquier otra forma de cifrado para proteger los datos. Si esta no es una opción, aún puede conectarse directamente [!DNL Commerce Intelligence] a la base de datos con las instrucciones de este tema.

Este tema le guiará a través de la conexión directa de [!DNL MySQL] base de datos a [!DNL Commerce Intelligence] usando [!DNL cPanel]. Este proceso también se puede utilizar para conectar [!DNL Adobe Commerce] y cualquier otra base de datos de comercio electrónico basada en MySQL para [!DNL Commerce Intelligence].

1. Crear un [!DNL Commerce Intelligence] [!DNL MySQL] usuario en [!DNL cPanel]
1. Especifique la conexión y la información de usuario en [!DNL Commerce Intelligence]

Empiece por.

## Creación de un [!DNL Commerce Intelligence] [!DNL MySQL] usuario en [!DNL cPanel] {#cpanel}

1. Iniciar sesión en [!DNL cPanel] a través de su proveedor de alojamiento.
1. Clic **[!UICONTROL [!DNL MySQL] Databases]**, ubicado en el `Database` sección.
1. Desplácese hacia abajo hasta el `Add New User` y cree un usuario para [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clic **[!UICONTROL Create User]**.
1. Ahora que ha creado el usuario, debe asociarlo a una base de datos. Vuelva a la `Add New User` sección: consulte la configuración de `Add User to Database?` Eso es lo que necesitas.
1. En el `User` de esta sección, seleccione el usuario que ha creado.
1. En el `Database` de esta sección, seleccione la base de datos a la que desea conectarse [!DNL Commerce Intelligence].
1. Clic **[!UICONTROL Add]**.
1. Cuando aparezca la lista de comprobación de privilegios, marque la casilla junto a `SELECT` - esto es todo [!DNL Commerce Intelligence] necesita conectarse a la base de datos.

## Introducción de la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejaste el [!DNL MySQL] ¿desea abrir la página credenciales? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]** y, a continuación, el [!DNL MySQL] icono.

Introduzca la siguiente información en esta página en la `Database Connection` sección:

* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Password`: La contraseña para el [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Port`: el puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: La dirección pública del `MySQL` server [!DNL Commerce Intelligence] se conecta a. Normalmente, es la dirección URL que se utiliza para iniciar sesión en `[!DNL cPanel]`.

Si utiliza un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), debe introducir la información de cifrado. Configure las variables `Encrypted` cambiar a `Yes` para mostrar el formulario.

* `Connection Type`: establezca esto en `SSH Tunnel`
* `Remote Address`: La dirección IP o el nombre de host del servidor [!DNL Commerce Intelligence] entrará en túnel
* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] `SSH (Linux)` usuario, consulte [instrucciones](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre cómo hacerlo, si aún no lo ha hecho)
* `SSH Port`: Puerto SSH en el servidor (`22` de forma predeterminada)

Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Relacionado:

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
