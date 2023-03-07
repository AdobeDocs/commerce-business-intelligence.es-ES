---
title: Restringir el acceso a métricas
description: Aprenda a trabajar con métricas de acceso y restricciones.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Administrar usuarios de métricas

Además de establecer los niveles de permisos de los usuarios, también puede restringir el acceso a las métricas usuario por usuario. Por ejemplo, si desea que el departamento de contabilidad tenga acceso a métricas relacionadas con los ingresos pero no a métricas de adquisición de usuarios, puede restringir el acceso a dichas métricas.

En casos como estos, Adobe recomienda configurar la cuenta de ese usuario como **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** los permisos deben concederse a los usuarios que no necesiten crear ni modificar métricas, columnas calculadas, integraciones o usuarios, pero que sí necesiten acceder a los datos de la Data Warehouse. Si desea restringir completamente el acceso a los datos, utilice la variable **[!UICONTROL Read Only]** en su lugar.

Después de establecer el nivel de permisos, puede seleccionar las métricas como **[!UICONTROL Standard]** El usuario puede acceder a haciendo lo siguiente:

1. Ir a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleccione la cuenta de usuario que desee.
1. El **[!UICONTROL Metrics]** Esta pestaña muestra una lista de las métricas disponibles. Compruebe las métricas a las que desea que el usuario tenga acceso; anule la selección de las que el usuario no debe tener acceso.
1. [!DNL MBI] guarda los cambios automáticamente. Si el cambio se realiza correctamente, [!DNL MBI] visualizaciones **[!UICONTROL Saved!]** en la parte superior de la página.

>[!NOTE]
>
>Todos los usuarios con **[!UICONTROL Standard]** Los permisos de pueden acceder a todos los datos de la Data Warehouse a través de la exportación de datos, además de todas las métricas de [!DNL Google Analytics].

También puede restringir el acceso a una métrica editando la métrica y **[!UICONTROL Standard]** seleccionar usuarios en la **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sección.

>[!NOTE]
>
>Si duplica una métrica, [!DNL MBI] copia los permisos de usuario establecidos en la métrica original.
