---
title: Conectar Facebook Ads
description: Aprenda a analizar los datos de gasto en publicidad y ver si el dinero se gasta de forma eficaz.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 0%

---

# Conectar [!DNL Facebook Ads]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![Logotipo de Facebook Ads](../../../assets/facebook-ads-logo.png)

Usted hizo su investigación, creó sus anuncios, inició su campaña el [!DNL Facebook]. Ahora es el momento de analizar los datos de gasto en publicidad y ver si el dinero se está gastando de forma eficaz. Con los datos de gasto en publicidad, puede [medir el retorno de la inversión de la campaña combinando el costo de publicidad con el valor de duración del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) de los usuarios adquiridos de sus campañas.

Conectar los datos de [!DNL Facebook Ad] a [!DNL Commerce Intelligence] es un proceso sencillo de tres pasos:

1. [Agregar  [!DNL Facebook] como origen de datos en [!DNL Commerce Intelligence]](#stepone)
1. [Permitir  [!DNL Commerce Intelligence] acceso a tus [!DNL Facebook Ads] datos](#steptwo)
1. [Seleccionar [!DNL Facebook Ads] cuentas para extraer datos](#stepthree)

## Agregar [!DNL Facebook] como origen de datos en [!DNL Commerce Intelligence] {#stepone}

1. Para agregar la integración de [!DNL Facebook] a su cuenta de [!DNL Commerce Intelligence], vaya a la página de `Connections` en **[!UICONTROL Manage Data** > **Integrations]**.
1. Haga clic en **[!UICONTROL Add Integration]**, ubicado a la derecha.
1. Haga clic en el icono [!DNL Facebook]. Esto muestra la página de autorización [!DNL Facebook].
1. Haga clic en **[!UICONTROL Authorize]**.

## Permitir que [!DNL Commerce Intelligence] acceda a sus datos de [!DNL Facebook Ads] {#steptwo}

Después de hacer clic en **[!DNL Facebook Authorize]**, aparecerá una pequeña ventana emergente:

![Cuadro de diálogo de permiso de acceso a Facebook para Commerce Intelligence](../../../assets/Facebook_Access_Popup.png)

Sigue una serie de pasos para permitir que [!DNL Commerce Intelligence] tenga acceso a los datos de su perfil público, [!DNL Facebook Ads] y estadísticas relacionadas. Haga clic **[!UICONTROL OK]** en estos pasos para continuar.

## Seleccionar [!DNL Facebook Ads] cuentas para extraer datos {#stepthree}

1. Una vez completada la autenticación, se le pedirá que seleccione las [!DNL Facebook Ads] cuentas de las que desee extraer datos. Seleccione las cuentas que desee haciendo clic en la casilla de verificación de la columna `Connect`.

   ![Interfaz de selección de cuentas de Facebook Ad](../../../assets/Facebook_Ad_Accounts.png)

1. Haga clic en **[!UICONTROL Save Connections]**.

   Si la conexión se ha realizado correctamente, se ha realizado correctamente una conexión de *.* mensaje se muestra en la parte superior de la página.

## ¿Cuál es el siguiente paso? {#next}

Asegúrese de realizar el seguimiento de [!DNL Facebook] campañas en [!DNL Google Analytics]. Esto garantiza que el campo `utm\_campaign` de [!DNL Google Analytics] se rellene correctamente para sus campañas [!DNL Facebook].

## Relacionado

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
* [Conecta tu cuenta de  [!DNL Google Adwords] &#x200B;](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de pedido mediante  [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../../analysis/track-usr-dev-browser.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo funciona la atribución de  [!DNL Google Analytics] UTM?](../../analysis/utm-attributes.md)
