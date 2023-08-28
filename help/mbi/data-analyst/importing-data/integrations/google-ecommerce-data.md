---
title: Previsto[!DNL Google ECommerce]datos
description: Descubra qué tipos de datos se comparten con Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Previsto [!DNL Google ECommerce] datos

Después de su [!DNL Google ECommerce] la cuenta se ha conectado correctamente a [!DNL Commerce Intelligence], el sistema empezará a importar datos en una tabla titulada `ecommerce`. Esta tabla registra una fila de datos para cada transacción. Esto incluye las siguientes columnas de datos en el nivel de pedido:

| Nombre de columna | Descripción |
|-----|-----|
| `\_id` | Esta columna es la clave principal. |
| `accountId` | Esta columna contiene el ID de cuenta asociado con su [!DNL Google Analytics] Cuenta de comercio electrónico. |
| `profileName` | Esta columna contiene su [!DNL Google Analytics] nombre del perfil. |
| `profileId` | Esta columna contiene su [!DNL Google Analytics] ID de perfil. |
| `socialNetwork` | Esta columna contiene el nombre de la red social (por ejemplo, [!DNL Facebook], o [!DNL YouTube]) |
| `campaign` | Esta columna contiene el nombre de la campaña (por ejemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Esta columna contiene el nombre del medio (por ejemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Esta columna contiene el nombre de origen. (por ejemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Esta columna contiene la descripción de la palabra clave (por ejemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Esta columna contiene el ID de pedido. Se utiliza para unir los datos de referencia a los datos de pedidos. |
| `updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. |

{style="table-layout:auto"}
