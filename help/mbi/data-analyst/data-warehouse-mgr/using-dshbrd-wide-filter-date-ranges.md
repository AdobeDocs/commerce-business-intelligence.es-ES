---
title: Filtrado en todo el panel
description: Aprenda a realizar ediciones masivas de todos los informes en un tablero específico.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/6wixrQXkvGMF9c36wrGJ4Qj23HqJ--Mr0XMYMBhujjo
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
source-wordcount: 449
ht-degree: 0%

---

# Filtrado en todo el panel

Con el filtrado en todo el tablero, puede realizar ediciones masivas de todos los informes en un tablero específico. Puede ver rápidamente el mismo análisis en diferentes periodos de tiempo o para diferentes tiendas. Puede comparar fácilmente el rendimiento de un año, mes o semana anteriores por tienda. Puede actualizar un tablero completo para acomodar una campaña recién iniciada.

## Filtros de fecha

Para cambiar el intervalo de fechas o el intervalo de informes en un panel, haga clic en el icono de calendario en la esquina superior derecha (![calendario](../../assets/calendar-button.png)).

Puede elegir ver los datos usando un `Fixed Date Range` o varios `Moving Date Ranges` precalculados:

![moviendo intervalos de fechas](../../assets/moving_date_ranges.png)

Las opciones de intervalo móvil de `Last Full...` representan el intervalo completado más recientemente, mientras que `This...` es el intervalo actual en curso. Por ejemplo, si es junio, `Last Full Month` es del _1 de mayo al 31 de mayo_, mientras que `This Month` es del _1 de junio al presente_.

O cree su propio `Custom Moving Range`\:

![intervalo móvil personalizado](../../assets/custom-moving-range.png)

Elija también cambiar el intervalo. Si selecciona el botón predeterminado (![intervalo de tiempo predeterminado](../../assets/time_interval_default.png)), solo cambiará el intervalo de fecha:

![intervalo de tiempo](../../assets/time_interval.png)

Para restaurar todos los informes a su intervalo de fechas inicial, haga clic en **[!UICONTROL Restore Defaults]** o en **[!UICONTROL Cancel]**.

Cuando se especifica un filtro de fecha para un panel, ese filtro se aplica solo a ese panel. No se aplica cuando se desplaza a otros paneles.

>[!NOTE]
>
>Actualmente, `Cohort Reports` y `SQL Reports` no se incluyen al aplicar cambios a nivel de panel.

## Filtros de tienda

Para analizar el rendimiento de un almacén específico, haga clic en el icono Almacenes en la esquina superior derecha (![Filtro de almacén](../../assets/store-filter.png)). De manera predeterminada, `Store Filter` está establecido en `All Stores`, que muestra los datos de todas las [vistas de tiendas](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) disponibles en su sitio de Commerce.

>[!NOTE]
>
>Se habilitó o deshabilitó un filtro de almacén para toda una cuenta de [!DNL Commerce Intelligence]. Si un tablero contiene informes que no se ven afectados por el filtro (como los informes que no están creados en ningún dato de [!DNL Adobe Commerce]), esos informes no se actualizan cuando se aplica el filtro de almacén. Puedes [ponerte en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si crees que un informe debería actualizarse en función de la selección de la tienda o si crees que el filtro de la tienda de cuentas se ha deshabilitado por error.

Cuando selecciona un almacén de `Store Filter`, el filtro conserva su selección cuando navega entre paneles. Conservar la selección le permite ver los datos del almacén seleccionado en todas partes hasta que seleccione `All Stores`.

## Filtros para paneles compartidos

En el caso de los paneles compartidos, si un usuario configura el filtro de fecha, otros usuarios con acceso al panel verán el mismo filtro aplicado. Sin embargo, el filtro de tienda no se aplica en este caso. Si el propietario del panel configura el filtro de almacén y comparte el panel, el filtro de almacén configurado no se mantiene para otro usuario. Un usuario debe tener [acceso de edición](../../data-user/dashboards/share-dashboard-with-users.md) a un tablero para ajustar los filtros del mismo.
