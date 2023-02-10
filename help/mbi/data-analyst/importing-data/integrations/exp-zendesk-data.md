---
title: Datos esperados de Zendesk
description: Conozca las principales tablas de datos que puede importar de Zendesk a MBI, incluidos vínculos a documentación adicional sobre los datos de Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Datos esperados de Zendesk

Después [ha conectado su [!DNL Zendesk] account](../integrations/zendesk.md), puede usar la variable [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis.

En este artículo, exploramos las principales tablas de datos desde las que puede importar [!DNL Zendesk] into [!DNL MBI], incluidos vínculos a documentación adicional sobre [!DNL Zendesk] datos.

| Nombre de tabla | Descripción |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La variable `Audits` la tabla registra la actividad asociada a un ticket, incluidos los cambios de estado y las respuestas del cliente y del agente. Esta tabla incluye un id de ticket que se vincula con el `Tickets` , que le permite analizar la hora de la primera respuesta y la hora de resolución de cada ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La variable `audit_~\_events` es el elemento secundario del `audits` y registra detalles adicionales de un evento de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | La variable `Organizations` la tabla registra la información de la empresa sobre los usuarios finales, como el nombre, el ID, los nombres de dominio asociados, las etiquetas y cualquier campo personalizado. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La variable `Tickets` la tabla registra todos los detalles del ticket, incluido el `created_at` timestamp, así como la variable `requester\_id` y `assignee\_id`, que le permite vincular un ticket a un usuario final y a un agente en la variable `Users` respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | La variable `ticket fields` contiene información sobre los campos de texto básicos, así como los campos de ticket personalizados de la cuenta. Los atributos de esta tabla incluyen el campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, información específica del agente y del usuario final, y información de creación y actualización. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | La variable `Users` incluye todos los detalles sobre usuarios finales y agentes, incluido el nombre y el correo electrónico de la persona. Esto le permite analizar tanto la participación de los usuarios finales como el rendimiento de sus agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Los grupos son como los agentes se organizan en su cuenta de Zendesk. La variable `Groups` información de registros de tabla, como `group ID`, `URL`, `name`y la información de creación y actualización. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Las macros son acciones definidas por el usuario que modifican los valores de los campos de un ticket. Esta tabla contiene atributos como el título, el ID, las acciones, las restricciones y la información de creación y actualización de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | La variable `Tags` contiene una lista de todas las etiquetas de la cuenta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabla contiene datos sobre las métricas de ticket. Los campos incluyen la variable `ticket ID`, `URL`y el número de grupos, usuarios asignados, reaperturas, respuestas, tiempo de respuesta (en minutos), tiempo de resolución completa y última actualización (por ejemplo, estado, usuario asignado o solicitante). |

{style=&quot;table-layout:auto&quot;}

## Relacionado

* [Conexión del escritorio central](../integrations/zendesk.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
