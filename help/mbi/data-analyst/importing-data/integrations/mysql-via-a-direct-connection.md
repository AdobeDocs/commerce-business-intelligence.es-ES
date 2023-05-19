---
title: Conexión de MySQL mediante una conexión directa
description: Obtenga información sobre cómo conectarse [!DNL MongoDB] mediante conexión directa.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Connect [!DNL MySQL] mediante conexión directa

## En este tema

* [Permitir el acceso al [!DNL Commerce Intelligence] Dirección IP](#allowlist)
* [Crear un [!DNL MySQL] usuario para [!DNL Commerce Intelligence]](#steptwo)
* [Introducir información de conexión en [!DNL Commerce Intelligence]](#stepthree)

## Saltar a

* [[!DNL MySQL] mediante ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] mediante [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] recomienda utilizar [SSH](../integrations/mysql-via-ssh-tunnel.md) o alguna otra forma de cifrado para proteger sus datos. Si esta no es una opción, aún puede conectarse directamente [!DNL Commerce Intelligence] a la base de datos con las instrucciones de este tema.

Este tema le guiará a través de la conexión directa de [!DNL MySQL] base de datos a [!DNL Commerce Intelligence]. Esta configuración también se puede utilizar con [!DNL Adobe Commerce] o cualquier otra base de datos de comercio electrónico que utilice MySQL.

## Permitir el acceso al [!DNL Commerce Intelligence] Direcciones IP {#allowlist}

Para que la conexión se realice correctamente, debe configurar el cortafuegos para permitir el acceso desde las direcciones IP. Lo son `54.88.76.97` y `34.250.211.151`, pero también está en la [!DNL MySQL] página credenciales:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Crear un [!DNL MySQL] usuario para [!DNL Commerce Intelligence]

La forma más sencilla de crear un `MySQL` usuario para [!DNL Commerce Intelligence] es ejecutar la siguiente consulta cuando se inicia sesión en `MySQL` con `GRANT` privilegios. Reemplazar `Commerce Intelligence IP Address` con el [!DNL Commerce Intelligence] Dirección IP y reemplazar `secure password` con una contraseña segura de su elección:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Para restringir el acceso de este usuario a datos en bases de datos, tablas o columnas específicas, puede ejecutar `GRANT` consultas que solo permiten el acceso a los datos permitidos.

**Vuelva a ejecutar la consulta GRANT para todas las direcciones IP requeridas con el mismo usuario y contraseña.**

## Introducir información de conexión en Commerce Intelligence

Para finalizar, debe introducir la conexión y la información de usuario en [!DNL Commerce Intelligence]. ¿Dejaste el [!DNL MySQL] ¿desea abrir la página credenciales? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego haga clic en [!DNL MySQL] icono. No olvide cambiar el `Encrypted` cambiar a `Yes`.

Introduzca la siguiente información en esta página, empezando por `Database Connection` sección:

* `Connection Nickname`: introduzca un nombre para la integración (por ejemplo, Tienda de comercio electrónico)
* `Username`: El nombre de usuario del [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Password`: La contraseña para el [!DNL Commerce Intelligence] [!DNL MySQL] usuario
* `Port`: el puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: De forma predeterminada, es localhost. En general, es el valor de dirección de enlace para su [!DNL MySQL] servidor, que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

   El valor se puede encontrar en su `my.cnf` archivo (ubicado en `/etc/my.cnf`) debajo de la línea que dice `\[mysqld\]`. Si la línea de dirección de enlace está comentada en ese archivo, el servidor está protegido frente a intentos de conexión externos.

Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Documentación relacionada

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
