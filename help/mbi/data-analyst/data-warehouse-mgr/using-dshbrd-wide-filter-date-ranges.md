---
title: Filtrado ancho del panel
description: Aprenda a realizar ediciones masivas de todos los informes en un tablero específico.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Filtrado ancho del panel

Con el filtrado de tableros de gran alcance, puede realizar ediciones masivas de todos los informes en un tablero específico. Puede ver rápidamente el mismo análisis en diferentes periodos de tiempo o en diferentes tiendas. Puede comparar fácilmente el rendimiento de un año, mes o semana anteriores por tienda. Además, puede actualizar un tablero completo para que quepa una campaña recién lanzada.

## Filtros de fecha

Para cambiar el intervalo de fechas o el intervalo de informes en un tablero, haga clic en el icono de calendario en la esquina superior derecha (![calendario](../../assets/calendar-button.png)).

Puede elegir ver los datos mediante un `Fixed Date Range` o una variedad de `Moving Date Ranges`:

![mover intervalos de fechas](../../assets/moving_date_ranges.png)

La variable `Last Full...` las opciones de intervalo de desplazamiento representan el intervalo completado más recientemente, mientras que `This...` será el intervalo actual en curso. Por ejemplo, si actualmente es junio, la variable `Last Full Month` es _Del 1 de mayo al 31 de mayo_, while `This Month` es _1 de junio - Ahora_.

O cree su propio `Custom Moving Range`\:

![intervalo móvil personalizado](../../assets/custom-moving-range.png)

Elija también cambiar el intervalo. Selección del botón predeterminado (![intervalo de tiempo predeterminado](../../assets/time_interval_default.png)) significa que solo se cambiará el intervalo de fechas:

![intervalo de tiempo](../../assets/time_interval.png)

Para restaurar todos los informes a su intervalo de fechas y a su intervalo inicial, haga clic en **[!UICONTROL Restore Defaults]** o haga clic en **[!UICONTROL Cancel]**.

Cuando se especifica un filtro de fecha para un tablero, ese filtro solo se aplica a ese tablero. No se aplica cuando se navega a otros tableros.

>[!NOTE]
>
>En este momento, `Cohort Reports` y `SQL Reports` no se incluyen al aplicar cambios en un nivel de panel.

## Filtros de almacenamiento

Para analizar el rendimiento de una tienda específica, haga clic en el icono de tiendas en la esquina superior derecha (![Filtro de tienda](../../assets/store-filter.png)). De forma predeterminada, `Store Filter` está configurado como `All Stores`, que muestra los datos de todas las [vistas de tiendas](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) disponible en su sitio de comercio.

>[!NOTE]
>
>Un filtro de tienda está habilitado o deshabilitado para todo un [!DNL MBI] cuenta. Si un tablero contiene informes que no se ven afectados por el filtro, como informes que no están basados en datos de comercio, esos informes no se actualizan cuando se aplica el filtro de almacenamiento. Puede [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md) si cree que un informe debe actualizarse en función de la selección del almacén o si cree que el filtro del almacén de cuentas está deshabilitado por error.

Al seleccionar un almacén de la variable `Store Filter`, el filtro conserva la selección cuando navega entre tableros. Retener la selección le permite ver los datos de la tienda seleccionada en todas partes hasta que seleccione `All Stores`.

## Filtros para tableros compartidos

En el caso de los tableros compartidos, si un usuario configura el filtro de fecha, otros usuarios con acceso al tablero verán ese mismo filtro aplicado. Sin embargo, el filtro de tienda no se aplica en este caso. Si el propietario del tablero configura el filtro de almacén y comparte el tablero, el filtro de almacén configurado no persistirá con otro usuario. Un usuario debe tener [editar acceso](../../data-user/dashboards/share-dashboard-with-users.md) a un tablero para ajustar los filtros de tablero.
