---
title: Datos del Mixpanel esperados
description: Explore las tablas de datos principales que se pueden importar desde Mixpanel a su [!DNL Commerce Intelligence] cuenta.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Previsto [!DNL Mixpanel] datos

Después [ha conectado su [!DNL Mixpanel] account](../integrations/mixpanel.md), puede utilizar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes para su análisis.

En este tema se exploran las tablas de datos principales desde las que se puede importar [!DNL Mixpanel] en su [!DNL Commerce Intelligence] cuenta. Las siguientes tablas se crearán en la Data Warehouse después de conectarse [!DNL Mixpanel]. Para ver todos los campos disponibles para el seguimiento, haga clic en los vínculos de la columna de nombre de tabla.

>[!NOTE]
>
>Debido a las limitaciones de la [!DNL Mixpanel] API, datos históricos: datos anteriores a siete (7) días desde la fecha de conexión a [!DNL Commerce Intelligence] - no se replica.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Esta tabla contiene datos de evento sin procesar, incluido el evento, las fechas del evento y el bloque de plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Esta tabla contiene datos sobre los canales, incluido el ID de canal, la longitud del canal (número de días que el usuario debe completar el canal) y las fechas de inicio y finalización del canal. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene datos de People Analytics, incluidos los ID de sesión, la página y la información de usuario, así como la fecha y la hora en que se vio por última vez al usuario. |

{style="table-layout:auto"}

## Documentación relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
