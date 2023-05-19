---
title: Conectar Google AdWords
description: Aprenda a medir el ROI de la campaña combinando el coste de la publicidad con el valor de duración del cliente (CLV) de los usuarios adquiridos de las campañas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Hiciste tu investigación, creaste tus anuncios, lanzaste tu [!DNL Google] campaña. Ahora es el momento de analizar los datos de gasto en publicidad y ver si el dinero se está gastando de forma eficaz. Con los datos de gasto en publicidad, puede hacer lo siguiente [mida el ROI de la campaña combinando el coste de la publicidad con el valor de duración del cliente (CLV)](../../analysis/roi-ad-camp.md) de usuarios adquiridos de sus campañas.

Comience introduciendo su [!DNL Google Adwords] credenciales en [!DNL Commerce Intelligence].

1. Vaya a la `Connections` página debajo de **Administrar datos > Integraciones**.
1. Clic **Añadir integración**, situado en la parte superior derecha de la pantalla.
1. Haga clic en **[!DNL Google Adwords]** icono. Esto abre el [!DNL Google Adwords] página credenciales.
1. Introduzca su [!DNL Google Analytics] credenciales. Una vez completado el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].
1. Se muestra una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Los cambios se guardan automáticamente, por lo que haga clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la `Connecting Multiple Google Analytics profiles` más abajo.

## Conexión múltiple [!DNL Google Analytics] perfiles

Es posible que tenga varios sitios web conectados a un único [!DNL Google Analytics] cuenta, identificadas por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tiene la opción de incluir todos los ID de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

**Para identificar el ID de perfil de Google Analytics de un sitio web en particular:**

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al sitio web de [!DNL Google Analytics] tablero
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconectando [!DNL Google Adwords]

1. Visite su [!DNL Google] [configuración de cuenta](https://www.google.com/account/about/?hl=en) página.
1. En el `Security` , haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Clic **[!UICONTROL revoke access]**.

## Relacionado

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Rastrear origen de referencia de pedido mediante [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../../analysis/utm-attributes.md)
