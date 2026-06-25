---
title: Conexión de bases de datos mediante VPN
description: Aprenda a conectar bases de datos a través de una VPN en lugar de un túnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0B7swwGIgBemitnx8Q4tyN8VtqwzcA-DYZdXHqzyNAk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: efc8727dd67a9ffcd7a8a1059ea93df8c6344599
workflow-type: tm+mt
source-wordcount: 414
ht-degree: 0%

---

# Conexión de bases de datos mediante VPN

Aunque Adobe recomienda conectar las bases de datos mediante `SSH tunnel`, también puede usar una conexión cifrada de `VPN` para mantener las cosas seguras. Para la inscripción de claves de host SSH, los errores y la solución de problemas en las conexiones de túnel SSH, consulte [Verificación de la clave de host SSH](ssh-host-key-verification.md). Se puede usar un `VPN` para cualquiera de las integraciones de la base de datos y, para que todo sea sencillo, el proceso es casi el mismo que configurar un `SSH tunnel`:

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

