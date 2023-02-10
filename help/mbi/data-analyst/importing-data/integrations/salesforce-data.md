---
title: Datos de Salesforce esperados
description: Obtenga información sobre los objetos admitidos y no admitidos en los datos de Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Esperado [!DNL Salesforce] data

[Después de la [!DNL Salesforce] configuración completada](../integrations/salesforce.md), una tabla para cada consulta [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - llamado `sf_/\{sobject-name}` : se creará en el almacén de datos.

>[!NOTE]
>
>La estructura (columnas) de cada tabla depende de los campos contenidos en el objeto.

Para obtener una lista de los objetos disponibles para su organización, consulte la [!DNL Salesforce] [Obtener una documentación de Lista de objetos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Una vez que tenga una lista de objetos, desproteja la [Sección Diagrama de relación de entidades (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) de [!DNL Salesforce] documentación para ver cómo se relacionan las entidades entre sí.

## Objetos no admitidos

En este momento, [!DNL Salesforce] actualmente no expone los siguientes objetos en su API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [¿Qué es un objeto externo?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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

* [Conexión [!DNL Salesforce]](../integrations/salesforce.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
