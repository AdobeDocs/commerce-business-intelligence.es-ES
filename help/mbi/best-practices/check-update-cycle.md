---
title: Comprobación del estado del ciclo de actualización
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Developer, User
feature: Dashboards
TQID: https://experienceleague.adobe.com/FAK0W9Qf002Xsug4GLlHs3ChiliC9UXHHrF-Wdo0reo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 0%

---

# Actualización del progreso del ciclo

Cuando inicia sesión en su panel de [!DNL Adobe Commerce Intelligence], existen varias formas de comprobar el estado de su último ciclo de actualización. Todo depende del tipo de [permisos de usuario](../administrator/user-management/user-management.md) que tenga.

## ¿Por qué debería comprobar el estado del ciclo de actualización?

La comprobación del ciclo de actualización de estado resulta útil cuando está auditando los datos de su cuenta de [!DNL Commerce Intelligence]. Si ve [resultados que no cumplen con sus expectativas](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), por ejemplo, las ventas diarias en [!DNL Commerce Intelligence] no coinciden con lo que está viendo en su plataforma de comercio electrónico o en sus [[!DNL Google] ingresos de comercio electrónico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=es), puede comprobar el último punto de datos para ver si el problema se resuelve una vez que se completa una actualización.

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
