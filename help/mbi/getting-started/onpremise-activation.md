---
title: Activación de [!DNL MBI] Cuenta para suscripciones locales
description: Obtenga información sobre cómo activar su [!DNL MBI] cuenta para suscripciones locales.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Active su [!DNL MBI] Cuenta para suscripciones locales

Para activar [!DNL MBI] para suscripciones locales, cree primero un [!DNL MBI] cuenta y luego conectar [!DNL MBI] a la base de datos de Commerce. Para obtener información sobre la activación en `Cloud Starter` proyectos, consulte [Activación de [!DNL MBI] Cuenta para `Cloud Starter` Suscripciones](../getting-started/cloud-activation.md).

1. Cree su [!DNL MBI] Cuenta.

   - Vaya a [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - Vaya a **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Haga clic en **[!UICONTROL Create Instance]**. Si no ve este botón, póngase en contacto con el gestor de éxito del cliente o con el asesor técnico del cliente.

   - Introduzca la información para crear la cuenta.

   ![](../assets/create-account-2.png)

   - Vaya a la bandeja de entrada y compruebe su dirección de correo electrónico. Si no recibió un correo electrónico, [póngase en contacto con el servicio de asistencia técnica](../guide-overview.md).

   - Cree su contraseña.

   ![](../assets/create-account-4.png)

   - Después de crear la cuenta, tiene la opción de agregar usuarios a la nueva cuenta. Ahora se pueden añadir administradores técnicos para realizar los siguientes pasos.

   ![](../assets/create-account-5.png)

1. Introduzca información sobre la tienda para establecer sus preferencias.

   ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] a la base de datos de Commerce mediante una conexión cifrada.

   Commerce recomienda encarecidamente que se conecte con un [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). Sin embargo, si esta no es una opción, aún puede vincular [!DNL MBI] a la base de datos mediante un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Una vez que se haya conectado correctamente [!DNL MBI] en la base de datos de comercio, póngase en contacto con el administrador de éxito de los clientes para coordinar los pasos siguientes, como la configuración de integraciones y otros pasos de configuración.

1. Cuando termine la configuración, puede [iniciar sesión](../getting-started/sign-in.md) a su [!DNL MBI] cuenta.
