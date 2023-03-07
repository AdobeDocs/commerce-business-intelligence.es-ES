---
title: Conexión de bases de datos mediante VPN
description: Aprenda a conectar bases de datos a través de una VPN en lugar de un túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Conexión de bases de datos mediante VPN

Aunque el Adobe recomienda que conecte las bases de datos mediante un túnel SSH, también puede utilizar una conexión VPN cifrada para mantener las cosas seguras. A `VPN` se puede utilizar para cualquiera de las integraciones de bases de datos y, para simplificar, el proceso es casi igual que configurar una `SSH tunnel`:

1. [Crear un [!DNL MBI] usuario base datos](#database)
1. [Crear un [!DNL MBI] usuario de VPN](#vpn)
1. [Permitir el acceso al [!DNL MBI] Dirección IP](#allowlist)
1. [Introduzca la conexión y la información de usuario de VPN en MBI](#finish)

Además de las credenciales de la base de datos, debe introducir las credenciales de un usuario de VPN para ajustar las cosas. Cualquier usuario de VPN funciona, pero Adobe recomienda crear una [!DNL MBI] usuario: facilita el seguimiento de los usuarios en la cuenta.

## Creación de un usuario de base de datos para [!DNL MBI] {#database}

El proceso de creación de un usuario de base de datos varía según el tipo de base de datos que se conecte. Para ver las instrucciones de cada tipo de base de datos, haga clic en los vínculos siguientes.

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creación de un `VPN` usuario para [!DNL MBI] {#vpn}

Como se mencionó anteriormente, cualquier `VPN` el usuario funciona, pero Adobe recomienda crear un usuario únicamente para [!DNL MBI] use.

## Permitir el acceso al [!DNL MBI] Direcciones IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Lo son `54.88.76.97` y `34.250.211.151`, pero también está en la `credentials` página para cualquier integración de base de datos:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Introducción de la conexión y `VPN` información de usuario en [!DNL MBI] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL MBI]. ¿Dejaste la base de datos? `credentials` ¿página abierta? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego el icono de la base de datos a la que se está conectando. No olvide cambiar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Username`: El nombre de usuario del [!DNL MBI] usuario base datos
* `Password`: La contraseña para el [!DNL MBI] usuario base datos
* `Port`: el puerto de la base de datos en el servidor. Los valores predeterminados son:
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: De forma predeterminada, es localhost `127.0.0.1`, pero también podría ser la dirección IP pública del servidor o una dirección de red de área local.
* `Database Name (optional)`: si solo ha permitido el acceso a una base de datos (esto se especifica durante el paso de creación de usuario de la base de datos), introduzca el nombre de la base de datos aquí.

En el `Encryption Connection` sección:

* `Encryption Type`: establezca esto en `Cisco IPsec VPN`
* `Gateway Address`: la dirección IP del servidor VPN
* `Group Name`: nombre del grupo utilizado para la autenticación de grupos
* `Group Secret`: la contraseña correspondiente al grupo.
* `Username`: La [!DNL MBI] `VPN` nombre de usuario
* `Password`: La [!DNL MBI] `VPN` contraseña de usuario

¡Eso es todo! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.
