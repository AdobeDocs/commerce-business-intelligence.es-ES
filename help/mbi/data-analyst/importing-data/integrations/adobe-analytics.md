---
title: Conectar Adobe Analytics
description: Aprenda a reunir el enfoque de recorrido integral del cliente de  [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que confía desde [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Conectar [!DNL Adobe Analytics]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

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
