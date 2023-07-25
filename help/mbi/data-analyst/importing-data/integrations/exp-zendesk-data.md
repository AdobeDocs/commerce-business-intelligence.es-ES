---
title: Datos esperados de Zendesk
description: Conozca las tablas de datos principales que puede importar de Zendesk a Commerce Intelligence, incluidos los vínculos a documentación adicional sobre Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Previsto [!DNL Zendesk] datos

Después [ha conectado su [!DNL Zendesk] account](../integrations/zendesk.md), puede utilizar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes para su análisis.

En este tema se exploran las tablas de datos principales desde las que se puede importar [!DNL Zendesk] en [!DNL Adobe Commerce Intelligence], incluidos vínculos a documentación adicional sobre [!DNL Zendesk] datos.

| Nombre de tabla | Descripción |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | El `Audits` la tabla registra la actividad asociada a un ticket, incluidos los cambios de estado y las respuestas del cliente y del agente. Esta tabla incluye un ID de ticket que se vincula de nuevo a `Tickets` , que le permite analizar el tiempo hasta la primera respuesta y el tiempo hasta la resolución de cada incidencia. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | El `audit_~\_events` La tabla es el elemento secundario del `audits` y registra detalles adicionales de un evento de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | El `Organizations` registra información de la compañía sobre los usuarios finales, como el nombre, el ID, los nombres de dominio asociados, las etiquetas y cualquier campo personalizado. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | El `Tickets` registra todos los detalles del ticket, incluido el `created_at` marca de tiempo y el `requester\_id` y `assignee\_id`, que le permite vincular un ticket a un usuario final y a un agente en `Users` tabla respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | El `ticket fields` contiene información sobre los campos de texto básicos y los campos de ticket personalizados de su cuenta. Los atributos de esta tabla incluyen el campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, información específica del agente y del usuario final, así como información de creación y actualización. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | El `Users` La tabla incluye todos los detalles sobre los usuarios finales y los agentes, incluido el nombre y el correo electrónico de la persona. Esto le permite analizar tanto la participación de los usuarios finales como el rendimiento de los agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Los grupos son la organización de los agentes en su cuenta de Zendesk. El `Groups` registra información como la `group ID`, `URL`, `name`y la información de creación y actualización. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Las macros son acciones definidas por el usuario que modifican los valores de los campos de un ticket. Esta tabla contiene atributos como el título, el identificador, las acciones, las restricciones y la información de creación y actualización de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | El `Tags` contiene una lista de todas las etiquetas de su cuenta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabla contiene datos sobre las métricas de tickets. Los campos incluyen `ticket ID`, `URL`, y el número de grupos, usuarios asignados, reaperturas, respuestas, tiempo de respuesta (en minutos), tiempo de resolución completa y información de última actualización (por ejemplo, estado, usuario asignado o solicitante). |

{style="table-layout:auto"}

## Relacionado

* [Conectando Zendesk](../integrations/zendesk.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
