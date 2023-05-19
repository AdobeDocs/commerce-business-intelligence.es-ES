---
title: Datos esperados de Google Adwords
description: Descubra cómo puede utilizar el Administrador de Datas Warehouse para rastrear fácilmente campos de datos relevantes para su análisis.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Previsto [!DNL Google Adwords] datos

Después [ha conectado su [!DNL Google Adwords] account](../integrations/google-adwords.md), puede utilizar el [Administrador de Datas Warehouse](../../data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes para su análisis.

Aquí puede ver dos tablas disponibles para la replicación en la Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

El `campaigns` tabla *debe usarse de forma predeterminada*, para que pueda empezar sincronizando todos los campos relevantes de esa tabla.

El `adwords` contiene cuatro columnas que no están en la `campaigns` tabla:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Siempre que esté interesado en realizar un análisis que tenga en cuenta estos atributos, debe utilizar la variable `adwords` tabla.

>[!IMPORTANT]
>
>Esta tabla excluye las filas en las que se encuentran las cuatro columnas `null`.

A continuación se muestra un vistazo al esquema esperado para ambas tablas.

## [!DNL Campaigns] tabla

El `campaigns` La tabla contiene las columnas siguientes:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | ID de la cuenta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nombre de la campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |

{style="table-layout:auto"}

## [!DNL AdWords] tabla

El `adwords` La tabla contiene las columnas siguientes:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | ID de la cuenta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nombre de la campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |
| `keyword` | La palabra clave de la campaña |
| `adContent` | Primera línea del texto de la campaña en línea |
| `adDestinationUrl` | La URL a la que se [!DNL Adwords] tráfico de referencia de anuncios |
| `adGroup` | El nombre del [!DNL Adwords] grupo de publicidad |

{style="table-layout:auto"}

Con estos datos, puede empezar a crear [métricas](../../../data-user/reports/ess-manage-data-metrics.md) y [informes](../../../tutorials/using-visual-report-builder.md) en función de los datos de gasto y [vincúlelo a sus ingresos de por vida para calcular el ROI](../../analysis/roi-ad-camp.md).

## Tablas consolidadas

[!DNL Adobe] recomienda crear un `consolidated ad spend` para combinar los datos de todas las fuentes de publicidad múltiples en una sola tabla. Esto le permite utilizar un único conjunto de métricas para el análisis de publicidad.

Si no tiene una tabla consolidada y crea un hermoso panel en la `adwords` , debe replicar los informes o crear métricas duplicadas para comparar esos datos con sus [!DNL Facebook Ads] datos. El uso de una tabla consolidada le permite incorporar [!DNL Facebook Ads] datos con los existentes [!DNL Adwords] informes. También puede segmentar por plataforma de publicidad.

Si ya ha sincronizado los campos anteriores, [Contáctenos.](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para consolidar su gasto en publicidad.
