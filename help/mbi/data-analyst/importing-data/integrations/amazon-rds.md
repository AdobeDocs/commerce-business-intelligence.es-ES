---
title: Conectar Amazon RDS
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Conectar Amazon RDS

Amazon Relational Database Services (RDS) es un servicio de base de datos administrada que se ejecuta en motores de base de datos con los que probablemente ya esté familiarizado: [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft® SQL]](../integrations/microsoft-sql-server.md), y [[!DNL PostgreSQ]](../integrations/postgresql.md).

Los pasos para conectar la instancia de RDS varían, según el tipo de base de datos que utilice y si está utilizando una conexión cifrada (como un [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), pero estos son los conceptos básicos:

## Autorizar [!DNL MBI] para acceder a la base de datos

En la página de credenciales (**[!UICONTROL Manage Data** > **Integrations]**) para cada base de datos, verá un cuadro que contiene las direcciones IP que debe autorizar para conectar RDS a MBI: `54.88.76.97` y `34.250.211.151`. Aquí tiene un vistazo a la `MySQL credentials` , donde resaltó el cuadro Dirección IP:

![](../../../assets/RDS_IP.png)

Para [!DNL MBI] para conectarse correctamente con la instancia de RDS, debe agregar estas direcciones IP al grupo de seguridad de base de datos correspondiente a través de la consola de administración de AWS. Estas direcciones IP se pueden añadir a un grupo existente o puede crear una. Lo importante es que el grupo esté autorizado para acceder a la instancia a la que desea conectarse [!DNL MBI].

Al añadir la variable [!DNL MBI] Direcciones IP, asegúrese de añadir una `/32` al final de la dirección para indicar a Amazon que es una dirección IP exacta. No se preocupe; la interfaz de AWS deja claro que es necesario.

## Crear un `Linux` usuario para [!DNL MBI] {#linux}

>[!NOTE]
>
>Este paso solo es necesario si utiliza una conexión cifrada. Para obtener instrucciones sobre cómo hacerlo, consulte el artículo de configuración de la base de datos que está utilizando (por ejemplo: MySQL). El `Linux` El usuario nos permite crear un `SSH tunnel`, que es el método más seguro de envío de datos a través de Internet.

## Crear un usuario de base de datos para MBI

Esta es la parte del proceso en la que, según la base de datos que utilice, los pasos varían. La idea es la misma: se crea un usuario para [!DNL MBI] que se utiliza para acceder a la base de datos. Instrucciones para crear una base de datos [!DNL MBI] El usuario se encuentra en el artículo de configuración de la base de datos que está utilizando.

## Introducir información de conexión en MBI

Después de conceder [!DNL MBI] acceder a su instancia y crear un usuario para nosotros, lo último que debe hacer es introducir la información de conexión en [!DNL MBI].

Las páginas de credenciales para `MySQL`, `Microsoft SQL`, y `PostgreSQL` se accede a través de la `Integrations` página (**[!UICONTROL Manage Data** > **Integrations]**) haciendo clic en **[!UICONTROL Add Integration]**. Cuando se muestre la lista de integraciones, haga clic en el icono de la base de datos que está utilizando para ir a la página de credenciales. Si actualmente no tiene acceso a la integración que necesita, póngase en contacto con el equipo de cuenta de Adobe.

Para terminar de crear la conexión, necesita la siguiente información:

* La dirección pública de la instancia de RDS: Esto se puede encontrar en la consola de administración de AWS.
* El puerto que utiliza la instancia de base de datos: Algunas bases de datos tienen un puerto predeterminado, que rellena automáticamente la variable `Port` field. Esta información también se encuentra en la documentación de configuración de la base de datos.
* Nombre de usuario y contraseña del usuario que ha creado para [!DNL MBI].

Si utiliza una conexión cifrada, cambie el `Encrypted` active la página credenciales de la base de datos para `Yes`. Esto muestra un formulario adicional para configurar el cifrado:

![](../../../assets/sql-integration-encrypted-yes.png)

¡Eso es todo lo que hay! Se ha completado la conexión de la instancia de RDS.
