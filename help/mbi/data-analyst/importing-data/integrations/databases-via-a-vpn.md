---
title: Conexión de bases de datos mediante VPN
description: Aprenda a conectar bases de datos a través de una VPN en lugar de un túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Conexión de bases de datos mediante VPN

Mientras que Adobe recomienda conectar las bases de datos mediante un `SSH tunnel`, también puede utilizar un cifrado de `VPN` para mantener las cosas seguras. A `VPN` se puede utilizar para cualquiera de las integraciones de bases de datos y, para simplificar, el proceso es casi igual que configurar una `SSH tunnel`:

1. [Crear un [!DNL Commerce Intelligence] usuario base datos](#database)
1. [Crear un [!DNL Commerce Intelligence] usuario de VPN](#vpn)
1. [Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP](#allowlist)
1. [Introduzca la conexión y la información de usuario de VPN en Commerce Intelligence](#finish)

Además de las credenciales de la base de datos, debe introducir las credenciales de un usuario de VPN para ajustar las cosas. Cualquier usuario de VPN funciona, pero Adobe recomienda crear una [!DNL Commerce Intelligence] , ya que facilita el seguimiento de los usuarios en la cuenta.

## Creación de un usuario de base de datos para [!DNL Commerce Intelligence] {#database}

El proceso de creación de un usuario de base de datos varía según el tipo de base de datos que se conecte. Para ver las instrucciones de cada tipo de base de datos, haga clic en los vínculos siguientes.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creación de un `VPN` usuario para [!DNL Commerce Intelligence] {#vpn}

Como se mencionó anteriormente, cualquier `VPN` el usuario funciona, pero Adobe recomienda crear un usuario únicamente para [!DNL Commerce Intelligence] use.

## Permitir el acceso al [!DNL Commerce Intelligence] Direcciones IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Lo son `54.88.76.97` y `34.250.211.151`, pero también está en la `credentials` página para cualquier integración de base de datos:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Introducción de la conexión y `VPN` información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejaste la base de datos? `credentials` ¿página abierta? Si no es así, vaya a **[!UICONTROL Manage Data** > **Connections]**. Clic **[!UICONTROL Add New Data Source]** y, a continuación, haga clic en el icono de la base de datos que está conectando. No olvide cambiar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] usuario base datos
* `Password`: La contraseña para el [!DNL Commerce Intelligence] usuario base datos
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
* `Username`: La [!DNL Commerce Intelligence] `VPN` nombre de usuario
* `Password`: La [!DNL Commerce Intelligence] `VPN` contraseña de usuario

Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.
