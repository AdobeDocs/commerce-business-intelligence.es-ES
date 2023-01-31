---
title: Conectar MySQL mediante cPanel
description: Aprenda a conectar MySQL a través de cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Conectar MySQL mediante cPanel

* [Cree un [!DNL MBI] Usuario MySQL en cPanel](#cpanel)
* [Introducir la conexión y la información de usuario en MBI](#finish)

## Saltar a

* [MySQL vía túnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL mediante conexión directa](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>Le recomendamos encarecidamente que utilice SSH o cualquier otra forma de cifrado para proteger sus datos. Si esta no es una opción, aún puede conectarse directamente [!DNL MBI] a la base de datos siguiendo las instrucciones de este artículo.

En este artículo, lo acompañamos a través de la conexión directa de la base de datos MySQL a [!DNL MBI] usando cPanel&quot;. Este proceso también se puede utilizar para conectar [!DNL Magento] y cualquier otra base de datos de comercio electrónico basada en MySQL para [!DNL MBI].

1. Cree un [!DNL MBI] Usuario MySQL en `cPanel`
1. Introduzca la conexión y la información de usuario en [!DNL MBI]

Empiece.

## Creación de [!DNL MBI] Usuario MySQL en `cPanel` {#cpanel}

1. Inicie sesión en [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) a través de su proveedor de alojamiento.
1. Haga clic en **[!UICONTROL MySQL Databases]**, ubicado en el `Database` para obtener más información.
1. Desplácese hacia abajo hasta el `Add New User` y crear un usuario para [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Haga clic en **[!UICONTROL Create User]**.
1. Ahora que ha creado el usuario, debe asociarlo a una base de datos. Vuelva a la `Add New User` sección : consulte la configuración de `Add User to Database?` Eso es lo que necesitamos.
1. En el `User` en esta sección, seleccione el usuario que ha creado.
1. En el `Database` lista desplegable de esta sección, seleccione la base de datos a la que desea conectarse [!DNL MBI].
1. Haga clic en **[!UICONTROL Add]**.
1. Cuando aparezca la lista de privilegios, marque la casilla junto a `SELECT` - esto es todo [!DNL MBI] debe conectarse a la base de datos.

## Introducción de la conexión y la información del usuario en [!DNL MBI] {#finish}

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Dejó abierta la página de credenciales de MySQL? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego el icono MySQL.

Introduzca la siguiente información en esta página en la `Database Connection` sección:

* `Username`: El nombre de usuario de la variable [!DNL MBI] Usuario MySQL
* `Password`: La contraseña de la variable [!DNL MBI] Usuario MySQL
* `Port`: Puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: La dirección pública del `MySQL` server [!DNL MBI] se conectará a. Normalmente es la dirección URL que utiliza para iniciar sesión `cPanel`.

Si está utilizando un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), también deberá introducir la información de cifrado. Configure las variables `Encrypted` alternar a `Yes` para mostrar el formulario.

* `Connection Type`: Configure esto como `SSH Tunnel`
* `Remote Address`: La dirección IP o el nombre de host del servidor [!DNL MBI] entrarán en el túnel
* `Username`: El nombre de usuario de la variable [!DNL MBI] `SSH (Linux)` usuario, consulte [instrucciones](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) sobre cómo hacerlo, si aún no lo ha hecho)
* `SSH Port`: Puerto SSH en el servidor (`22` de forma predeterminada)

¡Eso es! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Relacionado:

* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
