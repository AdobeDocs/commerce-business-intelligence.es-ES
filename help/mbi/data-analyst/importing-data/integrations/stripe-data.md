---
title: Datos Stripe esperados
description: Explore las tablas de datos principales que se pueden importar desde Stripe a Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/dCiDusso9q9gvZOXKeHcDcuVK-jCXkqR3pQg6eTKzdo
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 0%

---

# Se esperaban [!DNL Stripe] datos

Después de [haber conectado tu [!DNL Stripe] cuenta](../integrations/stripe.md), puedes usar [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis.

En este tema se exploran las tablas de datos principales que se pueden importar de [!DNL Stripe] a [!DNL Commerce Intelligence]. Una vez completada la configuración, se crearán las siguientes tablas en el Data Warehouse. Haga clic en los vínculos de la columna Nombre de tabla para obtener más información sobre los atributos de cada tabla.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Los objetos de cliente permiten realizar cargos recurrentes y realizar un seguimiento de varios cargos asociados al mismo cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Esta tabla contiene información sobre los cargos realizados en las tarjetas de crédito y débito, incluido el importe, la divisa, el estado, el ID de cliente, etc. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Esta tabla contiene información sobre un descuento por porcentaje o importe de descuento que puede que desee aplicar a un cliente. Los cupones solo se aplican a las facturas; no se aplican a cargos únicos. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Esta tabla contiene información sobre facturas, incluido el importe adeudado, suscripciones, artículos de factura, cualquier ajuste de prorrateo automático, etc. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Esta tabla contiene la información de precios de diferentes productos y niveles de funciones del sitio. Por ejemplo, puede tener un plan de $10 al mes para funciones básicas y un plan de $20 al mes para funciones premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Esta tabla contiene los detalles de los planes de suscripción a los que pertenecen sus clientes. Los atributos incluyen el ID de cliente, el estado, las fechas de cancelación/finalización, el porcentaje de impuestos, la información de prueba, etc. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Los eventos le permiten conocer algo interesante que ha sucedido en una cuenta de. [Cuando se produce un evento interesante](https://stripe.com/docs/api/events/types), se crea un nuevo objeto de evento. Por ejemplo, cuando un cargo se realiza correctamente `charge.succeeded`, se crea un evento o, cuando una factura no se puede pagar, se crea un evento `invoice.payment\_failed`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Muchas solicitudes de API pueden provocar la creación de varios eventos. Por ejemplo, si crea una suscripción para un cliente, recibirá un evento `customer.subscription.created` y un evento `charge.succeeded`.

## Relacionado:

* [Conectando [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
