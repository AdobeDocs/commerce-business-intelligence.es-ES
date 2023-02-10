---
title: Conexión de MySQL a través de una conexión directa
description: Aprenda a conectar [!DNL MongoDB] mediante conexión directa.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Connect [!DNL MongoDB] mediante conexión directa

## En este artículo

* [Permita el acceso al [!DNL MBI] Dirección IP](#allowlist)
* [Cree un ](#steptwo)
* [Introducir información de conexión en [!DNL MBI]](#stepthree)

## Saltar a

* [`MySQL a través del túnel SSH`](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [`MySQL a través de cPanel`](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Le recomendamos encarecidamente que use [SSH](../integrations/mysql-via-ssh-tunnel.md) o cualquier otra forma de cifrado para proteger sus datos. Si esta no es una opción, aún puede conectarse directamente [!DNL MBI] a la base de datos siguiendo las instrucciones de este artículo.

En este artículo, lo acompañamos a través de la conexión directa de la base de datos MySQL a [!DNL MBI]. Estos ajustes también pueden utilizarse con Commerce o con cualquier otra base de datos de comercio electrónico que utilice MySQL.

## Permita el acceso al [!DNL MBI] Direcciones IP {#allowlist}

Para que la conexión sea correcta, debe configurar el cortafuegos para permitir el acceso desde nuestras direcciones IP. Son `54.88.76.97` y `34.250.211.151`, pero también está en la página de credenciales de MySQL:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Crear un usuario de MySQL para [!DNL MBI]

La forma más sencilla de crear un `MySQL` usuario para [!DNL MBI] es ejecutar la siguiente consulta cuando haya iniciado sesión `MySQL` con `GRANT` privilegios. Reemplazar `MBI IP Address` con la variable [!DNL MBI] Dirección IP y reemplazo `secure password` con una contraseña segura de su elección:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Para restringir el acceso de este usuario a datos en bases de datos, tablas o columnas específicas, puede ejecutar `GRANT` consultas que solo permiten el acceso a los datos permitidos.

**Vuelva a ejecutar la consulta GRANT para todas las IP requeridas utilizando el mismo usuario y contraseña.**

## Introducir información de conexión en MBI

Para ajustar las cosas, debemos introducir la conexión y la información del usuario en [!DNL MBI]. ¿Dejó abierta la página de credenciales de MySQL? Si no es así, vaya a **[!UICONTROL Data** > **Connections]** y haga clic en **[!UICONTROL Add New Data Source]**, luego el icono MySQL. No olvide cambiar el `Encrypted` alternar a `Yes`.

Introduzca la siguiente información en esta página, empezando por el `Database Connection` sección:

* `Connection Nickname`: Introduzca un nombre para la integración (por ejemplo, Ecommerce Store)
* `Username`: El nombre de usuario de la variable [!DNL MBI] Usuario MySQL
* `Password`: La contraseña de la variable [!DNL MBI] Usuario MySQL
* `Port`: Puerto de MySQL en su servidor (`3306` de forma predeterminada)
* `Host`: De forma predeterminada, será localhost. En general, será el valor de la dirección de enlace para su servidor MySQL, que de forma predeterminada es `127.0.0.1 (localhost)`, pero también podría ser alguna dirección de red local (por ejemplo, `192.168.0.1`) o la dirección IP pública del servidor.

   El valor se puede encontrar en su `my.cnf` archivo (normalmente se encuentra en `/etc/my.cnf`) debajo de la línea que dice: `\[mysqld\]`. Si la línea bind-address está comentada en ese archivo, el servidor está protegido de los intentos de conexión externos.

¡Eso es! Cuando haya terminado, haga clic en **[!UICONTROL Save & Test]** para completar la configuración.

## Documentación relacionada

* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
