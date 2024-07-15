---
title: Conectar Zendesk
description: Aprenda a consolidar los informes del servicio de asistencia en  [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Conectar [!DNL Zendesk]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conectar los datos de [!DNL Zendesk] le permite consolidar los informes del servicio de asistencia en [!DNL Commerce Intelligence]. Esto le permite optimizar la asistencia al cliente y supervisar el rendimiento del servicio de asistencia junto con sus ingresos.

Conectar los datos de [!DNL Zendesk] es un proceso sencillo de tres pasos:

1. [Abrir la página  [!DNL Zendesk] credenciales en [!DNL Commerce Intelligence]](#stepone)
1. [Recuperar su token de API  [!DNL Zendesk] 0](#steptwo)
1. [Escriba su [!DNL Zendesk] información de inicio de sesión y token en [!DNL Commerce Intelligence]](#stepthree)

Para completar este proceso, debe abrir dos ventanas o fichas del explorador: una para [!DNL Commerce Intelligence] y otra para la cuenta de [!DNL Zendesk].

## Abrir la página de credenciales de [!DNL Zendesk] en [!DNL Commerce Intelligence] {#stepone}

1. Vaya a la página `Integrations` en **[!UICONTROL Manage Data** > ** Fuentes de datos **> **Integraciones]**.
1. Haga clic en **[!UICONTROL Add Integration]**, ubicado en el lado derecho de la pantalla.
1. Haga clic en el icono [!DNL Zendesk]. Se abre la página de credenciales [!DNL Zendesk].

## Recuperar su token de API [!DNL Zendesk] {#steptwo}

1. En la ventana o pestaña donde inició sesión en su cuenta de [!DNL Zendesk], haga clic en el icono Configuración (engranaje) en la esquina inferior izquierda de la pantalla.
1. Cuando se muestre el menú `Settings`, busque la sección `Channels`. Haga clic en **[!UICONTROL API]** en esta sección.
1. En la sección `Token Access` de esta página, haga clic en la casilla que hay junto a `Enabled`. Se muestra una lista de tokens de API activos.
1. Haga clic en **[!UICONTROL Add New Token]**.
1. Cuando se le solicite, introduzca una etiqueta para el token. El Adobe recomienda usar `Commerce Intelligence` para saber de un vistazo qué aplicación está usando el token.
1. Haga clic en **[!UICONTROL Create]**.
1. Se crea un token de API. Copie este token, se utilizará en el siguiente paso.

## Escriba [!DNL Zendesk] información de inicio de sesión y token de API en [!DNL Commerce Intelligence] {#stepthree}

1. Escriba el prefijo del sitio [!DNL Zendesk] y el correo electrónico de inicio de sesión en la página de credenciales de [!DNL Zendesk] en [!DNL Commerce Intelligence].
1. Introduzca su token de API.
1. Haga clic en **[!UICONTROL Save & Connect]**. Si la conexión se ha realizado correctamente, se ha realizado correctamente una conexión de *.* mensaje se muestra en la parte superior de la pantalla.

## Relacionado:

* [Se esperaban  [!DNL Zendesk] datos](../integrations/exp-zendesk-data.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
