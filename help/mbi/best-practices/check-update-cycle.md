---
title: Comprobación del estado del ciclo de actualización
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Actualizar progreso del ciclo

Cuando inicie sesión en su [!DNL MBI] tablero, hay varias formas de comprobar el estado del último ciclo de actualización. Todo depende del tipo de [permisos de usuario](../administrator/user-management/user-management.md) tú sí.

## ¿Por qué debería comprobar el estado del ciclo de actualización?

La comprobación del ciclo de actualización de estado es útil cuando audita los datos en su [!DNL MBI] cuenta. Si ve [resultados que no satisfacen sus expectativas](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), por ejemplo, ventas diarias en [!DNL MBI] no coinciden con lo que está viendo en su plataforma de comercio electrónico o en su [[!DNL Google] ingresos por comercio electrónico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) puede comprobar el último punto de datos para ver si el problema se resolverá una vez completada la actualización.

## [!UICONTROL Read-Only] y [!UICONTROL Standard]** Usuarios

`Read-only` los usuarios pueden iniciar sesión en su panel y ver la fecha en la que se han actualizado los datos pasando el cursor sobre el icono en la parte superior derecha de la página. Esto mostrará cuándo se extrajo el último punto de datos.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Usuarios

`Admin` los usuarios pueden iniciar sesión en el tablero y ver el último punto de datos anterior, junto con un breve icono de estado de las integraciones de su cuenta.

Para obtener más información, los usuarios administradores pueden hacer clic en **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Esta página muestra el estado de la actualización actual y la hora de la última actualización completada.

Si hay una actualización en curso, verá un vínculo para solicitar una notificación por correo electrónico una vez que se complete la actualización.

Si una actualización no está en curso, aparece un vínculo para forzar el inicio de una actualización.

>[!NOTE]
>
>Si tiene horas de interrupción (hora en la que no desea [!DNL MBI] para actualizar los datos), forzar una actualización iniciará un ciclo de actualización que no respete las limitaciones de esas horas de interrupción.
