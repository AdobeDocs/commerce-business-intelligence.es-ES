---
title: Conectar PostgreSQL mediante el túnel SSH
description: Aprenda a conectar la base de datos PostgreSQL a Commerce Intelligence a través de un túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/IsDW3nNBF840BAd4zIhCDmHvFAFJv-1oQmrJw5MKh0Q
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 566
ht-degree: 0%

---

# Conectar [!DNL PostgreSQL] a través de [!DNL SSH Tunnel]

Para conectar la base de datos [!DNL PostgreSQL] a [!DNL Commerce Intelligence] a través de un `SSH tunnel`, debe hacer algunas cosas:

1. [Recuperar la clave pública  [!DNL Commerce Intelligence] ](#retrieve)
1. [Permitir el acceso a la dirección IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Crear un [!DNL Linux] usuario para [!DNL Commerce Intelligence]](#linux)
1. [Crear un [!DNL PostgreSQL] usuario para [!DNL Commerce Intelligence]](#postgres)
1. [Escriba la conexión y la información de usuario en  [!DNL Commerce Intelligence]](#finish)

## Recuperando [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

`public key` se usa para autorizar al usuario [!DNL Commerce Intelligence] [!DNL Linux]. Ahora creará el usuario e importará la clave.

1. Vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add a Data Source]**.
1. Haga clic en el icono [!DNL PostgreSQL].
1. Una vez abierta la página `PostgreSQL credentials`, establezca la opción `Encrypted` en `Yes`. Esto muestra el formulario de configuración `SSH`.
1. `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

A continuación se muestra cómo navegar por [!DNL Commerce Intelligence] para recuperar la clave:

![Recuperando la clave pública RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permitir acceso a la dirección IP [!DNL Commerce Intelligence] {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde su dirección IP. Es `54.88.76.97/32`, pero también se encuentra en la página de credenciales de `PostgreSQL`. Consulte el cuadro azul en la sección GIF anterior.

## Creando un usuario [!DNL Linux] para [!DNL Commerce Intelligence] {#linux}

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) como desee, siempre y cuando conserve el derecho de conectarse al servidor [!DNL PostgreSQL].

1. Para agregar al nuevo usuario, ejecute los siguientes comandos como raíz en el servidor [!DNL Linux]:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. ¿Recuerda el(la) `public key` que recuperó(ó) en la primera sección? Para asegurarse de que el usuario tiene acceso a la base de datos, debe importar la clave en `authorized\_keys`.

   Copie la clave completa en el archivo `authorized\_keys` de la siguiente manera:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para terminar de crear el usuario, modifique los permisos en el directorio `/home/rjmetric` para permitir el acceso a través de `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Si el archivo de `sshd\_config` asociado con el servidor no está establecido en la opción predeterminada, sólo determinados usuarios tienen acceso al servidor, lo que impide que la conexión a [!DNL Commerce Intelligence] se realice correctamente. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que el usuario rjmetric tenga acceso al servidor.

## Creando un usuario [!DNL Commerce Intelligence] [!DNL Postgres] {#postgres}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando se inicia sesión en Postgres como usuario con el derecho de conceder privilegios. El usuario también debe ser propietario del esquema al que se concede acceso a [!DNL Commerce Intelligence].

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Reemplace `secure password` con su propia contraseña segura, que puede ser diferente a la contraseña SSH. Además, asegúrese de reemplazar `database name` y `schema name` con los nombres apropiados en su base de datos.

Si desea conectar varias bases de datos o esquemas, repita este proceso según sea necesario.

## Introduciendo la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página de credenciales de [!DNL PostgreSQL]? Si no es así, vaya a **[!UICONTROL Manage Data > Connections]** y haga clic en **[!UICONTROL Add a Data Source]**, luego en el icono [!DNL PostgreSQL]. No olvide establecer la opción `Encrypted` en `Yes`.

Escriba la siguiente información en esta página, empezando por la sección `Database Connection`:

* `Username`: el nombre de usuario de RJMetrics Postgres (debe ser rjmetric)
* `Password`: la contraseña de Postgres de RJMetrics
* `Port`: puerto PostgreSQL en el servidor (5432 de forma predeterminada)
* `Host`: 127.0.0.1

En `SSH Connection`:

* `Remote Address`: la dirección IP o el nombre de host del servidor en el que se SSH
* `Username`: su nombre de inicio de sesión SSH (debe ser rjmetric)
* `SSH Port`: puerto SSH en el servidor (22 de forma predeterminada)

Cuando termine, haga clic en **[!UICONTROL Save & Test]** para completar la instalación.

>[!NOTE]
>
>Para la inscripción, actualización, mensajes de error y solución de problemas de la clave de host SSH, consulte [Verificación de la clave de host SSH](ssh-host-key-verification.md).

## Relacionado {#related}

* [Verificación de la clave del host SSH](ssh-host-key-verification.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
