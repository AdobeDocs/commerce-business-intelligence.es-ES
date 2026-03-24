---
title: Se esperaban [!DNL Google ECommerce]datos
description: Descubra qué tipos de datos se comparten con Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# Se esperaban [!DNL Google ECommerce] datos

Una vez que la cuenta de [!DNL Google ECommerce] se haya conectado correctamente a [!DNL Commerce Intelligence], el sistema comenzará a importar datos en una tabla denominada `ecommerce`. Esta tabla registra una fila de datos para cada transacción. Esto incluye las siguientes columnas de datos en el nivel de pedido:

| Nombre de columna | Descripción |
|-----|-----|
| `\_id` | Esta columna es la clave principal. |
| `accountId` | Esta columna contiene el identificador de cuenta asociado con su cuenta de comercio electrónico [!DNL Google Analytics]. |
| `profileName` | Esta columna contiene el nombre de perfil [!DNL Google Analytics]. |
| `profileId` | Esta columna contiene su ID de perfil [!DNL Google Analytics]. |
| `socialNetwork` | Esta columna contiene el nombre de la red social (por ejemplo, [!DNL Facebook] o [!DNL YouTube]) |
| `campaign` | Esta columna contiene el nombre de la campaña (por ejemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Esta columna contiene el nombre del medio (por ejemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Esta columna contiene el nombre de origen. (por ejemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Esta columna contiene la descripción de la palabra clave (por ejemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Esta columna contiene el ID de pedido. Se utiliza para unir los datos de referencia a los datos de pedidos. |
| `updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. |

{style="table-layout:auto"}
