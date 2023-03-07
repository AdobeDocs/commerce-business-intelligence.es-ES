---
title: Conectar Facebook Ads
description: Aprenda a analizar los datos de gasto en publicidad y ver si el dinero se gasta de forma eficaz.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Hiciste tu investigación, creaste tus anuncios, lanzaste tu campaña en [!DNL Facebook]. Ahora es el momento de analizar los datos de gasto en publicidad y ver si el dinero se está gastando de forma eficaz. Con los datos de gasto en publicidad, puede hacer lo siguiente [mida el ROI de la campaña combinando el coste de la publicidad con el valor de duración del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) de usuarios adquiridos de sus campañas.

Conexión de los datos de anuncios de Facebook a [!DNL MBI] es un proceso sencillo de tres pasos:

1. [Añadir [!DNL Facebook] como fuente de datos en [!DNL MBI]](#stepone)
1. [Permitir [!DNL MBI] acceso a su [!DNL Facebook Ads] datos](#steptwo)
1. [Seleccionar [!DNL Facebook Ads] Cuentas para extraer datos](#stepthree)

## Añadir [!DNL Facebook] como fuente de datos en [!DNL MBI] {#stepone}

1. Para añadir el [!DNL Facebook] Integración de con su cuenta de, vaya a `Connections` página debajo de **[!UICONTROL Manage Data** > **Integrations]**.
1. Clic **[!UICONTROL Add Integration]**, situado en la parte derecha de la pantalla, encima de Data `Sources` tabla.
1. Haga clic en [!DNL Facebook] icono. Esto muestra el [!DNL Facebook] página de autorización.
1. Clic **[!UICONTROL Authorize]**.

## Permitir [!DNL MBI] acceso a su [!DNL Facebook Ads] datos {#steptwo}

Después de hacer clic **[!DNL Facebook Authorize]**, se mostrará una pequeña ventana emergente:

![](../../../assets/Facebook_Access_Popup.png)

Debe seguir una serie de pasos para permitir [!DNL MBI] para acceder a los datos de su perfil público, [!DNL Facebook Ads] y, estadísticas relacionadas. Clic **[!UICONTROL OK]** Siga estos pasos para continuar.

## Seleccionar [!DNL Facebook Ads] Cuentas para extraer datos {#stepthree}

1. Una vez completada la autenticación, se le pedirá que seleccione la variable [!DNL Facebook Ads] Cuentas de las que desea extraer datos. Seleccione las cuentas que desee haciendo clic en la casilla de verificación de la `Connect` columna.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Clic **[!UICONTROL Save Connections]**.

   Si la conexión se realiza correctamente, *Conexión correcta.* El mensaje se muestra en la parte superior de la página.

## ¿Cuál es el siguiente paso? {#next}

Asegúrese de que está realizando el seguimiento [!DNL Facebook] campañas en [!DNL Google Analytics]. Esto garantiza que la variable `utm\_campaign` field en [!DNL Google Analytics] se ha rellenado correctamente para su [!DNL Facebook] campañas.

## Relacionado

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conecte su [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de pedido mediante [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../../analysis/track-usr-dev-browser.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../../analysis/utm-attributes.md)
