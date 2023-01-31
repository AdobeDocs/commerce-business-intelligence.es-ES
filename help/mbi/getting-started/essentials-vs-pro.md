---
title: Esenciales de MBI frente a Pro
description: Aprenda cómo difiere MBI Essentials del MBI Pro.
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: 1703e469e245629797bbe08d691d7f8e816a4019
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>Esta documentación está archivada para [!DNL MBI].

La siguiente tabla describe lo que se incluye con Essentials y Pro.

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | Hasta 100 | Personalizado |
| `Pre-Defined Dashboards` | 5-6 | Personalizado |
| `New Custom Report Creation` | Sí | Sí |
| `Magento Commerce Tables` | 4-6 | Sin límite |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | Sí | Sí |
| `Data Warehouse Manager` | No disponible | Disponible |
| `Email Reports` | Sí | Sí |
| `Cohort Report Builder` | Sí | Sí |
| `Google Analytics Live Integration` | Sí | Sin límite |
| `3rd Party Integrations` | No disponible | Disponible |
| `Full API Access` | No | Sí |
| `Access to CS, AM, or Analysts` | No | Sí |
| `Professional Services` | Disponible | Disponible |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>El número de tablas depende del cierre de compra de los invitados.

**Tablas incluidas**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Columnas incluidas en Essentials

Elementos en _cursiva_ son campos calculados.

* `sales_order` tabla
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` tabla
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` tabla
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` tabla
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` tabla
   * `customer_group_id`
   * `customer_group_code`

* `store` tabla
   * `store_id`
   * `name`

Consulte la siguiente serie de vídeos para obtener más información sobre las diferencias entre [!DNL MBI Essentials] y [!DNL MBI Pro].

* [`Essentials`](https://support.magento.com/hc/en-us/articles/360005305614)
* [`Pro`](https://support.magento.com/hc/en-us/articles/360005373453)
