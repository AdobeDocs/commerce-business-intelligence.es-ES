---
title: Conectar PostgreSQL a través del túnel SSH
description: Obtenga información sobre cómo conectar la base de datos PostgreSQL a [!DNL MBI] a través de un túnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Connect `PostgreSQL` via `SSH` Túnel

Para conectar su `PostgreSQL` a [!DNL MBI] mediante una `SSH tunnel`, usted (o su equipo, si no es técnico) tendrá que hacer algunas cosas:

1. [Recupere el [!DNL MBI] clave pública](#retrieve)
1. [Permita el acceso al [!DNL MBI] Dirección IP](#allowlist)
1. [Crear un usuario de Linux para [!DNL MBI] ](#linux)
1. [Crear un usuario de Postgres para [!DNL MBI] ](#postgres)
1. [Introduzca la conexión y la información de usuario en MBI](#finish)

No es tan complicado como podría sonar. Empiece.

## Recuperación de la variable [!DNL MBI] `public key` {#retrieve}

La variable `public key` se usa para autorizar la variable [!DNL MBI] Usuario Linux. En la siguiente sección, crearemos el usuario e importaremos la clave.

1. Vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add a Data Source]**.
1. Haga clic en el `PostgreSQL` icono.
1. Después de la `PostgreSQL credentials` se abre la página, establezca la variable `Encrypted` alternar a `Yes`. Se mostrará la variable `SSH` formulario de configuración.
1. La variable `public key` se encuentra debajo de este formulario.

Deje esta página abierta a lo largo del tutorial: la necesitará en la siguiente sección y al final.

Si está un poco perdido, así es como navegar [!DNL MBI] para recuperar la clave:

![Recuperación de la clave pública RJMetrics](../../../assets/get-mbi-public-key.gif)

## Permita el acceso al [!DNL MBI] Dirección IP {#allowlist}

Para que la conexión sea correcta, debe configurar el cortafuegos para permitir el acceso desde nuestra dirección IP. es `54.88.76.97/32`, pero también se encuentra en el `PostgreSQL` credenciales . ¿Ves la caja azul en el GIF de arriba? ¡Eso es!

## Creación de `Linux` usuario para [!DNL MBI] {#linux}

Puede tratarse de un equipo de producción o de un equipo secundario, siempre que contenga datos en tiempo real (o que se actualicen con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) como desee, siempre y cuando mantenga el derecho a conectarse al servidor PostgreSQL.

1. Para agregar el nuevo usuario, ejecute los siguientes comandos como root en su `Linux` servidor:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Recuerde `public key` ¿recuperamos en la primera sección? Para garantizar que el usuario tenga acceso a la base de datos, es necesario importar la clave en `authorized\_keys`.

   Copie toda la clave en el `authorized\_keys` como se indica a continuación:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Para terminar de crear el usuario, modifique los permisos en la `/home/rjmetric` para permitir el acceso mediante `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` El archivo asociado con el servidor no está establecido en la opción predeterminada, solo algunos usuarios tendrán acceso al servidor, lo que impide que la conexión a [!DNL MBI]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir al usuario de rjmetric acceder al servidor.

## Creación de [!DNL MBI] Usuario de Postgres {#postgres}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando se inicia sesión en Postgres como usuario con el derecho de conceder privilegios. El usuario también debe ser propietario del esquema que [!DNL MBI] se le concede acceso a.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Reemplazar `secure password` con su propia contraseña segura, que puede ser diferente a la contraseña SSH. Además, asegúrese de reemplazar `database name` y `schema name` con los nombres adecuados en la base de datos.

Si desea conectar varias bases de datos o esquemas, repita este proceso según sea necesario.

## Introducción de la conexión y la información del usuario en [!DNL MBI] {#finish}

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Dejó abierta la página de credenciales de PostgreSQL? Si no es así, vaya a **[!UICONTROL Manage Data > Connections]** y haga clic en **[!UICONTROL Add a Data Source]** y, a continuación, el icono PostgreSQL. No olvide configurar la variable `Encrypted` alternar a `Yes`.

Introduzca la siguiente información en esta página, empezando por la sección Conexión a la base de datos:

* `Username`: El nombre de usuario de RJMetrics Postgres (debe ser rjmetric)
* `Password`: La contraseña de RJMetrics Postgres
* `Port`: Puerto PostgreSQL en el servidor (5432 de forma predeterminada)
* `Host`: 127.0.0.1

En `SSH Connection`:

* `Remote Address`: La dirección IP o el nombre de host del servidor en el que SSH
* `Username`: Nuestro nombre de inicio de sesión SSH (debe ser rjmetric)
* `SSH Port`: Puerto SSH en el servidor (22 de forma predeterminada)

¡Eso es! Cuando haya terminado, haga clic en **Guardar y probar** para completar la configuración.

### Relacionado

* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
