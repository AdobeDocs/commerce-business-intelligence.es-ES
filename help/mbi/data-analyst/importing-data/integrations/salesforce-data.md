---
title: Datos previstos de Salesforce
description: Obtenga información sobre los objetos admitidos y no admitidos en los datos de Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Previsto [!DNL Salesforce] datos

[Después del [!DNL Salesforce] la configuración ha finalizado](../integrations/salesforce.md), una tabla para cada consulta [objeto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - con nombre `sf_/\{sobject-name}` : se crea en la Data Warehouse.

>[!NOTE]
>
>La estructura (columnas) de cada tabla depende de los campos contenidos en el objeto.

Para obtener una lista de los objetos disponibles para su organización, consulte la [!DNL Salesforce] [Obtener una documentación de lista de objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Una vez que tenga una lista de objetos, extraiga el [Diagrama de relación de entidades (ERD), sección](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] para ver cómo se relacionan las entidades entre sí.

## Objetos no admitidos

Actualmente, [!DNL Salesforce] actualmente no expone los siguientes objetos en su API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [¿Qué es un objeto externo?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Relacionado:

* [Conectando [!DNL Salesforce]](../integrations/salesforce.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
