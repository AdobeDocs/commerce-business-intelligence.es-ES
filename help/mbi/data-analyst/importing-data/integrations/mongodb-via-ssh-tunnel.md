---
title: Connect [!DNL MongoDB] a través del túnel SSH
description: Aprenda a conectar [!DNL MongoDB] a través del túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Connect [!DNL MongoDB] a través del túnel SSH


Para conectar su [!DNL MongoDB] a [!DNL MBI] a través de un túnel SSH, usted (o su equipo, si no es un técnico) tendrá que hacer algunas cosas:

1. [Recupere el [!DNL MBI] clave pública](#retrieve)
1. [Permita el acceso al [!DNL MBI] Dirección IP](#allowlist)
1. [Crear un usuario de Linux para MBI](#linux)
1. [Cree un [!DNL MongoDB] usuario para MBI](#mongodb)
1. [Introduzca la conexión y la información de usuario en [!DNL MBI]](#finish)

>[!NOTE]
>
>Debido a la naturaleza técnica de esta configuración, le sugerimos realizar un bucle en un desarrollador para ayudar si no lo ha hecho antes.

## Recuperación de la variable [!DNL MBI] clave pública {#retrieve}

La variable `public key` se usa para autorizar la variable [!DNL MBI] `Linux` usuario. En la siguiente sección, creamos el usuario e importamos la clave.

1. Vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en el [!DNL MONGODB] icono.
1. Después de la [!DNL MongoDB] se abre la página de credenciales, cambie la `Encrypted` alternar a `Yes`. Se mostrará el formulario de configuración de SSH.
1. La variable `public key` se encuentra debajo de este formulario.

Deje esta página abierta a lo largo del tutorial: la necesitará en la siguiente sección y al final.

Si está un poco perdido, aquí está cómo navegar [!DNL MBI] para recuperar la clave:

![Recuperación de la clave pública RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permita el acceso al [!DNL MBI] Dirección IP {#allowlist}

Para que la conexión sea correcta, debe configurar el cortafuegos para permitir el acceso desde nuestras direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentra en el [!DNL MongoDB] página de credenciales:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creación de `Linux` usuario para [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Si la variable `sshd_config` El archivo asociado con el servidor no está establecido en la opción predeterminada, solo algunos usuarios tendrán acceso al servidor, lo que impide que la conexión a [!DNL MBI]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir que `rjmetric` acceso del usuario al servidor.

Puede tratarse de un equipo de producción o de un equipo secundario, siempre que contenga datos en tiempo real (o que se actualicen con frecuencia). Puede restringir este usuario de cualquier manera que desee siempre y cuando mantenga el derecho de conexión con la variable [!DNL MongoDB] servidor.

Para agregar el nuevo usuario, ejecute los siguientes comandos como root en su `Linux` servidor:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Recuerde `public key` ¿recuperamos en la primera sección? Para garantizar que el usuario tenga acceso a la base de datos, es necesario importar la clave en `authorized_keys`. Copie toda la clave en el `authorized_keys` como se indica a continuación:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para terminar de crear el usuario, modifique los permisos en el directorio /home/rjmetric para permitir el acceso a través de SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creación de [!DNL MBI] [!DNL MongoDB] usuario {#mongodb}

[!DNL MongoDB] los servidores tienen dos modos de ejecución: [uno con la opción &quot;auth&quot;](#auth) `(mongod -- auth)` y una sin, [que es el valor predeterminado](#default). Los pasos para crear una [!DNL MongoDB] variará un poco dependiendo del modo que utilice su servidor, por lo que asegúrese de comprobar el modo antes de continuar.

### Si su servidor utiliza la variable `Auth` Opción: {#auth}

Al conectarse a varias bases de datos, puede agregar el usuario iniciando sesión en [!DNL MongoDB] como usuario administrador y ejecutando los siguientes comandos.

>[!NOTE]
>
>Para ver todas las bases de datos disponibles, la variable [!DNL MBI] El usuario requiere los permisos para ejecutar `listDatabases.`

Este comando otorgará la variable [!DNL MBI] acceso de usuario `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilice este comando para conceder la variable [!DNL MBI] acceso de usuario `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Así se imprimirá una respuesta similar a la siguiente:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Si el servidor utiliza la opción predeterminada {#default}

Si su servidor no utiliza `auth` el modo [!DNL MongoDB] servidor seguirá siendo accesible incluso sin un nombre de usuario y contraseña. Sin embargo, debe asegurarse de que la variable `mongodb.conf` file `(/etc/mongodb.conf)` tiene las siguientes líneas: si no, reinicie el servidor después de agregarlo.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para enlazar su [!DNL MongoDB] servidor a una dirección diferente, ajuste el nombre de host de la base de datos en el siguiente paso en consecuencia.

## Introducción de la conexión y la información del usuario en [!DNL MBI] {#finish}

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Dejaste el [!DNL MongoDB] ¿se abre la página de credenciales? Si no es así, vaya a **[!UICONTROL Data > Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego la variable [!DNL MongoDB] icono. no olvide cambiar la variable `Encrypted` alternar a `Yes`.

Introduzca la siguiente información en esta página, empezando por el `Database Connection` sección:

* `Host`: `127.0.0.1`
* `Username`: La variable [!DNL MBI] [!DNL MongoDB] username (debe `rjmetric`)
* `Password`: La variable [!DNL MBI] [!DNL MongoDB] password
* `Port`: Puerto de MongoDB en su servidor (`27017` de forma predeterminada)
* `Database Name` (Opcional): Si solo ha permitido el acceso a una base de datos, especifique aquí el nombre de esa base de datos.

En el `SSH Connection` sección:

* `Remote Address`: La dirección IP o el nombre de host del servidor en el que SSH
* `Username`: La variable [!DNL MBI] Nombre de usuario de Linux (SSH) (debe ser rjmetric)
* `SSH Port`: El puerto SSH del servidor (22 de forma predeterminada)

¡Eso es! Cuando haya terminado, haga clic en **[!UICONTROL Save Test]** para completar la configuración.

### Relacionado

* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
