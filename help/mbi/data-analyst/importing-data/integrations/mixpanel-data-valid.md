---
title: Validación de datos en Mixpanel
description: Aprenda a confirmar que ha sincronizado los mismos datos que están disponibles directamente en Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Validación de datos en [!DNL Mixpanel]

Cuando [!DNL Adobe Commerce Intelligence] se conecte por primera vez a sus datos de [!DNL Mixpanel], su administrador de cuentas o analista puede solicitarle que proporcione exportaciones de datos de [!DNL Mixpanel] con fines de validación. Esto le permite confirmar que ha sincronizado todos los datos que están disponibles directamente en [!DNL Mixpanel].

## Proceso de exportación de datos: `Events`

1. Visite su sección `Segmentation` y vea `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Seleccione `Past 96 Hours` para el intervalo de tiempo

   ![](../../../assets/past-96-hours.png)

1. Desplácese hasta la parte inferior derecha del informe y exporte un archivo de `.csv`:

   ![](../../../assets/export-csv-mixpanel.png)

1. Envíe el archivo `.csv` al administrador de cuentas o al analista con el que esté trabajando en este proceso de validación.
