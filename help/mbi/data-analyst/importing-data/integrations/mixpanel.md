---
title: Conectar Mixpanel
description: Obtenga información sobre cómo analizar cómo navegan y utilizan los usuarios sus sitios web y aplicaciones.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/ap-nWiPVnPSpvUT4uiimZ7iC4fiuKvKH0ZMVkOTDcK8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
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
source-wordcount: 246
ht-degree: 0%

---

# Conectar [!DNL Mixpanel]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![Logotipo de Mixpanel](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel], puedes analizar cómo navegan y usan tus sitios web y aplicaciones los usuarios. Echar un vistazo a los datos de comportamiento de los usuarios conduce a decisiones de diseño y desarrollo más inteligentes, lo que significa un mejor producto en general. Conectar [!DNL Mixpanel] a [!DNL Commerce Intelligence] le permite analizar el comportamiento de los usuarios y cómo ese comportamiento se traduce en ingresos.

Conectar los datos de [!DNL Mixpanel] a [!DNL Commerce Intelligence] es un proceso sencillo de tres pasos:

1. [Abrir la página  [!DNL Mixpanel] credenciales en [!DNL Commerce Intelligence]](#stepone)
1. [Recuperar sus  [!DNL Mixpanel] credenciales de API](#steptwo)
1. [Escriba sus [!DNL Mixpanel] credenciales de API en [!DNL Commerce Intelligence]](#stepthree)

Para completar este proceso, debe abrir dos ventanas o fichas del explorador, una para [!DNL Commerce Intelligence] y otra para su cuenta de [!DNL Mixpanel].

## Abriendo la página de credenciales de [!DNL Mixpanel] {#stepone}

Introducción a:

1. Vaya a la página `Connections` en **[!DNL Manage Data** > **Connections]**.

1. Haga clic en **[!UICONTROL Add a New Source]**, ubicado en el lado derecho de la pantalla sobre la tabla `Data Sources`.

1. Haga clic en el icono [!DNL Mixpanel] y abra la página de credenciales.

Deje esta página abierta por ahora y cambie a la ventana del explorador con su cuenta de [!DNL Mixpanel].

## Recuperando sus credenciales de la API [!DNL Mixpanel] {#steptwo}

Si todavía no inició sesión en su cuenta de [!DNL Mixpanel], hágalo y haga lo siguiente:

1. Haga clic en **[!UICONTROL Account]** en la esquina superior derecha.

1. En el cuadro de diálogo que se muestra, haga clic en **[!UICONTROL Projects]**.

1. Se muestran sus credenciales de API:

![Recuperando credenciales de API de Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantén esto abierto, lo necesitas para terminar esto.

## Escribiendo sus credenciales de la API [!DNL Mixpanel] en [!DNL Commerce Intelligence] {#stepthree}

1. Copie `API Key` y `Secret` en la página de credenciales de [!DNL Mixpanel] en [!DNL Commerce Intelligence].
1. Haga clic en **[!UICONTROL Connect to Mixpanel]** para completar la instalación.

Si la conexión se ha realizado correctamente, _¡Correcto!_ mensaje se muestra en la parte superior de la página.

### Relacionado

* [Se esperaban  [!DNL Mixpanel] datos](../integrations/mixpanel-data.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
