---
title: Datos de QuickBooks esperados
description: Aprenda a rastrear fácilmente campos de datos relevantes para su análisis.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Esperado [!DNL QuickBooks] data

![](../../../assets/Quickbooks.png)

Después [ha conectado su [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), puede usar la variable [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente campos de datos relevantes para su análisis. Se crearán las tablas siguientes en el almacén de datos:

Para ver todos los campos disponibles para seguimiento, haga clic en los vínculos en la columna nombre de tabla.

## Entidades de transacción {#transactionentities}

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`bill`](https://developer.intuit.com/docs/api/accounting/Bill) | La tabla de facturas contiene información sobre transacciones AP o una solicitud de pago de un tercero. Los atributos incluyen tipo de moneda, tipo de cambio, cantidad total, fecha de vencimiento, saldo, etc. |
| [`billpayments`](https://developer.intuit.com/docs/api/accounting/BillPayment) | Las entidades BillPayment son la transacción final de pago de facturas recibidas de un proveedor. Esta tabla incluye la información del proveedor, el tipo de pago, el importe total, la fecha de transacción, etc. |
| [`creditmemos`](https://developer.intuit.com/docs/api/accounting/CreditMemo) | En el cuadro de notas de crédito se registran las transacciones que son reembolsos o créditos de pagos totales y parciales. Algunos atributos incluyen el nombre del cliente, la información de facturación y envío del cliente, la cantidad y la fecha. |
| [`deposits`](https://developer.intuit.com/docs/api/accounting/Deposit) | Los depósitos incluyen los depósitos directos y los pagos a clientes transferidos a la Cuenta de Activos después de haberse mantenido en la `Undeposited Funds` cuenta. Los atributos incluyen la cantidad, el ID de depósito y la fecha. |
| [`estimates`](https://developer.intuit.com/docs/api/accounting/Estimate) | Las estimaciones son transacciones dadas a clientes que incluyen los precios propuestos para un bien o servicio. Esta tabla registra la cantidad, cualquier información de descuento, información del cliente y fecha. |
| [`invoices`](https://developer.intuit.com/docs/api/accounting/Invoice) | Las facturas son formularios de venta que un cliente paga más tarde. La tabla de facturas registra cualquier información de depósito, fecha, artículos de línea, información de impuestos e información del cliente. |
| [`journalentries`](https://developer.intuit.com/docs/api/accounting/JournalEntry) | La tabla de periodismo registra la información de cuentas AR y AP, incluido el ID de entrada de diario, la fecha de transacción y la información de artículo de línea. |
| [`payments`](https://developer.intuit.com/docs/api/accounting/Payment) | Un registro de pago incluye atributos como el ID de pago, los importes aplicados y no aplicados, la fecha de transacción, el tipo de transacción y el estado de procesamiento. |
| [`purchases`](https://developer.intuit.com/docs/api/accounting/Purchase) | La tabla de compras representa sus gastos e incluye el ID de compra, el tipo de pago, el importe y cualquier información de artículo de línea. |
| [`purchaseorders`](https://developer.intuit.com/docs/api/accounting/PurchaseOrder) | Los pedidos de compra son solicitudes de bienes enviados a proveedores. Esta tabla incluye la información del proveedor, el ID de pedido de compra, la fecha de transacción, la información del artículo de línea, el importe total y la información de cuenta AP. |
| [`refundreceipts`](https://developer.intuit.com/docs/api/accounting/RefundReceipt) | En esta tabla se registran los reembolsos concedidos a los clientes. Los atributos incluyen el identificador de recibo de devolución, la información del artículo de línea, el importe total, la información del cliente y el saldo. |
| [`salesreceipts`](https://developer.intuit.com/docs/api/accounting/SalesReceipt) | La tabla de recibos de venta registra la información de los cobros de ventas entregados a los clientes, incluido el identificador de recibo de venta, la información de artículo de línea, el importe total, la información del cliente, la fecha de transacción y cualquier depósito. |
| [`timeactivities`](https://developer.intuit.com/docs/api/accounting/TimeActivity) | Las actividades horarias son registros horarios para proveedores o empleados. La tabla de actividades de tiempo incluye el ID de actividad de tiempo, la información de empleado/proveedor, el tiempo registrado, la descripción de la actividad y la fecha registrada. |
| [`transfers`](https://developer.intuit.com/docs/api/accounting/Transfer) | La tabla de transferencias registra información sobre los fondos transferidos entre cuentas. Los atributos incluyen el ID de transferencia, el importe, la información de la cuenta y la fecha. |
| [`vendorcredits`](https://developer.intuit.com/docs/api/accounting/VendorCredit) | Los créditos de proveedor son transacciones AP que son reembolsos o créditos otorgados a proveedores. La variable `vendorcredits` incluye el identificador de crédito del proveedor, la información del artículo de línea, la información del proveedor, la cuenta AP, el importe total y la fecha. |

{style=&quot;table-layout:auto&quot;}

## Asigne un nombre a las entidades de la lista {#namelistentities}

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/docs/api/accounting/Account) | Esta tabla incluye el ID de cuenta, el nombre, el estado, el tipo, el saldo, la moneda y el tiempo de creación. |
| [`budgets`](https://developer.intuit.com/docs/api/accounting/Budget) | Esta tabla registra toda la información relacionada con los presupuestos de la empresa, incluido el ID de presupuesto, el nombre, las fechas de inicio y finalización, el tipo, el estado y los detalles. |
| [`classes`](https://developer.intuit.com/docs/api/accounting/Class) | Las clases, aplicadas a líneas de detalle de transacciones, permiten rastrear segmentos que no están vinculados a un cliente o proyecto. Esta tabla registra el ID de clase, el nombre, la subclase y el estado. |
| [`customers`](https://developer.intuit.com/docs/api/accounting/Customer) | La tabla de clientes contiene toda la información relacionada con sus clientes, incluido el ID del cliente, el nombre, las direcciones de facturación y envío, el número de teléfono y la dirección de correo electrónico. |
| [`departments`](https://developer.intuit.com/docs/api/accounting/Department) | La tabla de departamentos incluye el ID, el nombre y el tipo de departamento (departamento de subdepartamento frente a departamento de nivel superior). |
| [`employees`](https://developer.intuit.com/docs/api/accounting/Employee) | La tabla de empleados registra información sobre las personas que trabajan para su empresa. Los atributos incluyen el ID de empleado, el nombre, la dirección, el número de teléfono y la información facturable, si la empresa tiene habilitada la nómina. |
| [`items`](https://developer.intuit.com/docs/api/accounting/Item) | La tabla de artículos contiene detalles sobre los productos o servicios que vende su empresa. Esta tabla incluye el ID del artículo, el nombre, la descripción, el precio unitario, el tipo, la información de compra, la cantidad disponible y la información de cuenta de ingresos y activos. |
| [`paymentmethods`](https://developer.intuit.com/docs/api/accounting/PaymentMethod) | El cuadro de métodos de pago registra el método de pago recibido por bienes y servicios. Contiene el ID de pago, el tipo y el nombre. |
| [`taxagencies`](https://developer.intuit.com/docs/api/accounting/TaxAgency) | Esta tabla registra información sobre las agencias fiscales, incluido el ID de la agencia tributaria, y el seguimiento de información sobre impuestos para compras y ventas. |
| [`taxcodes`](https://developer.intuit.com/docs/api/accounting/TaxCode) | Los códigos fiscales se utilizan para realizar un seguimiento del estado fiscal (imponible frente a no imponible) de los productos, servicios y clientes. La tabla de códigos de impuestos incluye el identificador del código de impuestos, el nombre, la descripción, el estado, el estado imponible, el tipo impositivo y el grupo de impuestos. |
| [`taxrates`](https://developer.intuit.com/docs/api/accounting/TaxRate) | Los tipos impositivos se utilizan para calcular los pasivos fiscales. Esta tabla incluye el ID de tipo impositivo, el nombre, la descripción, la tasa, la agencia tributaria, etc. |
| [`terms`](https://developer.intuit.com/docs/api/accounting/Term) | Esta entidad representa las condiciones bajo las cuales se realizan las ventas. La tabla de términos incluye el término ID, nombre, tipo, porcentaje de descuento y días de vencimiento. |
| [`vendors`](https://developer.intuit.com/docs/api/accounting/Vendor) | La tabla de proveedores contiene información sobre los proveedores desde los que compra. Los atributos de tabla incluyen el ID del proveedor, el nombre de la empresa, el número de cuenta, el saldo de la cuenta, el estado de 1099, la dirección de facturación, el número de teléfono, la dirección de correo electrónico y la dirección web. |

{style=&quot;table-layout:auto&quot;}

## Relacionado:

* [Conexión [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
