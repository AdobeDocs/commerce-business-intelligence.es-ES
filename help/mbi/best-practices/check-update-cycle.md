---
title: Comprobación del estado del ciclo de actualización
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Actualización del progreso del ciclo

Al iniciar sesión en su [!DNL MBI] , existen varias formas de comprobar el estado del último ciclo de actualización. Todo depende del tipo de [permisos de usuario](../administrator/user-management/user-management.md) que usted tiene.

## ¿Por qué debería comprobar el estado del ciclo de actualización?

La comprobación del ciclo de actualización de estado resulta útil cuando se auditan los datos en su [!DNL MBI] cuenta. Si ve [resultados que no cumplen con sus expectativas](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), por ejemplo, las ventas diarias en [!DNL MBI] no coinciden con lo que se ve en su plataforma de comercio electrónico o en su [[!DNL Google] ingresos por comercio electrónico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) puede comprobar el último punto de datos para ver si el problema se resuelve una vez que se completa una actualización.

## [!UICONTROL Read-Only] y [!UICONTROL Standard]** usuarios

`Read-only` Los usuarios de pueden iniciar sesión en su panel y ver la actualización reciente de los datos pasando el ratón por encima del icono en la parte superior derecha de la página. Esto muestra cuándo se extrajo el último punto de datos.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Usuarios

`Admin` los usuarios pueden iniciar sesión en el tablero y ver el último punto de datos anterior, junto con un breve icono de estado de las integraciones de su cuenta.

Para obtener más información, los usuarios administradores pueden hacer clic en **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Esta página muestra el estado actual de la actualización y la hora de la última actualización completada.

Si una actualización está en curso, verá un vínculo para solicitar una notificación por correo electrónico una vez que se complete la actualización.

Si una actualización no está en curso, verá un vínculo para forzar el inicio de una actualización.

>[!NOTE]
>
>Si tiene horas de interrupción (tiempo en el que no desea [!DNL MBI] para actualizar los datos), al forzar una actualización se inicia un ciclo de actualización que no respeta las limitaciones de esas horas de interrupción.
