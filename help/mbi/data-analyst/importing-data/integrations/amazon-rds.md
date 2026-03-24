---
title: Conectar Amazon RDS
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KAjnETtFvi9EHUDY8SJ-TSEhP3zooQel5ZlN-E3QxIg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 0%

---

# Conectar [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] es un servicio de base de datos administrada que se ejecuta en motores de base de datos con los que probablemente ya esté familiarizado:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

Los pasos para conectar su instancia de [!DNL RDS] varían, según el tipo de base de datos que esté usando y si está usando una conexión cifrada (como una [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), pero aquí están los conceptos básicos.

## Autorizar a [!DNL Commerce Intelligence] para acceder a su base de datos

En la página de credenciales (**[!UICONTROL Manage Data** > **Integrations]**) de cada base de datos, verá un cuadro que contiene las direcciones IP que debe autorizar para conectar R[!DNL RDS] a [!DNL Commerce Intelligence]: `54.88.76.97` y `34.250.211.151`. Aquí tiene un vistazo a la página de `MySQL credentials`, en la que resaltó el cuadro Dirección IP:

![Configuración del grupo de seguridad de Amazon RDS que muestra la configuración de la dirección IP](../../../assets/RDS_IP.png)

Para que [!DNL Commerce Intelligence] se conecte correctamente con su instancia de [!DNL RDS], debe agregar estas direcciones IP al grupo de seguridad de base de datos apropiado a través de la consola de administración de AWS. Estas direcciones IP se pueden agregar a un grupo existente o puede crear una. Lo importante es que el grupo tenga autorización para acceder a la instancia a la que desea conectarse [!DNL Commerce Intelligence].

Al agregar las [!DNL Commerce Intelligence] direcciones IP, asegúrese de agregar `/32` al final de la dirección para indicar a [!DNL Amazon] que se trata de una dirección IP exacta. No se preocupe; la interfaz de AWS deja claro que es necesario.

## Crear un usuario `Linux` para [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Este paso solo es necesario si utiliza una conexión cifrada. Para obtener instrucciones sobre cómo hacerlo, consulte el tema de configuración de la base de datos que está utilizando (por ejemplo: MySQL). El usuario `Linux` nos permite crear un `SSH tunnel`, que es el método más seguro de enviar datos a través de Internet.

## Crear un usuario de base de datos para [!DNL Commerce Intelligence]

Esta es la parte del proceso en la que, según la base de datos que utilice, los pasos varían. La idea es la misma, sin embargo, usted crea un usuario para [!DNL Commerce Intelligence] que se utiliza para acceder a su base de datos. Las instrucciones para crear un usuario de base de datos [!DNL Commerce Intelligence] se encuentran en el tema de configuración de la base de datos que está utilizando.

## Escriba la información de conexión en [!DNL Commerce Intelligence]

Después de conceder a [!DNL Commerce Intelligence] acceso a su instancia y crear un usuario para nosotros, lo último que debe hacer es escribir la información de conexión en [!DNL Commerce Intelligence].

Se tiene acceso a las páginas de credenciales de `MySQL`, `Microsoft SQL` y `PostgreSQL` a través de la página `Integrations` (**[!UICONTROL Manage Data** > **Integrations]**) haciendo clic en **[!UICONTROL Add Integration]**. Cuando se muestre la lista de integraciones, haga clic en el icono de la base de datos que está utilizando para ir a la página de credenciales. Si actualmente no tiene acceso a la integración que necesita, póngase en contacto con su equipo de cuenta de Adobe.

Para terminar de crear la conexión, necesita la siguiente información:

* La dirección pública de su instancia de RDS: Esto se encuentra en la consola de administración de [!DNL AWS].
* El puerto que utiliza la instancia de base de datos: algunas bases de datos tienen un puerto predeterminado, que rellena automáticamente el campo `Port`. Esta información también se encuentra en la documentación de configuración de la base de datos.
* Nombre de usuario y contraseña del usuario que creó para [!DNL Commerce Intelligence].

Si está usando una conexión cifrada, cambie el conmutador `Encrypted` de la página de credenciales de la base de datos a `Yes`. Esto muestra un formulario adicional para configurar el cifrado:

![Formulario de integración de SQL con cifrado habilitado que muestra la opción Yes](../../../assets/sql-integration-encrypted-yes.png)


