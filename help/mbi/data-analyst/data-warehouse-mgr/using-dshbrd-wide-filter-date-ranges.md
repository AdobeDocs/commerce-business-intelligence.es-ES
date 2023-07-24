---
title: Filtrado en todo el panel
description: Aprenda a realizar ediciones masivas de todos los informes en un tablero específico.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Filtrado en todo el panel

Con el filtrado en todo el tablero, puede realizar ediciones masivas de todos los informes en un tablero específico. Puede ver rápidamente el mismo análisis en diferentes periodos de tiempo o para diferentes tiendas. Puede comparar fácilmente el rendimiento de un año, mes o semana anteriores por tienda. Puede actualizar un tablero completo para acomodar una campaña recién iniciada.

## Filtros de fecha

Para cambiar el intervalo o el intervalo de fechas de los informes en un panel, haga clic en el icono de calendario en la esquina superior derecha (![calendario](../../assets/calendar-button.png)).

Puede elegir ver los datos mediante una `Fixed Date Range` o varios precalculados `Moving Date Ranges`:

![movimiento de intervalos de fechas](../../assets/moving_date_ranges.png)

El `Last Full...` las opciones de intervalo móvil representan el intervalo completado más recientemente, mientras que `This...` es el intervalo actual en curso. Por ejemplo, si es junio, la variable `Last Full Month` es _Del 1 al 31 de mayo_, mientras `This Month` es _1 de junio - Ahora_.

O cree los suyos propios `Custom Moving Range`\:

![rango de movimiento personalizado](../../assets/custom-moving-range.png)

Elija también cambiar el intervalo. Seleccionar el botón predeterminado (![intervalo de tiempo predeterminado](../../assets/time_interval_default.png)) significa que solo cambia el intervalo de fecha:

![intervalo de tiempo](../../assets/time_interval.png)

Para restaurar todos los informes a su intervalo de fechas inicial, haga clic en **[!UICONTROL Restore Defaults]** o haga clic en **[!UICONTROL Cancel]**.

Cuando se especifica un filtro de fecha para un panel, ese filtro se aplica solo a ese panel. No se aplica cuando se desplaza a otros paneles.

>[!NOTE]
>
>Actualmente, `Cohort Reports` y `SQL Reports` no se incluyen al aplicar cambios a nivel de panel.

## Filtros de tienda

Para analizar el rendimiento de una tienda específica, haga clic en el icono de tiendas en la esquina superior derecha (![Filtro de tienda](../../assets/store-filter.png)). De forma predeterminada, `Store Filter` se establece en `All Stores`, que muestra los datos de todos los [vistas de tienda](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) disponible en su sitio de Commerce.

>[!NOTE]
>
>Un filtro de tienda está habilitado o deshabilitado para un [!DNL Commerce Intelligence] cuenta. Si un tablero contiene informes que no se ven afectados por el filtro (como los informes que no están creados en ninguno de los [!DNL Adobe Commerce] datos), esos informes no se actualizan cuando se aplica el filtro de almacén. Puede [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si cree que un informe debe actualizarse en función de la selección de tiendas o si cree que el filtro del almacén de cuentas se ha deshabilitado por error.

Al seleccionar un almacén de la lista `Store Filter`Sin embargo, el filtro conserva su selección cuando navega entre paneles. Conservar la selección le permite ver los datos del almacén seleccionado en todas partes hasta que seleccione `All Stores`.

## Filtros para paneles compartidos

En el caso de los paneles compartidos, si un usuario configura el filtro de fecha, otros usuarios con acceso al panel verán el mismo filtro aplicado. Sin embargo, el filtro de tienda no se aplica en este caso. Si el propietario del panel configura el filtro de almacén y comparte el panel, el filtro de almacén configurado no se mantiene para otro usuario. Un usuario debe tener [acceso de edición](../../data-user/dashboards/share-dashboard-with-users.md) a un tablero para ajustar los filtros de este.
