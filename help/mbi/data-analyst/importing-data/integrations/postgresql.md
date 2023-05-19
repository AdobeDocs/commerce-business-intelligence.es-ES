---
title: Conectar PostgreSQL mediante el túnel SSH
description: Aprenda a conectar la base de datos de PostgreSQL a Commerce Intelligence a través de un túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Connect [!DNL PostgreSQL] mediante [!DNL SSH Tunnel]

Para conectar su [!DNL PostgreSQL] base de datos a [!DNL Commerce Intelligence] mediante un `SSH tunnel`, debe hacer algunas cosas:

1. [Recupere el [!DNL Commerce Intelligence] clave pública](#retrieve)
1. [Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP](#allowlist)
1. [Crear un [!DNL Linux] usuario para [!DNL Commerce Intelligence] ](#linux)
1. [Crear un [!DNL PostgreSQL] usuario para [!DNL Commerce Intelligence] ](#postgres)
1. [Introduzca la conexión y la información de usuario en [!DNL Commerce Intelligence]](#finish)

## Recuperación del [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

El `public key` se utiliza para autorizar la [!DNL Commerce Intelligence] [!DNL Linux] usuario. Ahora creará el usuario e importará la clave.

1. Ir a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add a Data Source]**.
1. Haga clic en [!DNL PostgreSQL] icono.
1. Después del `PostgreSQL credentials` se abre la página, configure el `Encrypted` cambiar a `Yes`. Esto muestra el `SSH` formulario de configuración.
1. El `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

A continuación se muestra cómo navegar por [!DNL Commerce Intelligence] para recuperar la clave:

![Recuperación de la clave pública de RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde su dirección IP. Lo es `54.88.76.97/32`, pero también está en la `PostgreSQL` página credenciales. Consulte el cuadro azul en el GIF de arriba.

## Creación de un [!DNL Linux] usuario para [!DNL Commerce Intelligence] {#linux}

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) de cualquier manera que desee, siempre y cuando conserve el derecho de conectarse al [!DNL PostgreSQL] servidor.

1. Para agregar al nuevo usuario, ejecute los siguientes comandos como raíz en su [!DNL Linux] servidor:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Recuerde la `public key` ¿la recuperó en la primera sección? Para garantizar que el usuario tenga acceso a la base de datos, debe importar la clave en `authorized\_keys`.

   Copie la clave completa en el `authorized\_keys` como se indica a continuación:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para terminar de crear el usuario, modifique los permisos en la `/home/rjmetric` directorio para permitir el acceso mediante `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` el archivo asociado con el servidor no está establecido en la opción predeterminada, solo determinados usuarios tienen acceso al servidor; esto impide una conexión correcta a [!DNL Commerce Intelligence]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que el usuario rjmetric tenga acceso al servidor.

## Creación de un [!DNL Commerce Intelligence] [!DNL Postgres] usuario {#postgres}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando se inicia sesión en Postgres como usuario con el derecho de conceder privilegios. El usuario también debe ser propietario del esquema que [!DNL Commerce Intelligence] se le está otorgando acceso a.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Reemplazar `secure password` con su propia contraseña segura, que puede diferir de la contraseña SSH. Además, asegúrese de reemplazar `database name` y `schema name` con los nombres adecuados en la base de datos.

Si desea conectar varias bases de datos o esquemas, repita este proceso según sea necesario.

## Introducción de la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejaste el [!DNL PostgreSQL] ¿desea abrir la página credenciales? Si no es así, vaya a **[!UICONTROL Manage Data > Connections]** y haga clic en **[!UICONTROL Add a Data Source]** y, a continuación, el [!DNL PostgreSQL] icono. No olvide configurar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Username`: el nombre de usuario de RJMetrics Postgres (debe ser rjmetric)
* `Password`: la contraseña de Postgres de RJMetrics
* `Port`: Puerto PostgreSQL en el servidor (5432 de forma predeterminada)
* `Host`: 127.0.0.1

En `SSH Connection`:

* `Remote Address`: La dirección IP o el nombre de host del servidor en el que se SSH
* `Username`: su nombre de inicio de sesión SSH (debe ser jjjmetric)
* `SSH Port`: Puerto SSH en el servidor (22 de forma predeterminada)

Cuando haya terminado, haga clic en **Guardar y probar** para completar la configuración.

### Relacionado

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
