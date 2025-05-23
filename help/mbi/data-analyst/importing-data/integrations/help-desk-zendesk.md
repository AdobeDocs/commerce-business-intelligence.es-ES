---
title: Informes del servicio de asistencia de Zendesk
description: Obtenga información sobre los canales de referencia más valorados.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Informes del servicio de asistencia para [!DNL Zendesk]

>[!NOTE]
>
>Esto solo está disponible para los clientes que se encuentran en el plan `Pro` y que utilizan la nueva arquitectura. Se encuentra en la nueva arquitectura si tiene disponible la sección `Data Warehouse Views` después de seleccionar `Manage Data` en la barra de herramientas principal.

Consolidar los datos de [!DNL Zendesk] con su base de datos transaccional es una excelente manera de comprender mejor cómo interactúan sus clientes con sus equipos de éxito de ventas o clientes. También le ayuda a saber qué tipo de clientes utilizan su plataforma de asistencia. En este tema se muestra cómo configurar un tablero para obtener informes granulares sobre el rendimiento de [!DNL Zendesk] y el tiempo en sus clientes transaccionales.

Antes de comenzar, desea conectar su [[!DNL Zendesk]](../integrations/zendesk.md). Este análisis contiene [columnas calculadas avanzadas](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Primeros pasos

### Columnas que rastrear

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

### Conjuntos de filtros para crear

* `[!DNL Zendesk] Tickets` tabla
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Columnas calculadas

### Columnas para crear

* **`[!DNL Zendesk] user's`** tabla
   * `User is agent? (Yes/No) `
   * &#x200B;
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `nulo` and `A!=`end-user` entonces `Yes` cuando `B` no es `null` y `B` como `%@magento.com` entonces `Yes` más `No` finalizan

      * Reemplazar `@magento.com` por su dominio

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** tabla
   * Seleccione una definición: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleccionar un(a) [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** tabla
   * Seleccione una definición: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Seleccione una definición: `Exists`
   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** tabla
   * Seleccione una definición: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleccionar un(a) [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Seleccione una definición: `Joined Column`
   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleccionar un(a) [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Seleccione una definición: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Seleccionar un(a) [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` se cambió a `solved = 1`

   * Seleccione una definición: `Min`
   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Seleccionar un(a) [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` menos `created_at`

* **`Seconds to first response`**
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` menos `created_at`

* **`Requester's ticket number`**
   * &#x200B;
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * &#x200B;
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Entero

* **`Ticket created_at (day of week)`**
   * &#x200B;
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`** tabla
   * Seleccione una definición: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * &#x200B;

     [!UICONTROL Uno]: `customer_entity.email`

   * Seleccionar un(a) [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * &#x200B;
      * `Column type` - &quot;Misma tabla > Cálculo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`** tabla
   * Seleccione una definición: `Joined Column`
   * Seleccionar un(a) [!UICONTROL table]: `customer_entity`
   * Seleccionar un(a) [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Métricas

* **[!DNL Zendesk]nuevos tickets**
   * `Tickets we count`

* En la tabla **`[!DNL Zendesk] tickets`**
* Esta métrica realiza **Count**
* En la columna **`id`**
* Ordenado por la marca de tiempo **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]tickets resueltos**
   * `Tickets we count`
   * estado EN `closed, solved`

* En la tabla **`[!DNL Zendesk] tickets`**
* Esta métrica realiza **Count**
* En la columna **`id`**
* Ordenado por la marca de tiempo **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]usuarios distintos están archivando tickets**
   * `Tickets we count`

* En la tabla **`[!DNL Zendesk] tickets`**
* Esta métrica realiza un **Recuento distinto**
* En la columna **`requester_id`**
* Ordenado por la marca de tiempo **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tiempo promedio/medio de resolución de tickets**
   * `Tickets we count`
   * estado EN `closed, solved`

* En la tabla **`[!DNL Zendesk] tickets`**
* Esta métrica realiza un **Promedio (o Mediana)**
* En la columna **`Seconds to resolution`**
* Ordenado por la marca de tiempo **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tiempo promedio/medio hasta la primera respuesta**
   * Entradas que se cuentan
   * estado IN cerrado, resuelto

* En la tabla **`[!DNL Zendesk] tickets`**
* Esta métrica realiza un **Promedio (o Mediana)**
* En la columna **`Seconds to first response`**
* Ordenado por la marca de tiempo **`created_at`**
* [!UICONTROL Filter]:

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a las métricas](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

### Informes

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * estado EN `new, open, pending`

* Métrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * estado EN `solved, closed`

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
   * estado EN `solved, closed`

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
   * estado EN `solved, closed`

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
   * &#x200B;

     [!UICONTROL Métrica]: Users

* Métrica `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
