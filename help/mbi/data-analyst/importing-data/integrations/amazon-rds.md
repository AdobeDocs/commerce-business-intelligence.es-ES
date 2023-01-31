---
title: Conectar Amazon RDS
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Conectar Amazon RDS

Amazon Relational Database Services (RDS) es un servicio de base de datos administrada que se ejecuta en motores de base de datos que probablemente ya esté familiarizado con: [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)y [[!DNL PostgreSQ]](../integrations/postgresql.md).

Los pasos para conectar su instancia de RDS varían ligeramente según el tipo de base de datos que esté utilizando (utilice los vínculos anteriores para obtener instrucciones detalladas para cada base de datos) y si está utilizando o no una conexión cifrada (como una [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), pero aquí están los conceptos básicos:

## Autorizar [!DNL MBI] para acceder a la base de datos

En la página de credenciales (**[!UICONTROL Manage Data** > **Integrations]**) para cada base de datos, verá un cuadro que contiene las direcciones IP que deberá autorizar para conectar RDS a MBI: `54.88.76.97` y `34.250.211.151`. Aquí puede ver el `MySQL credentials` , donde resaltamos el cuadro de dirección IP:

![](../../../assets/RDS_IP.png)

Para [!DNL MBI] para conectarse correctamente con la instancia de RDS, deberá agregar estas direcciones IP al grupo de seguridad de base de datos adecuado a través de la consola de administración de AWS. Estas direcciones IP se pueden agregar a un grupo existente o puede crear uno nuevo; lo importante es que el grupo esté autorizado para acceder a la instancia a la que desee conectarse [!DNL MBI].

Al añadir la variable [!DNL MBI] direcciones IP, asegúrese de agregar una `/32` al final de la dirección para indicar a Amazon que es una dirección IP exacta. No se preocupe; la interfaz de AWS dejará claro que esto es necesario.

## Cree un `Linux` usuario para [!DNL MBI] {#linux}

>[!NOTE]
>
>Este paso solo es necesario si utiliza una conexión cifrada. Para obtener instrucciones sobre cómo hacerlo, consulte el artículo de configuración de la base de datos que está utilizando (por ejemplo: MySQL). La variable `Linux` el usuario nos permitirá crear un `SSH tunnel`, que es el método más seguro para enviar datos a través de Internet.

## Crear un usuario de base de datos para MBI

Esta es la parte del proceso en la que, según la base de datos que esté utilizando, los pasos variarán. Sin embargo, la idea es la misma: creará un usuario para [!DNL MBI] que se utilizará para acceder a la base de datos. Instrucciones para crear una base de datos [!DNL MBI] se puede encontrar en el artículo de configuración de la base de datos que está utilizando.

## Introducir información de conexión en MBI

Una vez concedido [!DNL MBI] acceso a su instancia y crear un usuario para nosotros, lo último que debe hacer es introducir la información de conexión en [!DNL MBI].

Las páginas de credenciales de `MySQL`, `Microsoft SQL`y `PostgreSQL` se accede a través de la variable `Integrations` página (**[!UICONTROL Manage Data** > **Integrations]**) haciendo clic en **[!UICONTROL Add Integration]**. Cuando aparezca la lista de integraciones, haga clic en el icono de la base de datos que está utilizando para ir a la página de credenciales. Si actualmente no tiene acceso a la integración que necesita, póngase en contacto con su CSM.

Para terminar de crear la conexión, necesitamos la siguiente información:

* La dirección pública de su instancia de RDS: Esto se puede encontrar en la consola de administración de AWS.
* El puerto que utiliza la instancia de base de datos: Algunas bases de datos tienen un puerto predeterminado, que rellenará automáticamente la variable `Port` campo . Esta información también se encuentra en nuestra documentación de configuración para la base de datos.
* El nombre de usuario y la contraseña del usuario que ha creado para [!DNL MBI].

Si está utilizando una conexión cifrada, cambie la variable `Encrypted` alternar en la página de credenciales de la base de datos a `Yes`. Se mostrará un formulario adicional para configurar el cifrado:

![](../../../assets/sql-integration-encrypted-yes.png)

¡Eso es todo! Se ha completado la conexión de la instancia de RDS.
