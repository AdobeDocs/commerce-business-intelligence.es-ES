---
title: Datos de bandas esperados
description: Explorar las tablas de datos principales que se pueden importar desde la banda a [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Esperado [!DNL Stripe] data

Después [ha conectado su [!DNL Stripe] account](../integrations/stripe.md), puede usar la variable [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis.

En este artículo, exploramos las principales tablas de datos desde las que puede importar [!DNL Stripe] into [!DNL MBI]. Una vez completada la configuración, se crearán las tablas siguientes en el almacén de datos. Haga clic en los vínculos de la columna Nombre de tabla para obtener más información sobre los atributos de cada tabla.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | Los objetos del cliente le permiten realizar cargos recurrentes y rastrear múltiples cargos asociados al mismo cliente. |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | Esta tabla contiene información sobre los cargos a las tarjetas de crédito y de débito, incluyendo la cantidad, moneda, estado, ID de cliente, etc. |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | Esta tabla contiene información acerca de un descuento porcentual o de cantidad que puede querer aplicar a un cliente. Tenga en cuenta que los cupones solo se aplican a las facturas; no se aplican a los gastos únicos. |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | Esta tabla contiene información sobre facturas, incluido el importe adeudado, suscripciones, artículos de factura, cualquier ajuste automático de prorrateo, etc. |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | Esta tabla contiene la información de precios de diferentes productos y niveles de características del sitio. Por ejemplo, puede tener un plan de 10 dólares al mes para las funciones básicas y un plan de 20 dólares al mes para las funciones Premium. |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | Esta tabla contiene los detalles de los planes de suscripción a los que pertenecen sus clientes. Los atributos incluyen ID de cliente, estado, cancelado/finalizado en fechas, porcentaje de impuesto, información de prueba, etc. |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | Los eventos le permiten conocer algo interesante que acaba de suceder en una cuenta. [Cuando se produce un evento interesante](https://stripe.com/docs/api/curl#event_types), se crea un nuevo objeto de evento. Por ejemplo, cuando un cargo se realiza correctamente `charge.succeeded` se crea; o bien, cuando no se puede pagar una factura, `invoice.payment\_failed` se crea. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Muchas solicitudes de API pueden hacer que se creen varios eventos. Por ejemplo, si crea una nueva suscripción para un cliente, recibirá ambas `customer.subscription.created` y  `charge.succeeded` evento.

## Relacionado:

* [Conexión [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
