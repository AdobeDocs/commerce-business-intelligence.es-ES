---
title: Conectando  [!DNL MySQL] a través del túnel SSH
description: Aprenda a conectar  [!DNL MySQL] mediante el túnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Conectar [!DNL MySQL] a través de [!DNL SSH Tunnel]

* [Recuperar la clave pública  [!DNL Commerce Intelligence] ](#retrieve)
* [Permitir el acceso a la dirección IP  [!DNL Commerce Intelligence] ](#allowlist)
* [Crear un usuario Linux para  [!DNL Commerce Intelligence]](#linux)
* [Crear un [!DNL MySQL] usuario para [!DNL Commerce Intelligence]](#mysql)
* [Escriba la conexión y la información de usuario en  [!DNL Commerce Intelligence]](#finish)

## SALTAR A

* [[!DNL MySQL] mediante ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] a través de  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Para conectar la base de datos [!DNL MySQL] a [!DNL Commerce Intelligence] a través de un `SSH tunnel`, debe hacer algunas cosas:

1. Recuperar [!DNL Commerce Intelligence] `public key`
1. Permitir acceso a [!DNL Commerce Intelligence] `IP address`
1. Crear un usuario `Linux` para [!DNL Commerce Intelligence]
1. Crear un usuario `MySQL` para [!DNL Commerce Intelligence]
1. Escriba la conexión y la información de usuario en [!DNL Commerce Intelligence]


## Recuperando la clave pública [!DNL Commerce Intelligence] {#retrieve}

`public key` se usa para autorizar al usuario [!DNL Commerce Intelligence] `Linux`. En la siguiente sección, creará el usuario e importará la clave.

1. Vaya a **[!UICONTROL Manage Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en el icono `MySQL`.
1. Una vez abierta la página `MySQL credentials`, establezca la opción `Encrypted` en `Yes`. Esto muestra el formulario de configuración SSH.
1. `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

A continuación se indica cómo navegar por [!DNL Commerce Intelligence] para recuperar la clave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Permitir acceso a la dirección IP [!DNL Commerce Intelligence] {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentran en la página `MySQL credentials`. Consulte el cuadro azul en el GIF de arriba.

## Creando un usuario [!DNL Linux] para [!DNL Commerce Intelligence] {#linux}

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede [restringir este usuario](../../../administrator/account-management/restrict-db-access.md) como desee, siempre y cuando conserve el derecho de conectarse al servidor `MySQL`.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Si el archivo de `sshd\_config` asociado con el servidor no está establecido en la opción predeterminada, sólo determinados usuarios tienen acceso al servidor, lo que impide que la conexión a [!DNL Commerce Intelligence] se realice correctamente. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que el usuario `rjmetric` tenga acceso al servidor.

## Creando un usuario [!DNL MySQL] para [!DNL Commerce Intelligence] {#mysql}

Su organización puede requerir un proceso diferente, pero la forma más sencilla de crear este usuario es ejecutar la siguiente consulta cuando se inicia sesión en [!DNL MySQL] como usuario con derecho a conceder privilegios:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Reemplazar `secure password here` con una contraseña segura, que puede ser diferente a la contraseña de `SSH`.

Para restringir el acceso de este usuario a datos en bases de datos, tablas o columnas específicas, puede ejecutar consultas GRANT que sólo permitan el acceso a los datos permitidos.

## Introduciendo la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página `MySQL credentials`? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego en el icono [!DNL MySQL]. No olvide establecer la opción `Encrypted` en `Yes`.

Escriba la siguiente información en esta página, empezando por la sección `Database Connection`:

* `Username`: el nombre de usuario para el usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: la contraseña del usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: puerto [!DNL MySQL] en el servidor (3306 de forma predeterminada)
* `Host` De forma predeterminada, este es localhost. En general, es el valor de dirección de enlace del servidor [!DNL MySQL], que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

  El valor se encuentra en el archivo `my.cnf` (ubicado en `/etc/my.cnf`) debajo de la línea que dice `\[mysqld\]`. Si la línea de dirección de enlace está comentada en ese archivo, el servidor está protegido frente a intentos de conexión externos.

En la sección `SSH Connection`:

* `Remote Address`: la dirección IP o el nombre de host del servidor [!DNL Commerce Intelligence] se conectará mediante túnel a
* `Username`: el nombre de usuario para el usuario SSH [!DNL Commerce Intelligence] ([!DNL Linux])
* `SSH Port`: puerto SSH en el servidor (22 de forma predeterminada)

Cuando termine, haga clic en **[!UICONTROL Save & Test]** para completar la instalación.

## Relacionado:

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
