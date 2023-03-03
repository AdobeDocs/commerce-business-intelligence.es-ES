---
title: Activar su [!DNL MBI] Cuenta para suscripciones a Cloud Starter
description: Obtenga información sobre cómo activar [!DNL MBI] para proyectos de Cloud Starter.
exl-id: 172439ee-fa1d-4872-b6a9-c61a212a7cbe
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Activar su [!DNL MBI] Cuenta para `Cloud Starter` Suscripciones

Para activar [!DNL MBI] para `Cloud Starter` proyectos, cree primero un [!DNL MBI] cuenta y, a continuación, cree una `SSH` clave y, finalmente, conéctese a la base de datos de Commerce. Consulte [activación de suscripciones on-premise](../getting-started/onpremise-activation.md).

>[!NOTE]
>
>Para obtener ayuda sobre la activación [!DNL MBI] para `Cloud Pro` proyectos, póngase en contacto con el equipo de cuenta de Adobe o con el asesor técnico del cliente.

1. Cree su [!DNL MBI] Cuenta.

   - Ir a [Inicio de sesión de cuenta Adobe Commerce](https://account.magento.com/customer/account/login)

   - Ir a **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clic **[!UICONTROL Create Instance]**. Si no ve este botón, póngase en contacto con el equipo de cuenta de Adobe o con el asesor técnico del cliente.

   - Seleccione su `Cloud Starter` suscripción. Si solo tiene un `cloud starter` suscripción: esta opción se selecciona automáticamente.

   - Clic **[!UICONTROL Continue]**.

   - Introduzca su información para crear su cuenta de.

   ![](../assets/create-account-2.png)

   - Vaya a la bandeja de entrada y verifique su dirección de correo electrónico.

   ![](../assets/create-account-3.png)

   - Cree su contraseña.

   ![](../assets/create-account-4.png)

   - Después de crear la cuenta, tendrá la opción de agregar usuarios a la nueva cuenta. Ahora se pueden añadir administradores técnicos para llevar a cabo los siguientes pasos.

   ![](../assets/create-account-5.png)

1. Introduce información sobre tu tienda para establecer tus preferencias.

   ![](../assets/create-account-6.png)

   Debe recopilar cierta información antes de poder conectar la base de datos para el tercer paso del flujo de incorporación. Va a rellenar el `Connect your database` en el paso 9.

1. Crear dedicado [!DNL MBI] Usuario.

   - Cree un nuevo usuario en su [cuenta de Adobe Commerce](https://accounts.magento.com).

   - _¿Por qué un nuevo usuario?_ [!DNL MBI] necesita que se agregue un usuario al proyecto para recuperar continuamente nuevos datos que se transferirán al [!DNL MBI] data warehouse. Este usuario servirá como esa conexión. Añadir este usuario al proyecto se realizará en el paso 4.

   - La razón de tener un dedicado [!DNL MBI] el usuario debe evitar que el usuario añadido se desactive o elimine de forma involuntaria y que detenga el [!DNL MBI] conexión.

1. Agregue el usuario recién creado al entorno principal del proyecto como `Contributor`.

   ![](../assets/create-account-7.png)

1. Obtenga su [!DNL MBI] `SSH` llaves.

   - Vaya a la `Connect your database` página de la [!DNL MBI] configure la interfaz de usuario de y desplácese hacia abajo hasta `Encryption settings`.

   - Para el `Encryption Type` , elija `SSH Tunnel`.

   - En el menú desplegable, puede copiar y pegar el proporcionado [!DNL MBI] `Public Key`.

   ![](../assets/create-account-8.png)

1. Añada el nuevo [!DNL MBI] `Public key` a la [!DNL MBI] Usuario creado en el paso 5.

   - Ir a [su cuenta de cloud Adobe Commerce](https://accounts.magento.cloud/). Inicie sesión con su información de inicio de sesión de la cuenta para el nuevo [!DNL MBI] usuario creado. A continuación, vaya a `Account Settings` pestaña.

   - Desplácese hacia abajo por la página y expanda la lista desplegable para `SSH` llaves. Luego haga clic en **[!UICONTROL Add a public key]**.

   ![](../assets/create-account-9.png)

   - Añada el [!DNL MBI] `SSH Public Key` desde arriba.

   ![](../assets/create-account-10.png)

1. Proporcionar [!DNL MBI] Credenciales de MySQL.

   - Actualice su `.magento/services.yaml`

   ```sql
   mysql:
       type: mysql:10.0
       disk: 2048
       configuration:
           schemas:
               - main
           endpoints:
               mysql:
                   default_schema: main
                   privileges:
                       main: admin
               mbi:
                   default_schema: main
                   privileges:
                       main: ro
   ```

   - Actualice su `.magento.app.yaml`

   ```sql
           relationships:
               database: "mysql:mysql"
               mbi: "mysql:mbi"
               redis: "redis:redis"
   ```

1. Obtener información para conectar la base de datos a [!DNL MBI].

   Ejecutar
   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

   para obtener información sobre cómo conectar la base de datos.

   Debe recibir información similar a la siguiente:

   ```json
           "mbi" : [
                 {
                    "scheme" : "mysql",
                    "rel" : "mbi",
                    "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                    "query" : {
                       "is_master" : true
                    },
                    "ip" : "169.254.169.143",
                    "path" : "main",
                    "host" : "[!DNL MBI].internal",
                    "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                    "username" : "mbi",
                    "service" : "mysql",
                    "port" : 3306,
                    "password" : "[password]"
                 }
              ],
   ```

1. Conectar su base de datos de Commerce

   ![](../assets/create-account-11.png)

   - `Integration Name`: [Elija un nombre para la integración.]

   - `Host`: `[!DNL MBI].internal`

   - `Port`: `3306`

   - `Username`: `mbi`

   - `Password`: [contraseña de entrada proporcionada en la salida para el paso 8.]

   - `Database Name`: `main`

   - `Table Prefixes`: [dejar en blanco si no hay prefijos de tabla]

1. Defina la Configuración de zona horaria.

   ![Entradas](../assets/create-account-12.png)

   - `Database`: `Timezone: UTC`

   - `Desired Timezone`: [Elija la zona horaria en la que desea que se muestren los datos.]

1. Obtenga información para la configuración de cifrado.

   - La interfaz de usuario del proyecto proporciona un `SSH` cadena de acceso. Esta cadena se puede utilizar para recopilar la información necesaria para `Remote Address` y `Username` al configurar su `Encryption` configuración. Utilice el `SSH Access` cadena encontrada al hacer clic en el botón de acceso al sitio en la rama maestra de la interfaz de usuario del proyecto y encontrar la `User Name` y `Remote Address` como se muestra a continuación.

   ![](../assets/create-account-13.png)

   ![](../assets/create-account-14.png)

1. Introduzca información para su `Encryption` configuración

   ![](../assets/create-account-15.png)

   **Entradas**

   - `Encryption Type`: `SSH Tunnel`

   - `Remote Address`: `ssh.us-3.magento.cloud`

   - `Username`: `vfbfui4vmfez6-master-7rqtwti--mymagento`

   - `Port`: `22`

1. Clic **[!UICONTROL Save Integration]**.

1. Ahora se ha conectado correctamente a su [!DNL MBI] cuenta.

1. Después de conectarse correctamente [!DNL MBI] En la base de datos de Commerce, póngase en contacto con el equipo de cuenta de Adobe para coordinar los siguientes pasos, como la configuración de integraciones y otros pasos de configuración.

1. Cuando termine la configuración, puede hacer lo siguiente [iniciar sesión](../getting-started/sign-in.md) a su [!DNL MBI] cuenta.
