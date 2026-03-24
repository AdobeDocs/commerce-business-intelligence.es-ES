---
title: Conectar Stripe
description: Aprenda a administrar y rastrear los datos de pagos y facturas de su empresa.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
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
source-wordcount: 151
ht-degree: 0%

---

# Conectar [!DNL Stripe]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![logotipo de Stripe](../../../assets/stripe-logo.png)

[!DNL Stripe] le permite administrar y rastrear los datos de pagos y facturas de su empresa. Conectar su cuenta de [!DNL Stripe] a [!DNL Commerce Intelligence] es un proceso sencillo de dos pasos:

1. [Agregar  [!DNL Stripe] como origen de datos en [!DNL Commerce Intelligence]](#stepone)
1. [Permitir  [!DNL Commerce Intelligence] acceso a tus [!DNL Stripe] datos](#steptwo)

## Agregar [!DNL Stripe] como origen de datos {#stepone}

1. Vaya a la página `Connections` en **[!UICONTROL Admin** > **Connections]**.
1. Haga clic en **[!UICONTROL Add a Data Source]**, ubicado en el lado derecho de la pantalla sobre la tabla `Data Sources`.
1. Haga clic en el icono [!DNL Stripe]. Esto muestra la página `[!DNL Stripe] authorization`.
1. Haga clic en **[!UICONTROL Connect with Stripe]**.

## Permitir que [!DNL Commerce Intelligence] acceda a sus datos de [!DNL Stripe] {#steptwo}

Después de hacer clic en **[!UICONTROL Connect with Stripe]**, aparecerá una página de solicitud de acceso.

1. Haga clic en **[!UICONTROL Sign in with Stripe to Continue]**.

1. Escriba sus credenciales y haga clic en **[!UICONTROL Sign in to your account]**.

1. Se validarán sus credenciales y se le redirigirá a [!DNL Commerce Intelligence].

1. Si la conexión se ha realizado correctamente, se ha realizado correctamente una conexión de *.El mensaje* aparece en la parte superior de la pantalla.

## Relacionado:

La [[!DNL Stripe] documentación de la API](https://stripe.com/docs/api) puede ser un recurso útil para obtener más información acerca de cómo [!DNL Stripe] se integra con [!DNL Commerce Intelligence].

* [Se esperaban  [!DNL Stripe] datos](../integrations/stripe-data.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
