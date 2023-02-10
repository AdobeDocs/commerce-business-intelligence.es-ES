---
title: Datos esperados de los paneles mixtos
description: Explore las tablas de datos principales que puede importar desde Mixpanel a su [!DNL MBI] cuenta.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Esperado [!DNL Mixpanel] data

Después [ha conectado su [!DNL Mixpanel] account](../integrations/mixpanel.md), puede usar la variable [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis.

En este artículo, exploramos las principales tablas de datos desde las que puede importar [!DNL Mixpanel] en el [!DNL MBI] cuenta. Las siguientes tablas se crearán en el almacén de datos después de conectar Mixpanel. Para ver todos los campos disponibles para seguimiento, haga clic en los vínculos en la columna nombre de tabla.

>[!NOTE]
>
>Debido a las limitaciones de la variable [!DNL Mixpanel] API, datos históricos: datos anteriores a siete (7) días desde la fecha de conexión a [!DNL MBI] - no se replicará.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Esta tabla contiene datos de eventos sin procesar, incluidos el evento, las fechas del evento y el bloque de la plataforma. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Esta tabla contiene datos sobre los canales, incluido el ID del canal, la duración del canal (número de días que el usuario debe completar el canal) y las fechas de inicio y finalización del canal. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Contiene datos de People Analytics, incluidos los ID de sesión, la página y la información de usuario, así como la fecha y la hora en que se vio por última vez el usuario. |

{style=&quot;table-layout:auto&quot;}

## Documentación relacionada

* [Conexión [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
