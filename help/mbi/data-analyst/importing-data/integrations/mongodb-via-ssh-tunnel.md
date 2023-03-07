---
title: Connect [!DNL MongoDB] a través del túnel SSH
description: Obtenga información sobre cómo conectarse [!DNL MongoDB] vía túnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Connect [!DNL MongoDB] a través del túnel SSH

Para conectar su [!DNL MongoDB] base de datos a [!DNL MBI] a través de un túnel SSH, usted (o su equipo, si no es un técnico) debe hacer algunas cosas:

1. [Recupere el [!DNL MBI] clave pública](#retrieve)
1. [Permitir el acceso al [!DNL MBI] Dirección IP](#allowlist)
1. [Crear un Linux](#linux)
1. [Crear un [!DNL MongoDB] usuario para MBI](#mongodb)
1. [Introduzca la conexión y la información de usuario en [!DNL MBI]](#finish)

>[!NOTE]
>
>Debido a la naturaleza técnica de esta configuración, Adobe recomienda que inicie sesión en un desarrollador para que le ayude si no lo ha hecho antes.

## Recuperación del [!DNL MBI] clave pública {#retrieve}

El `public key` se utiliza para autorizar la [!DNL MBI] `Linux` usuario. La siguiente sección le explica cómo crear el usuario e importar las claves.

1. Ir a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**.
1. Haga clic en [!DNL MONGODB] icono.
1. Después del [!DNL MongoDB] Si se abre la página credenciales, cambie el `Encrypted` cambiar a `Yes`. Esto muestra el formulario de configuración SSH.
1. El `public key` se encuentra debajo de este formulario.

Deje esta página abierta durante todo el tutorial, la necesitará en la siguiente sección y al final.

Si está un poco perdido, así es como navegar [!DNL MBI] para recuperar la clave:

![Recuperación de la clave pública de RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Permitir el acceso al [!DNL MBI] Dirección IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Lo son `54.88.76.97` y `34.250.211.151`, pero también está en la [!DNL MongoDB] página credenciales:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creación de un `Linux` usuario para [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Si la variable `sshd_config` el archivo asociado con el servidor no está establecido en la opción predeterminada, solo determinados usuarios tienen acceso al servidor; esto impide una conexión correcta a [!DNL MBI]. En estos casos, es necesario ejecutar un comando como `AllowUsers` para permitir el `rjmetric` acceso del usuario al servidor.

Puede ser una máquina de producción o secundaria, siempre que contenga datos en tiempo real (o actualizados con frecuencia). Puede restringir a este usuario de la forma que desee, siempre y cuando conserve el derecho de conectarse a [!DNL MongoDB] servidor.

Para agregar al nuevo usuario, ejecute los siguientes comandos como raíz en su `Linux` servidor:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Recuerde la `public key` ¿la recuperó en la primera sección? Para garantizar que el usuario tenga acceso a la base de datos, debe importar la clave en `authorized_keys`. Copie la clave completa en el `authorized_keys` como se indica a continuación:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Para terminar de crear el usuario, modifique los permisos en el directorio /home/rjmetric para permitir el acceso a través de SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creación de un [!DNL MBI] [!DNL MongoDB] usuario {#mongodb}

[!DNL MongoDB] Los servidores de tienen dos modos de ejecución: [uno con la opción &quot;auth&quot;](#auth) `(mongod -- auth)` y uno sin él, [que es la opción predeterminada](#default). Los pasos para crear un [!DNL MongoDB] El usuario varía en función del modo que utilice el servidor. Asegúrese de verificar el modo antes de continuar.

### Si el servidor utiliza el `Auth` Opción: {#auth}

Al conectarse a varias bases de datos, puede agregar el usuario iniciando sesión en [!DNL MongoDB] como usuario administrador y ejecutando los siguientes comandos.

>[!NOTE]
>
>Para ver todas las bases de datos disponibles, la variable [!DNL MBI] El usuario de requiere los permisos para ejecutar `listDatabases.`

Este comando concede a [!DNL MBI] acceso de usuario `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilice este comando para conceder el [!DNL MBI] acceso de usuario `to a single database`:

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

Si el servidor no utiliza `auth` modo, su [!DNL MongoDB] el servidor es accesible incluso sin un nombre de usuario y una contraseña. Sin embargo, debe asegurarse de que `mongodb.conf` archivo `(/etc/mongodb.conf)` tiene las siguientes líneas: si no es así, reinicie el servidor después de agregarlas.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Para enlazar su [!DNL MongoDB] servidor a una dirección diferente, ajuste el nombre de host de la base de datos en el siguiente paso en consecuencia.

## Introducción de la conexión y la información de usuario en [!DNL MBI] {#finish}

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL MBI]. ¿Dejaste el [!DNL MongoDB] ¿desea abrir la página credenciales? Si no es así, vaya a **[!UICONTROL Data > Connections]** y haga clic en **[!UICONTROL Add New Data Source]** y, a continuación, el [!DNL MongoDB] icono. No olvide cambiar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Host`: `127.0.0.1`
* `Username`: La [!DNL MBI] [!DNL MongoDB] nombre de usuario (debe ser `rjmetric`)
* `Password`: La [!DNL MBI] [!DNL MongoDB] contraseña
* `Port`: Puerto de MongoDB en el servidor (`27017` de forma predeterminada)
* `Database Name` (Opcional): Si solo ha permitido el acceso a una base de datos, especifique el nombre de la base de datos aquí.

En el `SSH Connection` sección:

* `Remote Address`: La dirección IP o el nombre de host del servidor en el que se SSH
* `Username`: La [!DNL MBI] Nombre de usuario de Linux® (SSH) (debe ser rjmetric)
* `SSH Port`: el puerto SSH del servidor (22 de forma predeterminada)

¡Eso es todo! Cuando haya terminado, haga clic en **[!UICONTROL Save Test]** para completar la configuración.

### Relacionado

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
