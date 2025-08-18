---
title: Conexión de MySQL mediante una conexión directa
description: Aprenda a conectar [!DNL MongoDB] mediante conexión directa.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Conectar [!DNL MySQL] mediante conexión directa

## En este tema

* [Permitir el acceso a la dirección IP  [!DNL Commerce Intelligence] ](#allowlist)
* [Crear un [!DNL MySQL] usuario para [!DNL Commerce Intelligence]](#steptwo)
* [Escriba la información de conexión en  [!DNL Commerce Intelligence]](#stepthree)

## Saltar a

* [[!DNL MySQL] mediante ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] a través de  [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] recomienda que uses [SSH](../integrations/mysql-via-ssh-tunnel.md) o algún otro tipo de cifrado para proteger tus datos. Si no se trata de una opción, aún puede conectar directamente [!DNL Commerce Intelligence] a la base de datos siguiendo las instrucciones de este tema.

En este tema se explica cómo conectar directamente la base de datos de [!DNL MySQL] con [!DNL Commerce Intelligence]. Esta configuración también se puede usar con [!DNL Adobe Commerce] o con cualquier otra base de datos de comercio electrónico que use MySQL.

## Permitir acceso a las [!DNL Commerce Intelligence] direcciones IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también se encuentra en la página de credenciales de [!DNL MySQL]:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Crear un usuario [!DNL MySQL] para [!DNL Commerce Intelligence]

La forma más sencilla de crear un usuario de `MySQL` para [!DNL Commerce Intelligence] es ejecutar la siguiente consulta al iniciar sesión en `MySQL` con privilegios de `GRANT`. Reemplace `Commerce Intelligence IP Address` por la dirección IP [!DNL Commerce Intelligence] y reemplace `secure password` por una contraseña segura de su elección:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Para restringir el acceso de este usuario a datos en bases de datos, tablas o columnas específicas, puede ejecutar `GRANT` consultas que solo permitan el acceso a los datos permitidos.

**Vuelva a ejecutar la consulta GRANT para todas las direcciones IP necesarias utilizando el mismo usuario y contraseña.**

## Introducir información de conexión en Commerce Intelligence

Para finalizar, debe especificar la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejó abierta la página de credenciales de [!DNL MySQL]? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**; a continuación, haga clic en el icono [!DNL MySQL]. No olvide cambiar la opción `Encrypted` a `Yes`.

Escriba la siguiente información en esta página, empezando por la sección `Database Connection`:

* `Connection Nickname`: escriba un nombre para la integración (por ejemplo, Tienda electrónica)
* `Username`: el nombre de usuario para el usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: la contraseña del usuario [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: de forma predeterminada, es localhost. En general, es el valor de dirección de enlace del servidor [!DNL MySQL], que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

  El valor se encuentra en el archivo `my.cnf` (ubicado en `/etc/my.cnf`) debajo de la línea que dice `\[mysqld\]`. Si la línea de dirección de enlace está comentada en ese archivo, el servidor está protegido frente a intentos de conexión externos.

Cuando termine, haga clic en **[!UICONTROL Save & Test]** para completar la instalación.

## Documentación relacionada

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
