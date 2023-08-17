---
title: Conectar Adobe Analytics
description: Aprenda a reunir el enfoque de recorrido integral del cliente de [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que se basa [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

El [!DNL Adobe Analytics] integración para [!DNL Adobe Commerce Intelligence] le permite reunir el enfoque del recorrido del cliente de extremo a extremo de [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que se basa [!DNL Commerce Intelligence]. Esto le ofrece una imagen completa del rendimiento general de su tienda.

Más específicamente, la variable [!DNL Adobe Analytics] integración para [!DNL Commerce Intelligence] proporciona funcionalidad para que los comerciantes empiecen a combinar sus [!DNL Adobe Commerce] y [!DNL Adobe Analytics] conjuntos de datos.

- Cree una conexión a partir de la [!DNL Adobe Analytics] cuenta en [!DNL Commerce Intelligence].

- Seleccione hasta 25 métricas y dimensiones de un grupo de informes para replicarlas en su Data Warehouse.

- Usar todos los estándares [!DNL Commerce Intelligence] funcionalidad para transformar, unirse e informar sobre replicados [!DNL Adobe Analytics] datos.

## Requisitos previos de conexión

Se necesita la siguiente información para conectarse:

- [!DNL Adobe Analytics] credenciales de inicio de sesión

- `Name` y/o `ID` de [!DNL Adobe Analytics] grupo de informes desde el que replicar datos

- Lista de métricas y dimensiones para replicar en [!DNL Commerce Intelligence]

## Conexión del [!DNL Adobe Analytics] Integración para [!DNL Commerce Intelligence]

1. Vaya a la `Integrations` página debajo de **[!DNL Manage Data** > **Integrations]**.

1. Haga clic **[!UICONTROL Add an Integration]**.

1. Haga clic en **[!UICONTROL Adobe Analytics]** para acceder a la página que le permite autorizar su [!DNL Adobe Analytics] conexión de cuenta.

1. Haga clic **[!UICONTROL Authorize with Adobe Analytics]**.

1. Introduzca su [!DNL Adobe Analytics] credenciales. Después de la autorización correcta, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de los grupos de informes disponibles. Seleccione el grupo de informes desde el que desea importar los datos y haga clic en **[!UICONTROL Continue]**.

1. Se muestra la pantalla de selección de métricas y dimensiones. Seleccione al menos una métrica y una dimensión, hasta un total combinado de 25 métricas y dimensiones. Busque por nombre o desplácese hasta encontrar los componentes y, a continuación, haga clic en las casillas de verificación para seleccionar. Haga clic **[!UICONTROL Continue]**.

1. El grupo de informes seleccionado se muestra en una tabla. Clic **[!UICONTROL Save]** para confirmar la selección.

1. Informe al [!DNL Commerce Intelligence] [Equipo de soporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) Compruebe que la integración está autorizada y que ejecutan el proceso de conexión inicial por usted.

Una vez ejecutado el proceso de conexión inicial, la tabla estará disponible en la página Data Warehouse, en `All Tables` pestaña. Seleccione las columnas que desea duplicar y los datos aparecerán después de la siguiente actualización completa.
