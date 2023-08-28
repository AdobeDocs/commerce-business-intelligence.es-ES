---
title: Activar su [!DNL Adobe Commerce Intelligence] Cuenta
description: Aprenda con quién ponerse en contacto para activar su [!DNL Commerce Intelligence] cuenta.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Activar su [!DNL Commerce Intelligence] Cuenta para suscripciones locales y de inicio

Para activar [!DNL Commerce Intelligence] para suscripciones on-premise, cree primero una [!DNL Commerce Intelligence] cuenta, introduzca la información de configuración y, a continuación, conecte [!DNL Commerce Intelligence] a su [!DNL Commerce] base de datos. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Cree su [!DNL Commerce Intelligence] account

Para crear su cuenta, póngase en contacto con el equipo de cuenta de Adobe o con el asesor técnico del cliente.

## Cree su contraseña

Una vez creada la cuenta, busque en su correo electrónico un correo electrónico de notificación de la cuenta en [!DNL The Magento BI Team@rjmetrics.com]. Utilice el vínculo proporcionado en el correo electrónico para acceder a sus [!DNL Commerce Intelligence] y cree su contraseña. Vaya a la bandeja de entrada y verifique su dirección de correo electrónico.

Si no ha recibido un correo electrónico, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![](../assets/create-account-4.png)

## Establecer las preferencias de la tienda

Antes de configurar la conexión a la base de datos, complete el formulario de información de almacenamiento. Esta información es necesaria para completar el **[!UICONTROL Connect your Database]** configuración.

![](../assets/create-account-6.png)

## Añadir [!DNL Commerce Intelligence] usuarios

Después de establecer la contraseña e iniciar sesión en [!DNL Commerce Intelligence], puede agregar otros usuarios a su [!DNL Commerce Intelligence] cuenta. Al agregar usuarios, agregue usuarios administradores con los permisos adecuados para completar el proceso de activación.

![](../assets/create-account-5.png)

## Cree un dedicado [!DNL Commerce Intelligence] usuario en [!DNL Commerce] administrador

Para usar [!DNL Commerce Intelligence], debe agregar un usuario permanente y dedicado al [!DNL Commerce] proyecto. Este usuario dedicado sirve como conexión permanente a [!DNL Commerce] que permite recuperar y transferir nuevos datos al [!DNL Commerce Intelligence] Data Warehouse.

Configuración de un dedicado [!DNL Commerce Intelligence] El usuario garantiza que la cuenta no se desactive ni elimine, por lo que el [!DNL Commerce Intelligence] conexión.


>[!NOTE]
>
>El Adobe recomienda utilizar un nombre de cuenta que indique su estado permanente (por ejemplo, dedicado a ACI, conector de base de datos de ACI, etc.).

Después de crear el usuario dedicado para [!DNL Commerce Intelligence] en el Administrador, añada el mismo usuario al entorno principal del [!DNL Commerce] proyecto con un **[!UICONTROL Master]** configuración de `Contributor`.

![](../assets/commerce-add-user-settings.png)

## Obtenga sus claves SSH de Commerce Intelligence

1. En el [!UICONTROL Connect your database] página para [!DNL Commerce Intelligence] configure, desplácese hacia abajo y seleccione **[!UICONTROL Encryption settings]**.

1. Para **Tipo de cifrado**, seleccione `SSH Tunnel`.

1. En la lista desplegable, copie la clave pública proporcionada.

   ![](../assets/encryption-setting-new-account.png)

## Añada la clave pública a [!DNL Commerce Intelligence]

1. Desde el [!DNL Commerce Admin], inicie sesión con la información de inicio de sesión para [!DNL Commerce Intelligence] usuario que acaba de crear.

1. Seleccione el **Configuración de cuenta** pestaña.

1. Desplácese hacia abajo y expanda **[!UICONTROL SSH Keys]** menú desplegable. A continuación, seleccione **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. Pegue la clave pública que ha copiado en la [!DNL Encryption Type] paso superior.

   ![](../assets/paste-public-key.png)

## Proporcionar [!DNL Commerce Intelligence] Essentials `MySQL` credenciales

1. Actualice su `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. Actualice su `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## Obtener información de conexión a base de datos

Obtenga la información de conexión de la base de datos en [!DNL Commerce] base de datos a [!DNL Commerce Intelligence]

1. Ejecute lo siguiente para obtener su información.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Revise la información de la base de datos, que debería ser similar al siguiente ejemplo.

   ![](../assets/example-database-information.png)

## Connect [!DNL Commerce Intelligence] a su [!DNL Commerce] base de datos con una conexión cifrada

>[!NOTE]
>
>El Adobe recomienda encarecidamente que utilice una [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) túnel para establecer la conexión con la base de datos. Sin embargo, si este método no es una opción, aún puede vincular [!DNL Commerce Intelligence] a la base de datos mediante un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Introduzca su [!DNL Commerce Intelligence] información en la [!UICONTROL Connect your Magento Database] pantalla.

![](../assets/connect-magento-db.png)

**Entradas:**

[!UICONTROL Integration Name]: [elija un nombre para su [!DNL Commerce Intelligence] instancia]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Nombre de usuario]: `mbi`

[!UICONTROL Password]: [contraseña de entrada mostrada en la sección anterior]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [dejar en blanco si no hay prefijos de tabla]

## Configure su [!UICONTROL **Zona horaria**] configuración

![](../assets/time-zone-settings.png)

**Entradas:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [elija la zona horaria para la que desea que se muestren los datos]

## Obtener la información de configuración de cifrado

La IU del proyecto proporciona una cadena de acceso SSH. Esta cadena se puede utilizar para recopilar la información necesaria para el [!UICONTROL **Dirección remota**] y [!UICONTROL **Nombre de usuario**]. Utilice la cadena de acceso SSH seleccionando el botón del sitio de acceso en la rama maestra de la interfaz de usuario del proyecto. A continuación, busque su [!UICONTROL User Name] y [!UICONTROL Remote Address] como se muestra a continuación.

![](../assets/master-branch-settings.png)

## Introduzca su [!DNL Encryption] configuración

![](../assets/encryption-settings-2.png)

**Entradas:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud`  [del paso anterior]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento`  [del paso anterior]

[!UICONTROL Port]: `22`

## Guarde la integración.

Después de completar los pasos de configuración, aplique los cambios seleccionando [!UICONTROL **Guardar integración**].

Ahora ha conectado correctamente su [!DNL Commerce] base de datos a su [!DNL Commerce Intelligence] cuenta.

>[!NOTE]
>
>Si es un [!DNL Adobe Commerce Intelligence Pro] Para coordinar los siguientes pasos, póngase en contacto con el administrador de éxito del cliente o con el asesor técnico del cliente.

Una vez completada la configuración, [iniciar sesión](../getting-started/sign-in.md) a su [!DNL Commerce Intelligence] cuenta.

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
