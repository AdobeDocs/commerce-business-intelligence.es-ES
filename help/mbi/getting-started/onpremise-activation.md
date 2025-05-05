---
title: Activar tu cuenta de  [!DNL Adobe Commerce Intelligence]
description: Aprenda con quién ponerse en contacto para activar su cuenta de  [!DNL Commerce Intelligence] .
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Activar su cuenta de [!DNL Commerce Intelligence] para suscripciones locales y de inicio

Para activar [!DNL Commerce Intelligence] para suscripciones locales, primero cree una cuenta de [!DNL Commerce Intelligence], escriba la información de configuración y, a continuación, conecte [!DNL Commerce Intelligence] a la base de datos de [!DNL Commerce]. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Crear su cuenta de [!DNL Commerce Intelligence]

Para crear su cuenta, póngase en contacto con el equipo de cuenta de Adobe o con el asesor técnico del cliente.

## Cree su contraseña

Una vez creada la cuenta, busque en su correo electrónico un mensaje de notificación de cuenta de [!DNL The Magento BI Team@rjmetrics.com]. Use el vínculo proporcionado en el correo electrónico para obtener acceso a su cuenta de [!DNL Commerce Intelligence] y crear su contraseña. Vaya a la bandeja de entrada y verifique su dirección de correo electrónico.

Si no recibió un correo electrónico, [comuníquese con la atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).

![](../assets/create-account-4.png)

## Establecer las preferencias de la tienda

Antes de configurar la conexión a la base de datos, complete el formulario de información de almacenamiento. Esta información es necesaria para completar la configuración de **[!UICONTROL Connect your Database]**.

![](../assets/create-account-6.png)

## Agregar [!DNL Commerce Intelligence] usuarios

Después de establecer su contraseña e iniciar sesión en [!DNL Commerce Intelligence], puede agregar otros usuarios a su cuenta de [!DNL Commerce Intelligence]. Al agregar usuarios, agregue usuarios administradores con los permisos adecuados para completar el proceso de activación.

![](../assets/create-account-5.png)

## Crear un usuario [!DNL Commerce Intelligence] dedicado en el administrador [!DNL Commerce]

Para usar [!DNL Commerce Intelligence], debe agregar un usuario permanente y dedicado al proyecto [!DNL Commerce]. Este usuario especializado sirve como una conexión permanente con [!DNL Commerce] que permite la captura y transferencia de nuevos datos a la Data Warehouse [!DNL Commerce Intelligence] de la cuenta.

La configuración de un usuario [!DNL Commerce Intelligence] dedicado garantiza que la cuenta no se desactive ni elimine, deteniendo así la conexión [!DNL Commerce Intelligence].


>[!NOTE]
>
>El Adobe recomienda utilizar un nombre de cuenta que indique su estado permanente (por ejemplo, dedicado a ACI, conector de base de datos de ACI, etc.).

Después de crear el usuario dedicado para [!DNL Commerce Intelligence] en el Administrador, agregue el mismo usuario al entorno principal del proyecto [!DNL Commerce] con la configuración **[!UICONTROL Master]** de `Contributor`.

![](../assets/commerce-add-user-settings.png)

## Obtención de las claves SSH de Commerce Intelligence

1. En la página [!UICONTROL Connect your database] para la configuración de [!DNL Commerce Intelligence], desplácese hacia abajo y seleccione **[!UICONTROL Encryption settings]**.

1. Para **Tipo de cifrado**, seleccione `SSH Tunnel`.

1. En la lista desplegable, copie la clave pública proporcionada.

   ![](../assets/encryption-setting-new-account.png)

## Agregue su clave pública a [!DNL Commerce Intelligence]

1. Desde [!DNL Commerce Admin], inicie sesión con la información de inicio de sesión del usuario [!DNL Commerce Intelligence] que acaba de crear.

1. Seleccione la ficha **Configuración de la cuenta**.

1. Desplácese hacia abajo y expanda la lista desplegable **[!UICONTROL SSH Keys]**. A continuación, seleccione **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. Pegue la clave pública que copió en el paso [!DNL Encryption Type] anterior.

   ![](../assets/paste-public-key.png)

## Proporcionar credenciales de [!DNL Commerce Intelligence] Essentials `MySQL`

1. Actualice su `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. Actualice su `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## Obtener información de conexión a base de datos

Obtener la información de conexión de base de datos a la base de datos [!DNL Commerce] para [!DNL Commerce Intelligence]

1. Ejecute lo siguiente para obtener su información.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Revise la información de la base de datos, que debería ser similar al siguiente ejemplo.

   ![](../assets/example-database-information.png)

## Conectar [!DNL Commerce Intelligence] a la base de datos [!DNL Commerce] mediante una conexión cifrada

>[!NOTE]
>
>El Adobe recomienda encarecidamente que utilice un túnel [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) para establecer la conexión con la base de datos. Sin embargo, si este método no es una opción, aún puede vincular [!DNL Commerce Intelligence] a su base de datos con un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Escriba su información de [!DNL Commerce Intelligence] en la pantalla de [!UICONTROL Connect your Magento Database].

![](../assets/connect-magento-db.png)

**Entradas:**

[!UICONTROL Integration Name]: [elija un nombre para su instancia de [!DNL Commerce Intelligence]]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Nombre de usuario]: `mbi`

[!UICONTROL Password]: [contraseña de entrada mostrada en la sección anterior]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [dejar en blanco si no hay prefijos de tabla]

## Establece la configuración de la [!UICONTROL **zona horaria**]

![](../assets/time-zone-settings.png)

**Entradas:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [elija la zona horaria para la cual desea que se muestren sus datos]

## Obtener la información de configuración de cifrado

La IU del proyecto proporciona una cadena de acceso SSH. Esta cadena se puede usar para recopilar la información necesaria para [!UICONTROL **Dirección remota**] y [!UICONTROL **Nombre de usuario**]. Utilice la cadena de acceso SSH seleccionando el botón del sitio de acceso en la rama maestra de la interfaz de usuario del proyecto. A continuación, busque sus [!UICONTROL User Name] y [!UICONTROL Remote Address] como se muestra a continuación.

![](../assets/master-branch-settings.png)

## Introducir la configuración de [!DNL Encryption]

![](../assets/encryption-settings-2.png)

**Entradas:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud` [del paso anterior]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento` [del paso anterior]

[!UICONTROL Port]: `22`

## Guarde la integración.

Después de completar los pasos de configuración, aplique los cambios seleccionando [!UICONTROL **Guardar integración**].

Ahora ha conectado correctamente su base de datos [!DNL Commerce] a su cuenta [!DNL Commerce Intelligence].

>[!NOTE]
>
>Si es cliente de [!DNL Adobe Commerce Intelligence Pro], póngase en contacto con el administrador de éxito de los clientes o con el asesor técnico del cliente para coordinar los siguientes pasos.

Después de completar la configuración, [inicia sesión](../getting-started/sign-in.md) en tu cuenta de [!DNL Commerce Intelligence].

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
