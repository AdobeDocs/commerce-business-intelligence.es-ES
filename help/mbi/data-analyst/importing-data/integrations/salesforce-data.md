---
title: Datos Salesforce esperados
description: Obtenga información sobre los objetos admitidos y no admitidos en los datos de Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Se esperaban [!DNL Salesforce] datos

Una vez completada la instalación de [[!DNL Salesforce] setup](../integrations/salesforce.md), se creará en su Data Warehouse una tabla para cada [objeto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) que se pueda consultar, denominada `sf_/\{sobject-name}`.

>[!NOTE]
>
>La estructura (columnas) de cada tabla depende de los campos contenidos en el objeto.

Para obtener una lista de los objetos disponibles para su organización, consulte la [!DNL Salesforce] [Obtener una lista de objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Una vez que tenga una lista de objetos, consulte la [sección Diagrama de relación de entidades (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de la documentación de [!DNL Salesforce] para ver cómo se relacionan las entidades entre sí.

## Objetos no admitidos

Actualmente, [!DNL Salesforce] no expone los siguientes objetos en su API:

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
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
