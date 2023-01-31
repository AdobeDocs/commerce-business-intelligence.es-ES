---
title: Datos esperados de Google Adwords
description: Aprenda a utilizar el Administrador de Datas Warehouse para rastrear fácilmente los campos de datos relevantes para el análisis.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Datos esperados de Google Adwords

Después [ha conectado su [!DNL Google Adwords] account](../integrations/google-adwords.md), puede usar la variable [Administrador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis.

En este caso, verá dos tablas disponibles para la replicación en su almacén de datos: `campaigns[account-id]` y `adwords[account-id]`.

La variable `campaigns` tabla *debe usarse de forma predeterminada*, de modo que pueda empezar sincronizando todos los campos relevantes de esa tabla.

La variable `adwords` La tabla contiene cuatro columnas que no están en la `campaigns` tabla:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

Siempre que le interese realizar un análisis que tenga en cuenta estos atributos, debe usar la variable `adwords` tabla.

>[!IMPORTANT]
>
>Esta tabla excluirá filas donde las cuatro columnas están `null`.

A continuación, se muestra un vistazo al esquema esperado para ambas tablas:

## `Campaigns` tabla

La variable `campaigns` la tabla contiene las columnas siguientes:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | El ID de cuenta |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nombre de campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |

{style=&quot;table-layout:auto&quot;}

## Tabla AdWords

La variable `adwords` la tabla contiene las columnas siguientes:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | El ID de cuenta |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nombre de campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |
| `keyword` | Palabra clave de la campaña |
| `adContent` | Primera línea del texto de la campaña en línea |
| `adDestinationUrl` | La dirección URL a la que se llama [!DNL Adwords] tráfico de anuncios referidos |
| `adGroup` | El nombre del [!DNL Adwords] grupo de publicidad |

{style=&quot;table-layout:auto&quot;}

Con estos datos, puede empezar a crear [métricas ](../../../data-user/reports/ess-manage-data-metrics.md) y [informes](../../../tutorials/using-visual-report-builder.md) en función de los datos de gasto y [únela a sus ingresos de por vida para calcular el ROI](../../analysis/roi-ad-camp.md).

## Tablas consolidadas

Siempre se recomienda crear un `consolidated ad spend` para combinar los datos de todas las fuentes publicitarias múltiples en una sola tabla. Esto le permite utilizar un único conjunto de métricas para el análisis de publicidad.

Sin una tabla consolidada, si crea un panel hermoso en la `adwords` , debe replicar los informes o crear métricas duplicadas para comparar esos datos con sus [!DNL Facebook Ads] datos. El uso de una tabla consolidada le permite incorporar sin problemas [!DNL Facebook Ads] con los datos existentes [!DNL Adwords] informes. (No se preocupe: también tiene la capacidad de segmentar por plataforma de publicidad).

Si ya ha sincronizado los campos anteriores, póngase en contacto con nosotros para consolidar su gasto en publicidad.
