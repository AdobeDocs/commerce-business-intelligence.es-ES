---
title: Importar otros datos de gasto en publicidad
description: Obtenga información sobre cómo importar datos de gasto en publicidad o sin conexión en [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/jx-MMry1-XGeM4htPkH6GC1Et5nYjyD7aWn3p-nmcC8'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%
---
# Importar otros datos de gasto en publicidad

La carga de los datos de gasto en publicidad le permite medir el retorno de la inversión de la campaña combinando el costo de la publicidad con el `customer lifetime value (CLV)` de usuarios adquiridos de las campañas.

## Carga de datos de costes de publicidad

El primer paso para analizar los datos de gasto en publicidad es obtener los datos. Dado que la mayoría de las plataformas de publicidad le permiten exportar informes, Adobe recomienda exportar los datos sin procesar de su plataforma de publicidad y cargarlos directamente en [!DNL Commerce Intelligence] sin ninguna manipulación. Puede realizar operaciones en los datos de su Data Warehouse, por lo que no es necesario duplicar los esfuerzos.

Después de haber exportado los datos de gasto en publicidad, use la característica [`File Upload` &#x200B;](../connecting-data/using-file-uploader.md) para llevar los datos a Data Warehouse. Con el tiempo, puede cargar nuevos datos en la misma tabla [!DNL Commerce Intelligence].

## Fuentes sin conexión

Además de sus campañas en línea, es posible que también tenga anuncios sin conexión, como en la radio o en un cartel. Para tener en cuenta estos casos, puede cargar manualmente una hoja de cálculo con los datos de costo en [!DNL Commerce Intelligence].

La estructura de tabla que se explora a continuación se recomienda al crear un archivo de `.csv` para registrar y gastar datos. También se adjunta un archivo de plantilla al final de este tema para que sirva de ejemplo. Las columnas recomendadas son:

* `ID`: es un identificador único para cada fila de datos que la base de datos utiliza como clave principal. Debe ser diferente para cada fila.
* `Date`: fecha en la que se ejecutó la campaña, en formato aaaa-mm-dd.
* `Amount` - Esta es la cantidad que gastó en la campaña.
* `campaign`: nombre de la campaña. Si usa [!DNL Google Analytics] para hacer un seguimiento de los demás datos de gasto en publicidad, debe coincidir con el nombre utm\_campaign.
* `source`: este es el nombre de origen. Si usa [!DNL Google Analytics], debe coincidir con el nombre de `utm_source`.
* `other` (opcional): también puede incorporar columnas adicionales que le ayuden a segmentar campañas y costos. También puede ser una forma de resumir varios nombres de campañas de UTM diferentes en una sola campaña coherente con fines de seguimiento. En lugar de configurarlo manualmente, podría ser bueno usar una Búsqueda en V en una segunda hoja para hacer coincidir cada Nombre de campaña con el Otro nombre y crear un informe aquí de forma dinámica.

## Relacionado

* [Conectar  [!DNL AdWords] datos](../integrations/google-adwords.md)
* [Aumentar el retorno de la inversión en campañas publicitarias](../../analysis/roi-ad-camp.md)
