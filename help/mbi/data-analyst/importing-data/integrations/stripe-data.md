---
title: Datos de Stripe esperados
description: Explore las tablas de datos principales que puede importar de Stripe a Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Previsto [!DNL Stripe] datos

Después [ha conectado su [!DNL Stripe] account](../integrations/stripe.md), puede utilizar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes para su análisis.

En este tema se exploran las tablas de datos principales desde las que se puede importar [!DNL Stripe] en [!DNL Commerce Intelligence]. Una vez completada la configuración, se crearán las siguientes tablas en la Data Warehouse. Haga clic en los vínculos de la columna Nombre de tabla para obtener más información sobre los atributos de cada tabla.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Los objetos de cliente permiten realizar cargos recurrentes y realizar un seguimiento de varios cargos asociados al mismo cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Esta tabla contiene información sobre los cargos realizados en las tarjetas de crédito y débito, incluido el importe, la divisa, el estado, el ID de cliente, etc. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Esta tabla contiene información sobre un descuento por porcentaje o importe de descuento que puede que desee aplicar a un cliente. Los cupones solo se aplican a las facturas; no se aplican a cargos únicos. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Esta tabla contiene información sobre facturas, incluido el importe adeudado, suscripciones, artículos de factura, cualquier ajuste de prorrateo automático, etc. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Esta tabla contiene la información de precios de diferentes productos y niveles de funciones del sitio. Por ejemplo, puede tener un plan de $10 al mes para funciones básicas y un plan de $20 al mes para funciones premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Esta tabla contiene los detalles de los planes de suscripción a los que pertenecen sus clientes. Los atributos incluyen el ID de cliente, el estado, las fechas de cancelación/finalización, el porcentaje de impuestos, la información de prueba, etc. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Los eventos le permiten conocer algo interesante que ha sucedido en una cuenta de. [Cuando se produce un evento interesante](https://stripe.com/docs/api/events/types), se crea un nuevo objeto de evento. Por ejemplo, cuando un cargo se realiza correctamente `charge.succeeded` evento se ha creado, o cuando una factura no se puede pagar, `invoice.payment\_failed` evento creado. |

{style="table-layout:auto"}

>[!NOTE]
>
>Muchas solicitudes de API pueden provocar la creación de varios eventos. Por ejemplo, si crea una suscripción para un cliente, recibirá un `customer.subscription.created` evento y una  `charge.succeeded` evento.

## Relacionado:

* [Conectando [!DNL Stripe]](../integrations/stripe.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
