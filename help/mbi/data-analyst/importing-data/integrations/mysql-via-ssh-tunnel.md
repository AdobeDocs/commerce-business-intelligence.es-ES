---
title: Conectando [!DNL MySQL] a través del túnel SSH
description: Obtenga información sobre cómo conectarse [!DNL MySQL] a través del túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Connect [!DNL MySQL] mediante [!DNL SSH Tunnel]

* [Recupere el [!DNL Commerce Intelligence] clave pública](#retrieve)
* [Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP](#allowlist)
* [Crear un usuario de Linux para [!DNL Commerce Intelligence]](#linux)
* [Crear un [!DNL MySQL] usuario para [!DNL Commerce Intelligence]](#mysql)
* [Introduzca la conexión y la información de usuario en [!DNL Commerce Intelligence]](#finish)

## SALTAR A

* [[!DNL MySQL] mediante ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] mediante [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Para conectar su [!DNL MySQL] base de datos a [!DNL Commerce Intelligence] mediante un `SSH tunnel`, debe hacer algunas cosas:

1. Recupere el [!DNL Commerce Intelligence] `public key`
1. Permitir el acceso al [!DNL Commerce Intelligence] `IP address`
1. Crear un `Linux` usuario para [!DNL Commerce Intelligence]
1. Crear un `MySQL` usuario para [!DNL Commerce Intelligence]
1. Introduzca la conexión y la información de usuario en [!DNL Commerce Intelligence]


## Recuperación del [!DNL Commerce Intelligence] clave pública {#retrieve}

El `public key` se utiliza para autorizar la [!DNL Commerce Intelligence] `Linux` usuario. En la siguiente sección, creará el usuario e importará la clave.

1. Ir a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en `MySQL` icono.
1. Después del `MySQL credentials` se abre la página, configure el `Encrypted` cambiar a `Yes`. Esto muestra el formulario de configuración SSH.
1. El `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

A continuación se muestra cómo navegar [!DNL Commerce Intelligence] para recuperar la clave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Lo son `54.88.76.97` y `34.250.211.151` pero también están en el `MySQL credentials` página. Consulte el cuadro azul en el GIF de arriba.

## Creación de un [!DNL Linux] usuario para [!DNL Commerce Intelligence] {#linux}

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) de cualquier manera que desee, siempre y cuando conserve el derecho de conectarse al `MySQL` servidor.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Si la variable `sshd\_config` el archivo asociado con el servidor no está establecido en la opción predeterminada, solo determinados usuarios tienen acceso al servidor; esto impide una conexión correcta a [!DNL Commerce Intelligence]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir el `rjmetric` acceso del usuario al servidor.

## Creación de un [!DNL MySQL] usuario para [!DNL Commerce Intelligence] {#mysql}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando se inicia sesión en [!DNL MySQL] como usuario con derecho a otorgar privilegios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Reemplazar `secure password here` con una contraseña segura, que puede diferir de la contraseña de `SSH` contraseña.

Para restringir el acceso de este usuario a datos en bases de datos, tablas o columnas específicas, puede ejecutar consultas GRANT que sólo permitan el acceso a los datos permitidos.

## Introducción de la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejaste el `MySQL credentials` ¿página abierta? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]** y, a continuación, el [!DNL MySQL] icono. No olvide configurar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Password`: La contraseña para el [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Port`: [!DNL MySQL] puerto del servidor (3306 de forma predeterminada)
* `Host` De forma predeterminada, es localhost. En general, es el valor de dirección de enlace para su [!DNL MySQL] servidor, que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

   El valor se puede encontrar en su `my.cnf` archivo (ubicado en `/etc/my.cnf`) debajo de la línea que dice `\[mysqld\]`. Si la línea de dirección de enlace está comentada en ese archivo, el servidor está protegido frente a intentos de conexión externos.

En el `SSH Connection` sección:

* `Remote Address`: La dirección IP o el nombre de host del servidor [!DNL Commerce Intelligence] entrará en túnel
* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] SSH ([!DNL Linux]) usuario
* `SSH Port`: Puerto SSH en el servidor (22 de forma predeterminada)

Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Relacionado:

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
