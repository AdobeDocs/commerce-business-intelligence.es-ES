---
title: Conectar MySQL a través de cPanel
description: Aprenda a conectar MySQL a través de cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Conectar MySQL a través de cPanel

* [Crear un [!DNL MBI] Usuario de MySQL en cPanel](#cpanel)
* [Introducir conexión e información de usuario en MBI](#finish)

## Saltar a

* [MySQL a través del túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL mediante conexión directa](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>El Adobe recomienda utilizar SSH u otra forma de cifrado para proteger los datos. Si esta no es una opción, aún puede conectarse directamente [!DNL MBI] a la base de datos siguiendo las instrucciones de este artículo.

Este artículo lo acompaña conectando directamente su base de datos MySQL a [!DNL MBI] usando `cPanel`. Este proceso también se puede utilizar para conectar [!DNL Adobe Commerce] y cualquier otra base de datos de comercio electrónico basada en MySQL para [!DNL MBI].

1. Crear un [!DNL MBI] Usuario de MySQL en `cPanel`
1. Especifique la conexión y la información de usuario en [!DNL MBI]

Empiece por.

## Creación de un [!DNL MBI] Usuario de MySQL en `cPanel` {#cpanel}

1. Iniciar sesión en [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) a través de su proveedor de alojamiento.
1. Clic **[!UICONTROL MySQL Databases]**, ubicado en el `Database` sección.
1. Desplácese hacia abajo hasta el `Add New User` y cree un usuario para [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clic **[!UICONTROL Create User]**.
1. Ahora que ha creado el usuario, debe asociarlo a una base de datos. Vuelva a la `Add New User` sección: consulte la configuración de `Add User to Database?` Eso es lo que necesitas.
1. En el `User` de esta sección, seleccione el usuario que ha creado.
1. En el `Database` de esta sección, seleccione la base de datos a la que desea conectarse [!DNL MBI].
1. Clic **[!UICONTROL Add]**.
1. Cuando aparezca la lista de comprobación de privilegios, marque la casilla junto a `SELECT` - esto es todo [!DNL MBI] necesita conectarse a la base de datos.

## Introducción de la conexión y la información de usuario en [!DNL MBI] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL MBI]. ¿Dejó abierta la página de credenciales de MySQL? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego el icono MySQL.

Introduzca la siguiente información en esta página en la `Database Connection` sección:

* `Username`: El nombre de usuario del [!DNL MBI] Usuario de MySQL
* `Password`: La contraseña para el [!DNL MBI] Usuario de MySQL
* `Port`: el puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: La dirección pública del `MySQL` server [!DNL MBI] se conecta a. Normalmente, es la dirección URL que se utiliza para iniciar sesión en `cPanel`.

Si utiliza un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), debe introducir la información de cifrado. Configure las variables `Encrypted` cambiar a `Yes` para mostrar el formulario.

* `Connection Type`: establezca esto en `SSH Tunnel`
* `Remote Address`: La dirección IP o el nombre de host del servidor [!DNL MBI] entrará en túnel
* `Username`: El nombre de usuario del [!DNL MBI] `SSH (Linux)` usuario, consulte [instrucciones](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre cómo hacerlo, si aún no lo ha hecho)
* `SSH Port`: Puerto SSH en el servidor (`22` de forma predeterminada)

¡Eso es todo! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Relacionado:

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
