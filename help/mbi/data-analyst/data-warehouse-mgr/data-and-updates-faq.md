---
title: Datos e información de actualizaciones
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/qT3lojSuve8jHgNVKoJCUW82cN2QK497wFX8NVbptWI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 481
ht-degree: 0%

---

# Datos e información de actualizaciones

* [¿Por qué han cambiado mis datos?](#datachange)
* [¿Cuál es la diferencia entre una actualización regular y forzada?](#regularforcedupdates)
* [¿Por qué el ciclo de actualización tarda mucho tiempo?](#updatecycletime)
* [¿Se me puede notificar cuando se completa un ciclo de actualización?](#notifyupdate)
* [¿Por qué hay  [!DNL Google ECommerce] datos diferentes de mi base de datos?](#ecommdatabase)
* [¿Cómo puedo solucionar problemas de discrepancia de datos?](#datadiscrepancy)

## ¿Por qué han cambiado mis datos? {#datachange}

Los valores de los gráficos pueden cambiar a lo largo del día debido a que los nuevos datos se sincronizan con su Data Warehouse. Además, los valores de las columnas de datos existentes pueden cambiar debido a [nuevas comprobaciones](../data-warehouse-mgr/cfg-data-rechecks.md). Una nueva comprobación es un proceso que busca valores modificados en columnas de datos, como un estado de pedido que se mueve de `open` a `shipped`.

Existen varias formas [de comprobar el estado del ciclo de actualización](../../best-practices/check-update-cycle.md), según la configuración de permisos del usuario:

* Usuarios **[!UICONTROL Read-Only]y [!UICONTROL Standard]**: pueden pasar el ratón sobre el icono situado en la parte superior derecha de la página para ver cuándo se extrajo el último punto de datos.
* **[!UICONTROL Admin]usuarios**: pueden ver el último icono de estado de integraciones de cuentas y puntos de datos. Para obtener más información, vaya a **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** para ver el estado de la actualización actual y la hora de la última actualización completada.
* **Método de API**: puede recuperar el ciclo de actualización completado más reciente mediante la API Actualizar estado del ciclo.

Para obtener información detallada sobre la comprobación del estado del ciclo de actualización, consulte [Comprobación del estado del ciclo de actualización](../../best-practices/check-update-cycle.md).

## ¿Cuál es la diferencia entre una actualización regular y forzada? {#regularforcedupdates}

Las actualizaciones regulares son **procesos programados**, mientras que las actualizaciones forzadas son **procesos manuales iniciados por usted**. Si tiene horas de interrupción (o un período de tiempo en el que [!DNL Commerce Intelligence] no debe actualizar sus datos), forzar una actualización inicia un ciclo que no respeta las limitaciones del período de interrupción.

## ¿Por qué el ciclo de actualización tarda mucho tiempo? {#updatecycletime}

Numerosos factores pueden añadir a un tiempo de actualización ya largo. Algunos [métodos de replicación](../data-warehouse-mgr/cfg-replication-methods.md), [frecuencias de comprobación más altas](../data-warehouse-mgr/cfg-data-rechecks.md), y el número de paneles y gráficos son sólo algunos factores que contribuyen. Adobe recomienda [reconfigurar algunos de tus ajustes](../../best-practices/reduce-update-cycle-time.md) y [optimizar tu base de datos para el análisis](../../best-practices/opt-db-analysis.md) para reducir los tiempos de actualización.

## ¿Se me puede notificar cuando se completa un ciclo de actualización? {#notifyupdate}

Si hay una actualización en curso, hay un vínculo en la página **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** que puede usar para solicitar una notificación por correo electrónico una vez que finalice el ciclo. Si una actualización no está en curso, verá un vínculo para forzar el inicio de una actualización.

## ¿Por qué hay [!DNL Google ECommerce]datos diferentes de mi base de datos? {#ecommdatabase}

Las discrepancias entre [!DNL Google Analytics] y la base de datos pueden producirse por varios motivos. El seguimiento no se ha habilitado correctamente, los usuarios que visitan incógnito y los eventos de clic no funcionan correctamente son solo algunos ejemplos. Si los ingresos y los pedidos no se ven correctamente, [vea este tema](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) para diagnosticar un problema.

## ¿Cómo puedo solucionar problemas de discrepancia de datos? {#datadiscrepancy}

Adobe sabe que ver datos incoherentes puede ser una experiencia frustrante. Intente usar la [lista de comprobación de discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) o el [tutorial de exportaciones de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) para diagnosticar el problema. Si sigues con errores, [ponte en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
