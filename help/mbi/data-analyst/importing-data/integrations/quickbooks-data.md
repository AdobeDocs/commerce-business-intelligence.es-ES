---
title: Datos esperados de QuickBooks
description: Aprenda a rastrear fácilmente campos de datos relevantes para su análisis.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Se esperaban [!DNL QuickBooks] datos

Después de [haber conectado tu [!DNL QuickBooks] cuenta](../../../data-analyst/importing-data/integrations/quickbooks.md), puedes usar [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis. Las siguientes tablas se crean en Data Warehouse:

Para ver todos los campos disponibles para el seguimiento, haga clic en los vínculos de la columna de nombre de tabla.

## Entidades de transacción {#transactionentities}

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | La tabla `bills` contiene información sobre transacciones AP o una solicitud de pago de un tercero. Los atributos incluyen el tipo de divisa, el tipo de cambio, el importe total, la fecha de vencimiento, el saldo, etc. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` entidades son la transacción final del pago de facturas recibidas de un proveedor. Esta tabla incluye la información del proveedor, el tipo de pago, el importe total, la fecha de transacción, etc. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | La tabla `creditmemos` registra las transacciones que son reembolsos o créditos de pagos completos y parciales. Algunos atributos incluyen el nombre del cliente, la información de facturación y envío del cliente, la cantidad y la fecha. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` incluye depósitos directos y pagos de clientes trasladados a la cuenta de activos después de haber sido retenidos en la cuenta de `Undeposited Funds`. Los atributos incluyen la cantidad, el ID de depósito y la fecha. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` son transacciones dadas a clientes que incluyen precios propuestos para un bien o servicio. Esta tabla registra el importe, la información de descuento, la información del cliente y la fecha. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` son formularios de ventas que un cliente paga más tarde. La tabla facturas registra cualquier información de depósito, fecha, artículos de línea, información de impuestos e información del cliente. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | La tabla `journalentries` registra la información de cuentas de cuentas de cuentas de cuentas por cobrar y AP, incluido el identificador de entrada de diario, la fecha de transacción y la información de artículos de línea. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Un registro `payment` incluye atributos como el identificador de pago, los importes aplicados y no aplicados, la fecha de transacción, el tipo de transacción y el estado de procesamiento. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | La tabla `purchases` representa sus gastos e incluye el identificador de compra, el tipo de pago, el importe y cualquier información de elemento de línea. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | La tabla `purchaseorders` contiene solicitudes de productos enviados a proveedores. Esta tabla incluye la información del proveedor, el ID del pedido de compra, la fecha de transacción, la información del artículo de línea, el importe total y la información de la cuenta de AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | La tabla `refundreceipts` registra los reembolsos hechos a los clientes. Los atributos incluyen el identificador de recepción de reembolso, la información de artículo de línea, el importe total, la información del cliente y el saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | La tabla `salesreceipts` registra información en los recibos de ventas entregados a los clientes, incluido el identificador de recibo de ventas, la información de artículo de línea, el importe total, la información del cliente, la fecha de transacción y los depósitos. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | La tabla `timeactivities` contiene registros de tiempo de proveedores y/o empleados e incluye el identificador de actividad horaria, información de empleado/proveedor, tiempo registrado, descripción de actividad y fecha registrada. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | La tabla `transfers` registra información sobre los fondos movidos entre cuentas. Los atributos incluyen el ID de transferencia, el importe, la información de la cuenta y la fecha. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Los créditos de proveedor son transacciones de AP que son reembolsos o créditos otorgados a proveedores. La tabla `vendorcredits` incluye el identificador de crédito del proveedor, la información de artículo de línea, la información del proveedor, la cuenta de AP, el importe total y la fecha. |

{style="table-layout:auto"}

## Entidades de lista de nombres {#namelistentities}

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Esta tabla incluye el ID de cuenta, el nombre, el estado, el tipo, el saldo, la moneda y la hora de creación. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Esta tabla registra toda la información relacionada con los presupuestos de la empresa, incluido el ID de presupuesto, el nombre, las fechas de inicio y finalización, el tipo, el estado y los detalles. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Las clases, aplicadas a líneas de detalle de transacciones, permiten realizar un seguimiento de segmentos que no están vinculados a un cliente o proyecto. Esta tabla registra el ID de clase, el nombre, la subclase y el estado. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | La tabla `customers` contiene toda la información relacionada con sus clientes, incluidos el ID del cliente, el nombre, las direcciones de facturación y envío, el número de teléfono y la dirección de correo electrónico. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | La tabla `departments` incluye el identificador, el nombre y el tipo de departamento (subdepartamento frente a departamento de nivel superior). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | La tabla `employees` registra información sobre las personas que trabajan para su compañía. Los atributos incluyen el ID de empleado, el nombre, la dirección, el número de teléfono y la información facturable, si la empresa está habilitada para nóminas. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | La tabla `items` contiene detalles sobre los productos o servicios que vende su compañía. Esta tabla incluye el ID de artículo, el nombre, la descripción, el precio unitario, el tipo, la información de compra, la cantidad física actual y la información de cuenta de activos e ingresos. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | La tabla `paymentmethods` registra el método de pago recibido por bienes y servicios. Contiene el ID de pago, el tipo y el nombre. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | Esta tabla registra información sobre las agencias fiscales, incluido el ID de la agencia tributaria y la información de seguimiento de impuestos para compras y ventas. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Los códigos de impuestos se utilizan para realizar un seguimiento del estado fiscal (imponible frente a no imponible) de los productos, servicios y clientes. La tabla `taxcodes` incluye el identificador de código de impuesto, el nombre, la descripción, el estado, el estado imponible, el tipo impositivo y el grupo de impuestos. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Los tipos impositivos se utilizan para calcular los pasivos fiscales. Esta tabla incluye el ID de tipo impositivo, el nombre, la descripción, el tipo, la agencia tributaria, etc. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Esta entidad representa los términos bajo los cuales se realizan las ventas. La tabla de términos incluye el ID de término, el nombre, el tipo, el porcentaje de descuento y los días de vencimiento. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | La tabla de proveedores contiene información sobre los proveedores a los que realiza compras. Los atributos de la tabla incluyen el ID del proveedor, el nombre de la empresa, el número de cuenta, el saldo de la cuenta, el estado 1099, la dirección de facturación, el número de teléfono, la dirección de correo electrónico y la dirección web. |

{style="table-layout:auto"}

## Relacionado:

* [Conectando [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
