---
title: Conexión de bases de datos mediante VPN
description: Aprenda a conectar bases de datos a través de VPN en lugar de SSH Tunnel.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Conexión de bases de datos mediante VPN

Aunque le recomendamos que conecte sus bases de datos mediante un túnel SSH, también puede utilizar una conexión VPN cifrada para mantener las cosas seguras. A `VPN` puede utilizarse para cualquiera de nuestras integraciones de base de datos y, para mantener las cosas simples, el proceso es casi igual que configurar un `SSH tunnel`:

1. [Cree un [!DNL MBI] usuario de base de datos](#database)
1. [Cree un [!DNL MBI] Usuario VPN](#vpn)
1. [Permita el acceso al [!DNL MBI] Dirección IP](#allowlist)
1. [Introduzca la conexión y la información de usuario de VPN en MBI](#finish)

Además de las credenciales de la base de datos, tendrá que introducir las credenciales de un usuario VPN para ajustar las cosas. Cualquier usuario VPN funcionará, pero le recomendamos que cree un [!DNL MBI] usuario : le facilita mantener un seguimiento de los usuarios de su cuenta.

Empecemos.

## Creación de un usuario de base de datos para [!DNL MBI] {#database}

El proceso para crear un usuario de base de datos variará según el tipo de base de datos que se esté conectando. Para ver las instrucciones de cada tipo de base de datos, haga clic en los vínculos siguientes.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creación de `VPN` usuario para [!DNL MBI] {#vpn}

Como hemos mencionado anteriormente, cualquier `VPN` funcionará, pero recomendamos encarecidamente que cree un usuario solo para [!DNL MBI] use.

## Permita el acceso al [!DNL MBI] Direcciones IP {#allowlist}

Para que la conexión sea correcta, debe configurar el cortafuegos para permitir el acceso desde nuestras direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentra en el `credentials` para cualquier integración de base de datos:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Introducción de la conexión y `VPN` información de usuario en [!DNL MBI] {#finish}

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Ha salido de la base de datos? `credentials` apertura de página? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]** y, a continuación, el icono de la base de datos que está conectando. no olvide cambiar la variable `Encrypted` alternar a `Yes`.

Introduzca la siguiente información en esta página, empezando por el `Database Connection` sección:

* `Username`: El nombre de usuario de la variable [!DNL MBI] usuario de base de datos
* `Password`: La contraseña de la variable [!DNL MBI] usuario de base de datos
* `Port`: Puerto de la base de datos en el servidor. Los valores predeterminados son:
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: De forma predeterminada, será localhost `127.0.0.1`, pero también podría ser la dirección IP pública de su servidor o una dirección de red de área local.
* `Database Name (optional)`: Si solo ha permitido el acceso a una base de datos (esto se especifica durante el paso de creación de usuarios de la base de datos), introduzca el nombre de esa base de datos aquí.

En el `Encryption Connection` sección:

* `Encryption Type`: Configure esto como `Cisco IPsec VPN`
* `Gateway Address`: La dirección IP del servidor VPN
* `Group Name`: Nombre del grupo utilizado para la autenticación de grupo
* `Group Secret`: La contraseña correspondiente al grupo.
* `Username`: La variable [!DNL MBI] `VPN` username
* `Password`: La variable [!DNL MBI] `VPN` contraseña de usuario

¡Eso es! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.
