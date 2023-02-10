---
title: Conectar Facebook Ads
description: Aprenda a analizar los datos de gasto publicitario y a ver si se gasta su dinero de manera efectiva.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Realizó su investigación, creó sus publicidades, inició su campaña en [!DNL Facebook]. Ahora es el momento de analizar los datos del gasto publicitario y ver si el dinero se está gastando de manera efectiva. Con los datos de gasto en publicidad, puede [mida el ROI de la campaña casando su coste publicitario con el valor de duración del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) de usuarios adquiridos en sus campañas.

Conexión de los datos de publicidad de Facebook a [!DNL MBI] es un proceso sencillo de tres pasos:

1. [Agregar [!DNL Facebook] como fuente de datos en [!DNL MBI]](#stepone)
1. [Permitir [!DNL MBI] acceso a su [!DNL Facebook Ads] data](#steptwo)
1. [Select [!DNL Facebook Ads] Cuentas para extraer datos](#stepthree)

## Agregar [!DNL Facebook] como fuente de datos en [!DNL MBI] {#stepone}

1. Para agregar la variable [!DNL Facebook] integración con su cuenta, vaya a la `Connections` página debajo de **[!UICONTROL Manage Data** > **Integrations]**.
1. Haga clic en **[!UICONTROL Add Integration]**, situado en el lado derecho de la pantalla, encima de los datos `Sources` tabla.
1. Haga clic en el [!DNL Facebook] icono. Se mostrará la variable [!DNL Facebook] página de autorización.
1. Haga clic en **[!UICONTROL Authorize]**.

## Permitir [!DNL MBI] acceso a su [!DNL Facebook Ads] data {#steptwo}

Después de hacer clic en **[!DNL Facebook Authorize]**, aparece una pequeña ventana emergente:

![](../../../assets/Facebook_Access_Popup.png)

Siga una serie de pasos para permitir [!DNL MBI] para acceder a los datos de su perfil público, [!DNL Facebook Ads] y estadísticas relacionadas. Haga clic en **[!UICONTROL OK]** para continuar.

## Select [!DNL Facebook Ads] Cuentas para extraer datos {#stepthree}

1. Una vez finalizada la autenticación, se le pedirá que seleccione la variable [!DNL Facebook Ads] Cuentas de las que desea extraer datos. Para seleccionar las cuentas que desee, haga clic en la casilla de verificación de la `Connect` para abrir el Navegador.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Haga clic en **[!UICONTROL Save Connections]**.

   Si la conexión se realiza correctamente, una *Conexión correcta* se mostrará en la parte superior de la página.

## ¿qué sigue? {#next}

Asegúrese de que está realizando el seguimiento [!DNL Facebook] campañas en [!DNL Google Analytics]. Esto garantizará que la variable `utm\_campaign` en [!DNL Google Analytics] se rellena correctamente para [!DNL Facebook] campañas.

## Relacionado

* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conecte su [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Rastrear la fuente de referencia de pedidos a través de [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Seguimiento del origen de referencia del usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Seguimiento de datos de dispositivos de usuario, exploradores y sistemas operativos en la base de datos](../../analysis/track-usr-dev-browser.md)
* [Descubra las fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumento del ROI en las campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../../analysis/utm-attributes.md)
