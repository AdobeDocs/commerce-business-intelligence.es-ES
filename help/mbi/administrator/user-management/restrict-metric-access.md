---
title: Restringir el acceso a métricas
description: Aprenda a trabajar con métricas de acceso y restricciones.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Administrar usuarios de métricas

Además de establecer los niveles de permisos de los usuarios, también puede restringir el acceso a las métricas usuario por usuario. Por ejemplo, si desea que el departamento de contabilidad tenga acceso a métricas relacionadas con los ingresos pero no a métricas de adquisición de usuarios, puede restringir el acceso a dichas métricas.

En casos como estos, Adobe recomienda configurar la cuenta de ese usuario como **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** los permisos deben concederse a los usuarios que no necesiten crear ni modificar métricas, columnas calculadas, integraciones o usuarios, pero que sí necesiten acceder a los datos de la Data Warehouse. Si desea restringir completamente el acceso a los datos, utilice la variable **[!UICONTROL Read Only]** en su lugar.

Después de establecer el nivel de permisos, puede seleccionar las métricas como **[!UICONTROL Standard]** El usuario puede acceder a haciendo lo siguiente:

1. Ir a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleccione la cuenta de usuario que desee.
1. El **[!UICONTROL Metrics]** Esta pestaña muestra una lista de las métricas disponibles. Compruebe las métricas a las que desea que el usuario tenga acceso y anule la selección de aquellas a las que el usuario no debe tener acceso.
1. [!DNL Adobe Commerce Intelligence] guarda los cambios automáticamente. Si el cambio se realiza correctamente, [!DNL Commerce Intelligence] visualizaciones **[!UICONTROL Saved!]** en la parte superior de la página.

>[!NOTE]
>
>Todos los usuarios con **[!UICONTROL Standard]** Los permisos de pueden acceder a todos los datos de la Data Warehouse a través de la exportación de datos, además de todas las métricas de [!DNL Google Analytics].

También puede restringir el acceso a una métrica editando la métrica y **[!UICONTROL Standard]** seleccionar usuarios en la **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sección.

>[!NOTE]
>
>Si duplica una métrica, [!DNL Commerce Intelligence] copia los permisos de usuario establecidos en la métrica original.
