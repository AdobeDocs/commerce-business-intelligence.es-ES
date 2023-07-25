---
title: Conectar Zendesk
description: Obtenga información sobre cómo consolidar los informes del servicio de asistencia en [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conexión de su [!DNL Zendesk] Los datos de le permiten consolidar sus informes del servicio de asistencia en [!DNL Commerce Intelligence]. Esto le permite optimizar la asistencia al cliente y supervisar el rendimiento del servicio de asistencia junto con sus ingresos.

Conexión de su [!DNL Zendesk] Los datos de son un proceso sencillo de tres pasos:

1. [Abra el [!DNL Zendesk] página credenciales en [!DNL Commerce Intelligence]](#stepone)
1. [Recupere su [!DNL Zendesk] Token de API](#steptwo)
1. [Introduzca su [!DNL Zendesk] información de inicio de sesión y token en [!DNL Commerce Intelligence]](#stepthree)

Para completar este proceso, debe abrir dos ventanas o pestañas del explorador, una para [!DNL Commerce Intelligence], el otro para su [!DNL Zendesk] cuenta.

## Abra el [!DNL Zendesk] página credenciales en [!DNL Commerce Intelligence] {#stepone}

1. Vaya a la `Integrations` página debajo de **[!UICONTROL Manage Data** > ** Fuentes de datos **> **Integraciones]**.
1. Clic **[!UICONTROL Add Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en [!DNL Zendesk] icono. Esto abre el [!DNL Zendesk] página credenciales.

## Recupere su [!DNL Zendesk] Token de API {#steptwo}

1. En la ventana o pestaña donde inició sesión en su [!DNL Zendesk] , haga clic en el icono Configuración (engranaje) en la esquina inferior izquierda de la pantalla.
1. Si la variable `Settings` del menú, busque la variable `Channels` sección. Clic **[!UICONTROL API]** en esta sección.
1. En el `Token Access` de esta página, haga clic en la casilla de verificación situada junto a `Enabled`. Se muestra una lista de tokens de API activos.
1. Clic **[!UICONTROL Add New Token]**.
1. Cuando se le solicite, introduzca una etiqueta para el token. Adobe recomienda utilizar `Commerce Intelligence`, para que sepa de un vistazo qué aplicación utiliza el token.
1. Clic **[!UICONTROL Create]**.
1. Se crea un token de API. Copie este token, se utilizará en el siguiente paso.

## Entrar [!DNL Zendesk] información de inicio de sesión y token de API en [!DNL Commerce Intelligence] {#stepthree}

1. Introduzca su [!DNL Zendesk] prefijo de sitio e inicio de sesión en la [!DNL Zendesk] página credenciales en [!DNL Commerce Intelligence].
1. Introduzca su token de API.
1. Clic **[!UICONTROL Save & Connect]**. Si la conexión se realiza correctamente, *Conexión correcta.* El mensaje se muestra en la parte superior de la pantalla.

## Relacionado:

* [Previsto [!DNL Zendesk] datos](../integrations/exp-zendesk-data.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
