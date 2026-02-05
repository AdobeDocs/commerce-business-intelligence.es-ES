---
title: Comprobación del estado del ciclo de actualización
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: 776b4b666c47775a7b883a3a6f71c16b4b3bfbad
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Actualización del progreso del ciclo

Cuando inicia sesión en su panel de [!DNL Adobe Commerce Intelligence], existen varias formas de comprobar el estado de su último ciclo de actualización. Todo depende del tipo de [permisos de usuario](../administrator/user-management/user-management.md) que tenga.

## ¿Por qué debería comprobar el estado del ciclo de actualización?

La comprobación del ciclo de actualización de estado resulta útil cuando está auditando los datos de su cuenta de [!DNL Commerce Intelligence]. Si ve [resultados que no cumplen con sus expectativas](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), por ejemplo, las ventas diarias en [!DNL Commerce Intelligence] no coinciden con lo que está viendo en su plataforma de comercio electrónico o en sus [[!DNL Google] ingresos de comercio electrónico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html), puede comprobar el último punto de datos para ver si el problema se resuelve una vez que se completa una actualización.

## [!UICONTROL Read-Only] y [!UICONTROL Standard] usuarios

Los usuarios de `Read-only` pueden iniciar sesión en su panel y ver la actualización reciente de los datos pasando el puntero sobre el icono en la parte superior derecha de la página. Esto muestra cuándo se extrajo el último punto de datos.

![Última marca de tiempo de actualización de datos correcta mostrada en la interfaz](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] usuarios

Los usuarios de `Admin` pueden iniciar sesión en el panel y ver el último punto de datos anterior, junto con un breve icono de estado de las integraciones de su cuenta.

Para obtener más información, los usuarios administradores pueden hacer clic en **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![Página Administrar integraciones de datos que muestra detalles de conexión y estado de actualización](../../mbi/assets/detail-manage-data-integrations.png)

Esta página muestra el estado actual de la actualización y la hora de la última actualización completada.

Si una actualización está en curso, verá un vínculo para solicitar una notificación por correo electrónico una vez que se complete la actualización.

Si una actualización no está en curso, verá un vínculo para forzar el inicio de una actualización.

>[!NOTE]
>
>Si tiene horas de interrupción (tiempo en el que no desea que [!DNL Commerce Intelligence] actualice los datos) establecidas, al forzar una actualización se inicia un ciclo de actualización que no respeta las limitaciones de esas horas de interrupción.


## Compruebe el estado del ciclo de actualización mediante la API

Puede recuperar el ciclo de actualización completado más reciente mediante la **API de estado del ciclo de actualización**.

**Solicitud**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**Respuesta (ejemplo)**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

Para obtener información sobre los parámetros, la autenticación, los errores y los límites de velocidad, consulte [Actualizar la API de estado del ciclo](https://developer.adobe.com/commerce/services/reporting/update-cycle/) en la documentación para desarrolladores.
