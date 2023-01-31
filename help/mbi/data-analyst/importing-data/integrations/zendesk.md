---
title: Conectar Zendesk
description: Aprenda a consolidar los informes del servicio de asistencia técnica en [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Conexión de [!DNL Zendesk] los datos le permiten consolidar los informes del servicio de asistencia en [!DNL MBI]. Esto le permite optimizar la asistencia al cliente y monitorizar el rendimiento del servicio de asistencia al cliente junto con sus ingresos.

Conexión de [!DNL Zendesk] es un proceso sencillo de tres pasos:

1. [Abra el [!DNL Zendesk] página credenciales en [!DNL MBI]](#stepone)
1. [Recupere su [!DNL Zendesk] Token de API](#steptwo)
1. [Escriba la [!DNL Zendesk] información de inicio de sesión y inicio de sesión [!DNL MBI]](#stepthree)

Para completar este proceso, deberá abrir dos ventanas o pestañas del explorador: una para [!DNL MBI], el otro para su [!DNL Zendesk] cuenta.

## Abra el [!DNL Zendesk] página credenciales en [!DNL MBI] {#stepone}

1. Vaya a la `Integrations` página debajo de **[!UICONTROL Manage Data** > ** Fuentes de datos **> **Integraciones]**.
1. Haga clic en **[!UICONTROL Add Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en el [!DNL Zendesk] icono. Se abrirá la variable [!DNL Zendesk] credenciales .

## Recupere su [!DNL Zendesk] Token de API {#steptwo}

1. En la ventana o pestaña en la que ha iniciado sesión en su [!DNL Zendesk] haga clic en el icono de Configuración (engranaje) en la esquina inferior izquierda de la pantalla.
1. Cuando la variable `Settings` , busque `Channels` para obtener más información. Haga clic en **[!UICONTROL API]** en esta sección.
1. En el `Token Access` de esta página, haga clic en la casilla de verificación situada junto a `Enabled`. Se mostrará una lista de tokens de API activos.
1. Haga clic en **[!UICONTROL Add New Token]**.
1. Cuando se le pida, introduzca una etiqueta para el token. Se recomienda usar `MBI`, así que sabrá, de un vistazo, qué aplicación está usando el token.
1. Haga clic en **[!UICONTROL Create]**.
1. Se creará un token de API. Copiar este token; se utilizará en el siguiente paso.

## Entrar [!DNL Zendesk] información de inicio de sesión y token de API en [!DNL MBI] {#stepthree}

1. Escriba la [!DNL Zendesk] prefijo del sitio y correo electrónico de inicio de sesión en la [!DNL Zendesk] página credenciales en [!DNL MBI].
1. Introduzca su token de API.
1. Haga clic en **[!UICONTROL Save & Connect]**. Si la conexión se realiza correctamente, una *Conexión correcta* se mostrará en la parte superior de la pantalla.

## Relacionado:

* [Esperado [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
