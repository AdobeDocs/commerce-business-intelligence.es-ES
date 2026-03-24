---
title: Validación de datos en Mixpanel
description: Aprenda a confirmar que ha sincronizado los mismos datos que están disponibles directamente en Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 134
ht-degree: 0%

---

# Validación de datos en [!DNL Mixpanel]

Cuando [!DNL Adobe Commerce Intelligence] se conecte por primera vez a sus datos de [!DNL Mixpanel], su administrador de cuentas o analista puede solicitarle que proporcione exportaciones de datos de [!DNL Mixpanel] con fines de validación. Esto le permite confirmar que ha sincronizado todos los datos que están disponibles directamente en [!DNL Mixpanel].

## Proceso de exportación de datos: `Events`

1. Visite su sección `Segmentation` y vea `Your Top Events`.

   ![Panel mixto que muestra los eventos principales](../../../assets/your-top-events.png)

1. Seleccione `Past 96 Hours` para el intervalo de tiempo

   ![Selector de intervalo de tiempo del panel mixto que muestra la opción de las últimas 96 horas](../../../assets/past-96-hours.png)

1. Desplácese hasta la parte inferior derecha del informe y exporte un archivo de `.csv`:

   ![Opción de exportación del panel mixto a CSV en el menú](../../../assets/export-csv-mixpanel.png)

1. Envíe el archivo `.csv` al administrador de cuentas o al analista con el que esté trabajando en este proceso de validación.

