---
title: Datos del Mixpanel esperados
description: Explore las tablas de datos principales que se pueden importar desde Mixpanel a su cuenta de  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# Se esperaban [!DNL Mixpanel] datos

Después de [haber conectado tu [!DNL Mixpanel] cuenta](../integrations/mixpanel.md), puedes usar [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis.

En este tema se exploran las tablas de datos principales que puede importar de [!DNL Mixpanel] a su cuenta de [!DNL Commerce Intelligence]. Las siguientes tablas se crearán en su Data Warehouse después de conectar [!DNL Mixpanel]. Para ver todos los campos disponibles para el seguimiento, haga clic en los vínculos de la columna de nombre de tabla.

>[!NOTE]
>
>Debido a las limitaciones de la API [!DNL Mixpanel], los datos históricos (datos anteriores a siete (7) días desde la fecha de conexión a [!DNL Commerce Intelligence]) no se replican.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Esta tabla contiene datos de evento sin procesar, incluido el evento, las fechas del evento y el bloque de plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Esta tabla contiene datos sobre los canales, incluido el funnel ID, la duración de la funnel (# de días que el usuario debe completar la funnel) y las fechas de inicio y finalización de la funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene datos de People Analytics, incluidos los ID de sesión, la página y la información de usuario, así como la fecha y la hora en que se vio por última vez al usuario. |

{style="table-layout:auto"}

## Documentación relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
