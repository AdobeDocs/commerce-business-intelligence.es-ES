---
title: Conectar  [!DNL MongoDB] a través del túnel SSH
description: Aprenda a conectar  [!DNL MongoDB] a través del túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Conectar [!DNL MongoDB] mediante túnel SSH

Para conectar la base de datos [!DNL MongoDB] a [!DNL Commerce Intelligence] a través de un túnel SSH, debe hacer lo siguiente:

1. [Recuperar la clave pública  [!DNL Commerce Intelligence] ](#retrieve)
1. [Permitir el acceso a la dirección IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Creación de un usuario de Linux para Commerce Intelligence](#linux)
1. [Crear un usuario  [!DNL MongoDB] para Commerce Intelligence](#mongodb)
1. [Escriba la conexión y la información de usuario en  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>Debido a la naturaleza técnica de esta configuración, Adobe recomienda que inicie sesión en un desarrollador para que le ayude si no lo ha hecho antes.

## Recuperando la clave pública [!DNL Commerce Intelligence] {#retrieve}

`public key` se usa para autorizar al usuario [!DNL Commerce Intelligence] `Linux`. La siguiente sección le explica cómo crear el usuario e importar las claves.

1. Vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en el icono [!DNL MONGODB].
1. Una vez abierta la página de credenciales de [!DNL MongoDB], cambie el conmutador `Encrypted` a `Yes`. Esto muestra el formulario de configuración SSH.
1. `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

Si se ha perdido un poco, le explicamos cómo navegar por [!DNL Commerce Intelligence] para recuperar la clave:

![Recuperando la clave pública RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permitir acceso a la dirección IP [!DNL Commerce Intelligence] {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentra en la página de credenciales de [!DNL MongoDB]:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creando un usuario `Linux` para [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Si el archivo de `sshd_config` asociado con el servidor no está establecido en la opción predeterminada, sólo determinados usuarios tienen acceso al servidor, lo que impide que la conexión a [!DNL Commerce Intelligence] se realice correctamente. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que el usuario `rjmetric` tenga acceso al servidor.

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede restringir este usuario como desee, siempre y cuando conserve el derecho de conectarse al servidor [!DNL MongoDB].

Para agregar al nuevo usuario, ejecute los siguientes comandos como raíz en el servidor `Linux`:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

¿Recuerda el(la) `public key` que recuperó(ó) en la primera sección? Para asegurarse de que el usuario tiene acceso a la base de datos, debe importar la clave en `authorized_keys`. Copie la clave completa en el archivo `authorized_keys` de la siguiente manera:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para terminar de crear el usuario, modifique los permisos en el directorio /home/rjmetric para permitir el acceso a través de SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creando un usuario [!DNL Commerce Intelligence] [!DNL MongoDB] {#mongodb}

[!DNL MongoDB] servidores tienen dos modos de ejecución: [uno con la opción &quot;auth&quot;](#auth) `(mongod -- auth)` y otro sin [que es el predeterminado](#default). Los pasos para crear un usuario de [!DNL MongoDB] varían según el modo que esté usando el servidor. Asegúrese de verificar el modo antes de continuar.

### Si su servidor usa la opción `Auth`: {#auth}

Al conectarse a varias bases de datos, puede agregar al usuario iniciando sesión en [!DNL MongoDB] como usuario administrador y ejecutando los siguientes comandos.

>[!NOTE]
>
>Para ver todas las bases de datos disponibles, el usuario [!DNL Commerce Intelligence] necesita los permisos para ejecutar `listDatabases.`

Este comando concede al usuario [!DNL Commerce Intelligence] acceso `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Use este comando para conceder al usuario [!DNL Commerce Intelligence] acceso a `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Imprime una respuesta con este aspecto:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Si el servidor utiliza la opción predeterminada {#default}

Si el servidor no usa el modo `auth`, se podrá obtener acceso al servidor [!DNL MongoDB] incluso sin un nombre de usuario y una contraseña. Sin embargo, debe asegurarse de que el archivo `mongodb.conf` `(/etc/mongodb.conf)` tenga las líneas siguientes; de lo contrario, reinicie el servidor después de agregarlas.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para enlazar su servidor [!DNL MongoDB] a una dirección diferente, ajuste el nombre de host de la base de datos en el paso siguiente en consecuencia.

## Introduciendo la conexión y la información de usuario en [!DNL Commerce Intelligence] {#finish}

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página de credenciales de [!DNL MongoDB]? Si no es así, vaya a **[!UICONTROL Data > Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego en el icono [!DNL MongoDB]. No olvide cambiar la opción `Encrypted` a `Yes`.

Escriba la siguiente información en esta página, empezando por la sección `Database Connection`:

* `Host`: `127.0.0.1`
* `Username`: el nombre de usuario [!DNL Commerce Intelligence] [!DNL MongoDB] (debe ser `rjmetric`)
* `Password`: la contraseña de [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port`: puerto de MongoDB en el servidor (`27017` de forma predeterminada)
* `Database Name` (opcional): si solo permitió el acceso a una base de datos, especifique el nombre de la base de datos aquí.

En la sección `SSH Connection`:

* `Remote Address`: la dirección IP o el nombre de host del servidor en el que se SSH
* `Username`: el nombre de usuario de Linux (SSH) [!DNL Commerce Intelligence] (debe ser rjmetric)
* `SSH Port`: el puerto SSH del servidor (22 de forma predeterminada)

Cuando termine, haga clic en **[!UICONTROL Save Test]** para completar la instalación.

### Relacionado

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
