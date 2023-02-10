---
title: Conectar Google Analytics
description: Aprenda a conectar Google Analytics con [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en Internet. Implementación [!DNL Google Analytics] en el sitio web permite rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, dónde abandonan los visitantes, etc. Analizar estas métricas en [!DNL MBI], junto con otros datos, mejorará el estado general y la capacidad de uso de su sitio.

Empecemos entrando en nuestra [!DNL Google Analytics] credenciales a [!DNL MBI]:

1. Vaya a la **[!UICONTROL Manage Data** > **Integrations]** página.
1. Haga clic en **[!UICONTROL Add Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en el [!DNL Google Analytics] icono. Se abrirá la variable [!DNL Google Analytics] credenciales .
1. Escriba la [!DNL Google Analytics] credenciales. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL MBI].
1. Se mostrará una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL MBI]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte [!DNL Google Analytics] a continuación.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Los cambios se guardan automáticamente, por lo que haga clic en **Volver a Conexiones** cuando haya terminado.

## Conexión múltiple [!DNL Google Analytics] perfiles

Es posible que tenga varios sitios web conectados a una sola [!DNL Google Analytics] cuenta, identificada por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tendrá la opción de incluir todos sus ID de perfil en [!DNL MBI]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión [!DNL Google Analytics]
1. Vaya al sitio web en particular [!DNL Google Analytics] tablero
1. Busque la dirección URL: el ID de perfil corresponde a los 8 números siguientes `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconexión [!DNL Google Analytics] from [!DNL MBI] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de la cuenta](https://www.google.com/accounts/) página.
1. En el `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL MBI].

## Relacionado:

* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conexión [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de los clientes](../../analysis/web-act-cust-conversion.md)
* [Seguimiento de datos de adquisición de usuarios mediante [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
