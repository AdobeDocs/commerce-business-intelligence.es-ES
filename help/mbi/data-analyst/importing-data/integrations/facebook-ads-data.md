---
title: Datos esperados de Facebook Ads
description: Obtenga información general sobre las tablas que le recomendamos sincronizar con el almacén de datos
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Esperado [!DNL Facebook Ads] data

![](../../../assets/Facebook_Logo.png)

Después de [conectado el [!DNL Facebook Ads] account](../integrations/facebook-ads.md), puede usar la variable [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis.

En este artículo, le proporcionamos una breve descripción general de las tablas que le recomendamos sincronizar con su almacén de datos. No se trata de una lista completa, ya que hay bastantes subtablas. Solo resaltamos las tablas principales.

## Tablas de campañas de anuncios principales

Estas tablas contienen datos sobre los componentes principales de campañas de publicidad.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

Esta tabla es la tabla principal de las campañas de una [!DNL Facebook Ads] cuenta. Las columnas incluyen `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Esta tabla registra la tabla principal de [!DNL Facebook Ads] Configura en un [!DNL Facebook Ads] cuenta. Las columnas incluyen la publicidad `Campaign id/name` el conjunto de anuncios pertenece a, la información de asignación de presupuestos, tipo de oferta, programación y segmentación de audiencia.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

Esta tabla registra todas las publicidades de un [!DNL Facebook Ads] cuenta. Las columnas incluyen la información de la publicidad, incluidos el conjunto de anuncios y la campaña de publicidad a la que pertenece, la oferta de anuncios, el targeting de anuncios y la referencia a elementos creativos específicos (imagen/texto) que utiliza la publicidad.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

Esta tabla registra todos los elementos creativos utilizados en [!DNL Facebook Ads]. Esto incluye el nombre creativo, la descripción y las direcciones URL de imagen relevantes donde corresponda.

## Tablas de campaña segmentadas

Las siguientes tablas contienen una entrada para cada combinación de campaña, conjunto o anuncio de cada día, segmentada por dimensiones como edad, sexo y país.

### `facebook _ads insights_ (account-id)`

Esta tabla incluye una entrada para cada combinación de campaña/conjunto/anuncio para cada día, junto con estadísticas que incluyen impresiones, clics, coste, cpc, cpm, cpp, ctr, alcance, alcance social y gasto.

### `facebook _ads insights_ (account-id)_~\_actions`

Esta es una subtabla del `facebook_ads_insights_{account_id}` tabla. Incluye datos de conversión para acciones que se producen en función de diferentes campañas.

### `facebook _ads insights country_ (account-id)`

Esta tabla incluye la misma información que la variable `facebook_ads_insights_{account_id}` y lo segmenta por país.

### `facebook ads insights age and gender (account-id)`

Esta tabla incluye la misma información que la variable `facebook_ads_insights_{account_id}` y la segmenta por edad y sexo.

## Relacionado

* [Conexión [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
