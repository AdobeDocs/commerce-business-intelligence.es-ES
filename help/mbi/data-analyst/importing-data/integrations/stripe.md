---
title: Stripe de Connect
description: Aprenda a administrar y rastrear los datos de pagos y facturas de su empresa.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Conectar [!DNL Stripe]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

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
