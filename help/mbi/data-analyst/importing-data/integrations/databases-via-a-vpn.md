---
title: Conexión de bases de datos mediante VPN
description: Aprenda a conectar bases de datos a través de una VPN en lugar de un túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Conexión de bases de datos mediante VPN

Aunque el Adobe recomienda conectar las bases de datos mediante `SSH tunnel`, también puede utilizar una conexión cifrada de `VPN` para mantener las cosas seguras. Se puede usar un `VPN` para cualquiera de las integraciones de la base de datos y, para que todo sea sencillo, el proceso es casi el mismo que configurar un `SSH tunnel`:

1. [Crear un usuario de base de datos  [!DNL Commerce Intelligence] ](#database)
1. [Crear un usuario de  [!DNL Commerce Intelligence] VPN](#vpn)
1. [Permitir el acceso a la dirección IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Introduzca la conexión y la información de usuario de VPN en Commerce Intelligence](#finish)

Además de las credenciales de la base de datos, debe introducir las credenciales de un usuario de VPN para ajustar las cosas. Cualquier usuario de VPN funciona, pero Adobe recomienda crear un usuario de [!DNL Commerce Intelligence], ya que le facilita el seguimiento de los usuarios de su cuenta.

## Creando un usuario de base de datos para [!DNL Commerce Intelligence] {#database}

El proceso de creación de un usuario de base de datos varía según el tipo de base de datos que se conecte. Para ver las instrucciones de cada tipo de base de datos, haga clic en los vínculos siguientes.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creando un usuario `VPN` para [!DNL Commerce Intelligence] {#vpn}

Como se mencionó anteriormente, cualquier usuario de `VPN` válido funciona, pero Adobe recomienda crear un usuario únicamente para el uso de [!DNL Commerce Intelligence].

## Permitir acceso a las [!DNL Commerce Intelligence] direcciones IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentra en la página `credentials` para cualquier integración de base de datos:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Introduciendo la conexión y la información de usuario de `VPN` en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página de la base de datos `credentials`? Si no, vaya a **[!UICONTROL Manage Data** > **Connections]**. Haga clic en **[!UICONTROL Add New Data Source]** y, a continuación, haga clic en el icono de la base de datos que está conectando. No olvide cambiar la opción `Encrypted` a `Yes`.

Escriba la siguiente información en esta página, empezando por la sección `Database Connection`:

* `Username`: el nombre de usuario para el usuario de base de datos [!DNL Commerce Intelligence]
* `Password`: contraseña del usuario de la base de datos [!DNL Commerce Intelligence]
* `Port`: el puerto de la base de datos en el servidor. Los valores predeterminados son:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: de forma predeterminada, se trata del host local `127.0.0.1`, pero también podría ser la dirección IP pública del servidor o una dirección de red de área local.
* `Database Name (optional)`: si solo ha permitido el acceso a una base de datos (especificado durante el paso de creación del usuario de la base de datos), escriba el nombre de la base de datos aquí.

En la sección `Encryption Connection`:

* `Encryption Type`: establecer esto en `Cisco IPsec VPN`
* `Gateway Address`: la dirección IP del servidor VPN
* `Group Name`: nombre del grupo utilizado para la autenticación de grupo
* `Group Secret`: la contraseña correspondiente al grupo.
* `Username`: el nombre de usuario [!DNL Commerce Intelligence] `VPN`
* `Password`: la contraseña de usuario [!DNL Commerce Intelligence] `VPN`

Cuando termine, haga clic en **[!UICONTROL Save & Test]** para completar la instalación.
