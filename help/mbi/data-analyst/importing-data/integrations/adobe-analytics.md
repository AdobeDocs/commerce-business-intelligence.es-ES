---
title: Conectar Adobe Analytics
description: Aprenda a unir el enfoque de recorrido del cliente de extremo a extremo de [!DNL Adobe Analytics] y el enfoque del comercio electrónico del que confía [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

La variable [!DNL Adobe Analytics] integración para [!DNL MBI] le permite unir el enfoque de recorrido de cliente de extremo a extremo de [!DNL Adobe Analytics] y el enfoque del comercio electrónico del que confía [!DNL MBI], para obtener una imagen más completa del rendimiento general de su tienda.

Más específicamente, la variable [!DNL Adobe Analytics] integración para [!DNL MBI] proporciona funcionalidad para que los comerciantes empiecen a combinar sus conjuntos de datos de Commerce y Analytics.
- Cree una conexión a partir de su [!DNL Adobe Analytics] account en [!DNL MBI].
- Seleccione hasta 25 métricas y dimensiones de un grupo de informes para replicarlas en su [!DNL MBI] almacén de datos.
- Utilice todos los estándares [!DNL MBI] funcionalidad para transformar, unir e informar sobre la replicación [!DNL Adobe Analytics] datos.

## Requisitos previos de conexión

Se necesita la siguiente información para conectar:
- [!DNL Adobe Analytics] credenciales de inicio de sesión
- `Name` y/o `ID` de [!DNL Adobe Analytics] grupo de informes desde el que duplicar datos
- Lista de métricas y dimensiones en las que duplicar [!DNL MBI]

## Conexión de [!DNL Adobe Analytics] Integración para MBI

1. Vaya a la `Integrations` página debajo de **[!DNL Manage Data** > **Integrations]**.
1. Haga clic en **[!UICONTROL Add an Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en el **[!UICONTROL Adobe Analytics]** para acceder a la página que le permite autorizar su [!DNL Adobe Analytics] conexión de cuenta.
1. Haga clic en **[!UICONTROL Authorize with Adobe Analytics]**.
1. Escriba la [!DNL Adobe Analytics] credenciales. Después de una autorización correcta, se le redirige de nuevo a [!DNL MBI].
1. Se muestra una lista de los grupos de informes disponibles. Seleccione el grupo de informes desde el que desea importar los datos y haga clic en **[!UICONTROL Continue]**.
1. Aparece la pantalla de selección de métricas y dimensiones. Seleccione al menos una métrica y al menos una dimensión, hasta un total combinado de 25 métricas y dimensiones. Busque por nombre o desplácese para encontrar los componentes y, a continuación, haga clic en las casillas de verificación que desee seleccionar. Haga clic en **[!UICONTROL Continue]**.
1. El grupo de informes seleccionado se muestra en una tabla. Haga clic en **[!UICONTROL Save]** para confirmar la selección.
1. Informar al [!DNL MBI] El equipo de asistencia técnica indica que su integración está autorizada y que ejecutarán el proceso de conexión inicial por usted.

Una vez que se ejecute el proceso de conexión inicial, la tabla estará disponible en la página de Data Warehouse, en la sección `All Tables` pestaña . Seleccione las columnas que desee duplicar y los datos aparecerán después de la siguiente actualización completa.
