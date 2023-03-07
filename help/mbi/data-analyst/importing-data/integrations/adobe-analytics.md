---
title: Conectar Adobe Analytics
description: Aprenda a reunir el enfoque de recorrido integral del cliente de [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que se basa [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

El [!DNL Adobe Analytics] integración para [!DNL MBI] le permite reunir el enfoque del recorrido del cliente de extremo a extremo de [!DNL Adobe Analytics] y el enfoque de comercio electrónico en el que se basa [!DNL MBI]. Esto le ofrece una imagen completa del rendimiento general de su tienda.

Más específicamente, la variable [!DNL Adobe Analytics] integración para [!DNL MBI] proporciona funcionalidad para que los comerciantes empiecen a combinar sus conjuntos de datos de Commerce y Analytics.
- Cree una conexión a partir de la [!DNL Adobe Analytics] cuenta en [!DNL MBI].
- Seleccione hasta 25 métricas y dimensiones de un grupo de informes para replicarlas en su [!DNL MBI] Data Warehouse.
- Usar todos los estándares [!DNL MBI] funcionalidad para transformar, unirse e informar sobre replicados [!DNL Adobe Analytics] datos.

## Requisitos previos de conexión

Se necesita la siguiente información para conectarse:
- [!DNL Adobe Analytics] credenciales de inicio de sesión
- `Name` y/o `ID` de [!DNL Adobe Analytics] grupo de informes desde el que replicar datos
- Lista de métricas y dimensiones para replicar en [!DNL MBI]

## Conexión del [!DNL Adobe Analytics] Integración para MBI

1. Vaya a la `Integrations` página debajo de **[!DNL Manage Data** > **Integrations]**.
1. Clic **[!UICONTROL Add an Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en **[!UICONTROL Adobe Analytics]** para acceder a la página que le permite autorizar su [!DNL Adobe Analytics] conexión de cuenta.
1. Clic **[!UICONTROL Authorize with Adobe Analytics]**.
1. Introduzca su [!DNL Adobe Analytics] credenciales. Después de la autorización correcta, se le redirigirá de nuevo a [!DNL MBI].
1. Se muestra una lista de los grupos de informes disponibles. Seleccione el grupo de informes desde el que desea importar los datos y haga clic en **[!UICONTROL Continue]**.
1. Se muestra la pantalla de selección de métricas y dimensiones. Seleccione al menos una métrica y una dimensión, hasta un total combinado de 25 métricas y dimensiones. Busque por nombre o desplácese hasta encontrar los componentes y, a continuación, haga clic en las casillas de verificación para seleccionar. Clic **[!UICONTROL Continue]**.
1. El grupo de informes seleccionado se muestra en una tabla. Clic **[!UICONTROL Save]** para confirmar la selección.
1. Informe al [!DNL MBI] Equipo de soporte: Verifique que la integración esté autorizada y ejecute el proceso de conexión inicial por usted.

Una vez ejecutado el proceso de conexión inicial, la tabla estará disponible en la página Data Warehouse, en `All Tables` pestaña. Seleccione las columnas que desea duplicar y los datos aparecerán después de la siguiente actualización completa.
