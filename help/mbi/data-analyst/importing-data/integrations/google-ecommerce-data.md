---
title: Esperado[!DNL Google ECommerce]data
description: Descubra qué tipos de datos se comparten con Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Esperado[!DNL Google ECommerce] data

Después de [!DNL Google ECommerce] la cuenta está conectada correctamente a [!DNL MBI], el sistema empezará a importar datos en una tabla titulada `ecommerce`. En esta tabla se registrará una fila de datos para cada transacción. Esto incluye las siguientes columnas de datos de nivel de pedido:

| Nombre de columna | Descripción |
|-----|-----|
| `\_id` | Esta columna es la clave principal. |
| `accountId` | Esta columna contiene el ID de cuenta asociado con su [!DNL Google Analytics] Cuenta de comercio electrónico. |
| `profileName` | Esta columna contiene su [!DNL Google Analytics] nombre del perfil. |
| `profileId` | Esta columna contiene su [!DNL Google Analytics] ID de perfil. |
| `socialNetwork` | Esta columna contiene el nombre de la red social (por ejemplo, [!DNL Facebook]o [!DNL YouTube]) |
| `campaign` | Esta columna contiene el nombre de la campaña (por ejemplo, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Esta columna contiene el nombre medio (por ejemplo, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Esta columna contiene el nombre del origen. (por ejemplo, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Esta columna contiene la descripción de la palabra clave (por ejemplo, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Esta columna contiene el ID de pedido. Se utilizará para unir los datos de referente a los datos de pedidos. |
| `updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. |

{style=&quot;table-layout:auto&quot;}
