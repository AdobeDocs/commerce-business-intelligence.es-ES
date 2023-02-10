---
title: Informes del servicio de asistencia técnica de Zendesk
description: Conozca sus canales de referencia más valiosos.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Informes del servicio de asistencia para [!DNL Zendesk]

>[!NOTE]
>
>Esto solo está disponible para los clientes que se encuentran en la variable `Pro` planifique y utilice la nueva arquitectura. Está en la nueva arquitectura si tiene la variable `Data Warehouse Views` sección disponible después de seleccionar `Manage Data` de la barra de herramientas principal.

Consolidar su [!DNL Zendesk] los datos de su base de datos transaccional son una excelente manera de comprender mejor cómo interactúan sus clientes con los equipos de ventas o éxito de los clientes y qué tipo de clientes están utilizando su plataforma de asistencia. En este artículo, demostramos cómo configurar un tablero para obtener informes granulares sobre su [!DNL Zendesk] rendimiento y tiempo en sus clientes transaccionales.

Antes de comenzar, debe conectar con su [[!DNL Zendesk]](../integrations/zendesk.md). Este análisis contiene [columnas calculadas avanzadas](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Introducción

### Columnas para rastrear

* `audits` tabla
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` tabla
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` tabla
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` tabla
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Filtrar conjuntos para crear

* `[!DNL Zendesk] Tickets` tabla
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Columnas calculadas

### Columnas que crear

* **`[!DNL Zendesk] user's`** tabla
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `¡A!=`end-user` then `Yes` when `B` no es `null` y `B` like `%@magento.com` then `Yes` else `No` end

      * Reemplazar `@magento.com` con su dominio

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** tabla
   * Seleccione una definición: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Seleccione un [!UICONTROL table]: `[Zendesk] users`
   * Seleccione un [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** tabla
   * Seleccione una definición: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * Seleccione un [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Seleccione una definición: `Exists`
   * Seleccione un [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[Zendesk] Tickets`** tabla
   * Seleccione una definición: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Seleccione un [!UICONTROL table]: `[Zendesk] users`
   * Seleccione un [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleccione una definición: `Joined Column`
   * Seleccione un [!UICONTROL table]: `[Zendesk] users`
   * Seleccione un [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleccione una definición: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * Seleccione un [!UICONTROL table]: `[Zendesk] audits`
   * Seleccione un [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` cambió a `solved = 1`

   * Seleccione una definición: `Min`
   * Seleccione un [!UICONTROL table]: `[Zendesk] audits`
   * Seleccione un [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` menos `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` menos `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Número entero

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` – `String`


* **`customer_entity`** tabla
   * Seleccione una definición: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.email`
   * 

      [!UICONTROL Uno]: `customer_entity.email`

   * Seleccione un [!UICONTROL table]: `[Zendesk] tickets`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[Zendesk] Tickets`** tabla
   * Seleccione una definición: `Joined Column`
   * Seleccione un [!UICONTROL table]: `customer_entity`
   * Seleccione un [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Métricas

* **[!DNL Zendesk]Nuevos tickets**
   * `Tickets we count`

* En el **`[Zendesk] tickets`** tabla
* Esta métrica realiza una **Recuento**
* En el **`id`** column
* Solicitado por el **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Votos resueltos**
   * `Tickets we count`
   * status IN `closed, solved`

* En el **`[Zendesk] tickets`** tabla
* Esta métrica realiza una **Recuento**
* En el **`id`** column
* Solicitado por el **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Distintos usuarios que presentan tickets**
   * `Tickets we count`

* En el **`[Zendesk] tickets`** tabla
* Esta métrica realiza una **Recuento distinto**
* En el **`requester_id`** column
* Solicitado por el **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tiempo medio/medio de resolución del ticket**
   * `Tickets we count`
   * status IN `closed, solved`

* En el **`[Zendesk] tickets`** tabla
* Esta métrica realiza una **Promedio (o Mediana)**
* En el **`Seconds to resolution`** column
* Solicitado por el **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tiempo medio/medio hasta la primera respuesta**
   * Entradas que contamos
   * estado IN cerrado, resuelto

* En el **`[Zendesk] tickets`** tabla
* Esta métrica realiza una **Promedio (o Mediana)**
* En el **`Seconds to first response`** column
* Solicitado por el **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

### Informes

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Métrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* Métrica `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Métrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Métrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Métrica `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Métrica `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [!UICONTROL Métrica]: Users

* Métrica `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
