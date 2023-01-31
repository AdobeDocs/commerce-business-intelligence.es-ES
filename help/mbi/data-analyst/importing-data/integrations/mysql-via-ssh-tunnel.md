---
title: Conexión de MySQL a través del túnel SSH
description: Aprenda a conectar MySQL a través del túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Connect `MySQL` via `SSH Tunnel`

* [Recupere el [!DNL MBI] clave pública](#retrieve)
* [Permita el acceso al [!DNL MBI] Dirección IP](#allowlist)
* [Crear un usuario de Linux para [!DNL MBI]](#linux)
* [Crear un usuario de MySQL para [!DNL MBI]](#mysql)
* [Introduzca la conexión y la información de usuario en [!DNL MBI]](#finish)

## SALTAR A

* `MySQL via SSH tunnel`
* [`MySQL`](../integrations/mysql-via-a-direct-connection.md)
* [`MySQL`](../integrations/mysql-via-cpanel.md)

Para conectar su `MySQL` a [!DNL MBI] mediante una `SSH tunnel`, usted (o su equipo, si no es técnico) tendrá que hacer algunas cosas:

1. Recupere el [!DNL MBI] `public key`
1. Permita el acceso al [!DNL MBI] `IP address`
1. Cree un `Linux` usuario para [!DNL MBI]
1. Cree un `MySQL` usuario para [!DNL MBI]
1. Introduzca la conexión y la información de usuario en [!DNL MBI]

No es tan complicado como podría sonar. Empecemos.

## Recuperación de la variable [!DNL MBI] clave pública {#retrieve}

La variable `public key` se usa para autorizar la variable [!DNL MBI] `Linux` usuario. En la siguiente sección, crearemos el usuario e importaremos la clave.

1. Vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en el `MySQL` icono.
1. Después de la `MySQL credentials` se abre la página, establezca la variable `Encrypted` alternar a `Yes`. Se mostrará el formulario de configuración de SSH.
1. La variable `public key` se encuentra debajo de este formulario.

Deje esta página abierta a lo largo del tutorial: la necesitará en la siguiente sección y al final.

Si está un poco perdido, así es como navegar [!DNL MBI] para recuperar la clave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permita el acceso al [!DNL MBI] Dirección IP {#allowlist}

Para que la conexión sea correcta, debe configurar el cortafuegos para permitir el acceso desde nuestras direcciones IP. Son `54.88.76.97` y `34.250.211.151` pero también están en el `MySQL credentials` página. ¿Ves la caja azul en el GIF de arriba? ¡Eso es!

## Creación de `Linux` usuario para [!DNL MBI] {#linux}

Puede tratarse de un equipo de producción o de un equipo secundario, siempre que contenga datos en tiempo real (o que se actualicen con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) de cualquier forma que desee, siempre y cuando mantenga el derecho de conexión con la variable `MySQL` servidor.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` El archivo asociado con el servidor no está establecido en la opción predeterminada, solo algunos usuarios tendrán acceso al servidor, lo que impide que la conexión a [!DNL MBI]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que `rjmetric` acceso del usuario al servidor.

## Creación de `MySQL` usuario para [!DNL MBI] {#mysql}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando inicie sesión `MySQL` como usuario con derecho a conceder privilegios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Reemplazar `secure password here` con una contraseña segura, que puede ser diferente a la de `SSH` contraseña.

Para impedir que este usuario acceda a datos en bases de datos, tablas o columnas específicas, puede ejecutar consultas GRANT que solo permitan el acceso a los datos que permita.

## Introducción de la conexión y la información del usuario en [!DNL MBI] {#finish}

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Dejaste el `MySQL credentials` apertura de página? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego el icono MySQL. no olvide configurar la variable `Encrypted` alternar a `Yes`.

Introduzca la siguiente información en esta página, empezando por la sección Conexión a la base de datos:

* `Username`: El nombre de usuario de la variable [!DNL MBI] Usuario MySQL
* `Password`: La contraseña de la variable [!DNL MBI] Usuario MySQL
* `Port`: Puerto de MySQL en su servidor (3306 por defecto)
* `Host` De forma predeterminada, será localhost. En general, será el valor de la dirección de enlace para su servidor MySQL, que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

   El valor se puede encontrar en su `my.cnf` archivo (normalmente se encuentra en `/etc/my.cnf`) debajo de la línea que dice: `\[mysqld\]`. Si la línea bind-address está comentada en ese archivo, el servidor está protegido de los intentos de conexión externos.

En el `SSH Connection` sección:

* `Remote Address`: La dirección IP o el nombre de host del servidor [!DNL MBI] entrarán en el túnel
* `Username`: El nombre de usuario de la variable [!DNL MBI] Usuario SSH (Linux)
* `SSH Port`: Puerto SSH en el servidor (22 de forma predeterminada)

¡Eso es! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Relacionado:

* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
