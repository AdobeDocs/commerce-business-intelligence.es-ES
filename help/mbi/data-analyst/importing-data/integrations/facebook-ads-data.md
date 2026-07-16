---
title: Datos previstos de Facebook Ads
description: Obtenga información general breve sobre las tablas que se recomiendan para sincronizar con su Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: c8d7097b4f841a4fe8c5777f207ea0ea53202a0f
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 0%

---

# Se esperaban [!DNL Facebook Ads] datos

Una vez que hayas [conectado tu [!DNL Facebook Ads] cuenta](../integrations/facebook-ads.md), puedes usar el [Administrador de Data Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes y analizarlos.

En este tema se ofrece una breve descripción general de las tablas que Adobe recomienda sincronizar con su Data Warehouse. Esto solo resalta las tablas principales, ya que hay bastantes subtablas.

## Tablas de campañas de anuncios principales

Estas tablas contienen datos sobre los componentes principales de la campaña de publicidad.

### `facebook _campaigns_ (account-id)`

[`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Esta tabla es la tabla principal de campañas en una cuenta de [!DNL Facebook Ads]. Las columnas incluyen `campaign id`, `name`, `status (active/paused)`, `objective`.

### `facebook _adsets_ (account-id)`

[`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Este registro de tabla es la tabla principal de [!DNL Facebook Ads] conjuntos en una cuenta [!DNL Facebook Ads]. Las columnas incluyen el anuncio `Campaign id/name` al que pertenece el conjunto de anuncios, la información de presupuesto, tipo de oferta, programación y segmentación de audiencia.

### `facebook _ads_ (account-id)`

[`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Esta tabla registra todos los anuncios en una cuenta de [!DNL Facebook Ads]. Las columnas incluyen la información de la publicidad, incluidos el conjunto de anuncios y la campaña de publicidad a la que pertenece, las ofertas de publicidad, la segmentación de publicidad y la referencia a elementos creativos específicos (imagen/texto) que utiliza la publicidad.

### `facebook _adcreative_ (account-id)`

[`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

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
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
