---
title: Datos esperados de Zendesk
description: Conozca las tablas de datos principales que puede importar de Zendesk a Commerce Intelligence, incluidos los vínculos a documentación adicional sobre Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0p4SOrpj7wM-y5j3CMpHTs7HpysB5znJu3jSNiVJ2YY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 362
ht-degree: 0%

---

# Se esperaban [!DNL Zendesk] datos

Después de [haber conectado tu [!DNL Zendesk] cuenta](../integrations/zendesk.md), puedes usar [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis.

En este tema se exploran las tablas de datos principales que se pueden importar de [!DNL Zendesk] a [!DNL Adobe Commerce Intelligence], incluidos los vínculos a documentación adicional sobre los datos de [!DNL Zendesk].

| Nombre de tabla | Descripción |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La tabla `Audits` registra la actividad asociada con un ticket, incluidos los cambios de estado y las respuestas del cliente y del agente. Esta tabla incluye un identificador de ticket que se vincula de nuevo a la tabla `Tickets`, lo que le permite analizar el tiempo hasta la primera respuesta y el tiempo hasta la resolución de cada ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La tabla `audit_~\_events` es la secundaria de la tabla `audits` y registra detalles adicionales de un evento de ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | La tabla `Organizations` registra información de la compañía acerca de los usuarios finales, como el nombre, el identificador, los nombres de dominio asociados, las etiquetas y cualquier campo personalizado. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La tabla `Tickets` registra todos los detalles del vale, incluida la marca de tiempo `created_at` y las marcas de tiempo `requester\_id` y `assignee\_id`, lo que le permite vincular un vale a un usuario final y a un agente en la tabla `Users` respectivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | La tabla `ticket fields` contiene información sobre los campos de texto básicos y los campos de ticket personalizados de su cuenta. Los atributos de esta tabla incluyen el campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, información específica del agente y del usuario final, así como información de creación y actualización. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | La tabla `Users` incluye todos los detalles sobre los usuarios finales y los agentes, incluidos el nombre y el correo electrónico de la persona. Esto le permite analizar tanto la participación de los usuarios finales como el rendimiento de los agentes. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Los grupos son la organización de los agentes en su cuenta de Zendesk. La tabla `Groups` registra información como `group ID`, `URL`, `name`, así como información de creación y actualización. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Las macros son acciones definidas por el usuario que modifican los valores de los campos de un ticket. Esta tabla contiene atributos como el título, el identificador, las acciones, las restricciones y la información de creación y actualización de la macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | La tabla `Tags` contiene una lista de todas las etiquetas de su cuenta. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Esta tabla contiene datos sobre las métricas de tickets. Los campos incluyen `ticket ID`, `URL`, y el número de grupos, usuarios asignados, reaperturas, respuestas, tiempo de respuesta (en minutos), tiempo de resolución completo y la información de última actualización (por ejemplo, estado, usuario asignado o solicitante). |

{style="table-layout:auto"}

## Relacionado

* [Conectando Zendesk](../integrations/zendesk.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
