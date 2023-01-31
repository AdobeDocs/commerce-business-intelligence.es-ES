---
title: Conectar adwords de Google
description: Aprenda a medir el ROI de la campaña casando su coste publicitario con el valor de duración de clientes (CLV) de los usuarios adquiridos en sus campañas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Hiciste tu investigación, creaste tus publicidades, iniciaste tu campaña. Ahora es el momento de analizar los datos del gasto publicitario y ver si el dinero se está gastando de manera efectiva. Con los datos de gasto en publicidad, puede [mida el ROI de la campaña casando su coste publicitario con el valor de duración del cliente (CLV)](../../analysis/roi-ad-camp.md) de usuarios adquiridos en sus campañas.

Empecemos entrando en nuestra [!DNL Google Adwords] credenciales a [!DNL MBI]:

1. Vaya a la página Conexiones debajo de **Administrar datos > Integraciones**.
1. Haga clic en **Añadir integración**, situado en la parte superior derecha de la pantalla.
1. Haga clic en el **[!DNL Google Adwords]** icono. Se abrirá la variable [!DNL Google Adwords] credenciales .
1. Escriba la [!DNL Google Analytics] credenciales. Una vez completado el proceso de autorización, se le redirigirá de nuevo a [!DNL MBI].
1. Se mostrará una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. Los cambios se guardan automáticamente, por lo que haga clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la `Connecting Multiple Google Analytics profiles` a continuación.

## `Connecting multiple Google Analytics profiles`

Es posible que tenga varios sitios web conectados a una sola [!DNL Google Analytics] cuenta, identificada por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tendrá la opción de incluir todos sus ID de perfil en [!DNL MBI]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

**Para identificar el ID de perfil de los Google Analytics de un sitio web en particular:**

1. Iniciar sesión [!DNL Google Analytics]
1. Vaya al sitio web en particular [!DNL Google Analytics] tablero
1. Busque la dirección URL: el ID de perfil corresponde a los 8 números siguientes `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconexión [!DNL Google Adwords]

1. Visite su [!DNL Google] [configuración de la cuenta](https://www.google.com/accounts/) página.
1. En el `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL MBI].

## Relacionado

* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
* [Rastrear la fuente de referencia de pedidos a través de [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Seguimiento del origen de referencia del usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Seguimiento de datos de dispositivos de usuario, exploradores y sistemas operativos en la base de datos](https://support.magento.com/hc/en-us/articles/360016732911)
* [Descubra las fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumento del ROI en las campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../../analysis/utm-attributes.md)
