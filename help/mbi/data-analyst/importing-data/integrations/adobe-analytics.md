---
title: Conectar Adobe Analytics
description: Aprenda a reunir el enfoque de recorrido integral del cliente de  [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que confía desde [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Conectar [!DNL Adobe Analytics]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![logotipo de Adobe Analytics](../../../assets/adobe-analytic-slogo.png)

La integración de [!DNL Adobe Analytics] para [!DNL Adobe Commerce Intelligence] le permite reunir el enfoque de recorrido de cliente de extremo a extremo de [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que confía de [!DNL Commerce Intelligence]. Esto le ofrece una imagen completa del rendimiento general de su tienda.

Más específicamente, la integración de [!DNL Adobe Analytics] para [!DNL Commerce Intelligence] proporciona funcionalidad para que los comerciantes empiecen a combinar sus conjuntos de datos de [!DNL Adobe Commerce] y [!DNL Adobe Analytics].

- Cree una conexión desde su cuenta existente de [!DNL Adobe Analytics] a [!DNL Commerce Intelligence].

- Seleccione hasta 25 métricas y dimensiones de un grupo de informes para replicarlas en su Data Warehouse.

- Use toda la funcionalidad estándar de [!DNL Commerce Intelligence] para transformar, unirse e informar sobre los datos [!DNL Adobe Analytics] duplicados.

## Requisitos previos de conexión

Se necesita la siguiente información para conectarse:

- [!DNL Adobe Analytics] credenciales de inicio de sesión

- `Name` o `ID` de [!DNL Adobe Analytics] grupo de informes desde el cual replicar datos

- Lista de métricas y dimensiones para replicar en [!DNL Commerce Intelligence]

## Conectando la integración de [!DNL Adobe Analytics] para [!DNL Commerce Intelligence]

1. Vaya a la página `Integrations` en **[!DNL Manage Data** > **Integrations]**.

1. Haga clic en **[!UICONTROL Add an Integration]**.

1. Haga clic en el icono **[!UICONTROL Adobe Analytics]** para acceder a la página que le permite autorizar la conexión de la cuenta de [!DNL Adobe Analytics].

1. Haga clic en **[!UICONTROL Authorize with Adobe Analytics]**.

1. Escriba sus credenciales de [!DNL Adobe Analytics]. Después de la autorización correcta, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de los grupos de informes disponibles. Seleccione el grupo de informes del cual desea importar los datos y haga clic en **[!UICONTROL Continue]**.

1. Se muestra la pantalla de selección de métricas y dimensiones. Seleccione al menos una métrica y una dimensión, hasta un total combinado de 25 métricas y dimensiones. Busque por nombre o desplácese hasta encontrar los componentes y, a continuación, haga clic en las casillas de verificación para seleccionar. Haga clic en **[!UICONTROL Continue]**.

1. El grupo de informes seleccionado se muestra en una tabla. Haga clic en **[!UICONTROL Save]** para confirmar la selección.

1. Informe al [!DNL Commerce Intelligence] [equipo de atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) de que su integración está autorizada y que ejecuta el proceso de conexión inicial por usted.

Una vez que se ejecute el proceso de conexión inicial, la tabla estará disponible en la página Data Warehouse, en la pestaña `All Tables`. Seleccione las columnas que desea duplicar y los datos aparecerán después de la siguiente actualización completa.
