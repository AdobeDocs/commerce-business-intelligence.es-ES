---
title: Datos previstos de Facebook Ads
description: Obtenga información general breve sobre las tablas que se recomiendan para sincronizar con su Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Se esperaban [!DNL Facebook Ads] datos

Una vez que hayas [conectado tu [!DNL Facebook Ads] cuenta](../integrations/facebook-ads.md), puedes usar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes y analizarlos.

En este tema se ofrece una breve descripción general de las tablas que el Adobe recomienda sincronizar con la Data Warehouse. Esto solo resalta las tablas principales, ya que hay bastantes subtablas.

## Tablas de campañas de anuncios principales

Estas tablas contienen datos sobre los componentes principales de la campaña de publicidad.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Esta tabla es la tabla principal de campañas en una cuenta de [!DNL Facebook Ads]. Las columnas incluyen `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Este registro de tabla es la tabla principal de [!DNL Facebook Ads] conjuntos en una cuenta [!DNL Facebook Ads]. Las columnas incluyen el anuncio `Campaign id/name` al que pertenece el conjunto de anuncios, la información de presupuesto, tipo de oferta, programación y segmentación de audiencia.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Esta tabla registra todos los anuncios en una cuenta de [!DNL Facebook Ads]. Las columnas incluyen la información de la publicidad, incluidos el conjunto de anuncios y la campaña de publicidad a la que pertenece, las ofertas de publicidad, la segmentación de publicidad y la referencia a elementos creativos específicos (imagen/texto) que utiliza la publicidad.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Esta tabla registra los elementos creativos utilizados en [!DNL Facebook Ads]. Creativos incluye un nombre creativo, una descripción y direcciones URL de imagen relevantes cuando corresponda.

## Tablas de campaña segmentadas

Las siguientes tablas contienen una entrada para cada combinación de campaña, conjunto o publicidad de cada día, segmentada por dimensiones como edad, sexo y país.

### `facebook _ads insights_ (account-id)`

Esta tabla incluye una entrada para cada combinación de campaña, conjunto/anuncio para cada día, junto con estadísticas que incluyen impresiones, clics, coste, cpc, cpm, cpp, ctr, alcance, alcance social y gasto.

### `facebook _ads insights_ (account-id)_~\_actions`

Esta es una subtabla de la tabla `facebook_ads_insights_{account_id}`. Incluye datos de conversión para acciones que se producen en función de diferentes campañas.

### `facebook _ads insights country_ (account-id)`

Esta tabla incluye la misma información que la tabla `facebook_ads_insights_{account_id}` y la segmenta por país.

### `facebook ads insights age and gender (account-id)`

Esta tabla incluye la misma información que la tabla `facebook_ads_insights_{account_id}` y la segmenta por edad y sexo.

## Relacionado

* [Conectando [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
