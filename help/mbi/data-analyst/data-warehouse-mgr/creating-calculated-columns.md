---
title: Creación de columnas calculadas
description: Aprenda a consolidar datos de diferentes fuentes.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: 'https://experienceleague.adobe.com/dGzhox6Xjuvc3goSxkF2W-5yBlkgKgnOJg7YcuD2Q0s'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%
---
# Crear columnas calculadas

Al analizar los datos, resulta útil consolidar los datos de diferentes fuentes. ¿Desea agrupar los ingresos por origen de adquisición, vinculando los datos de la tabla `orders` y los datos [!DNL Google Analytics]? Tal vez desee agrupar los ingresos por sexo del cliente o unir un atributo del cliente a los datos de transacción para la segmentación. En este tema se explica cómo hacerlo.

Antes de comenzar, Adobe recomienda que revise la [Guía de tipos de columnas calculadas](../../data-analyst/data-warehouse-mgr/calc-column-types.md) para obtener información sobre los tipos de columnas que puede crear en el Administrador de Data Warehouse, junto con sus definiciones y ejemplos.

1. Para empezar, haga clic en **[!DNL Manage Data > Data Warehouse]**.

1. Haga clic en la tabla en la que desea crear una columna. Por ejemplo, si desea crear una columna `Customer Gender` para la segmentación de ingresos, debe seleccionar la tabla `sales_flat_order`.

1. Se muestra el esquema de tabla. Haga clic en **[!UICONTROL Create New Column]**.

1. Asigne un nombre a la columna. Por ejemplo, `Customer Gender`.

1. Seleccione la definición de la columna. ¡Aquí es donde la guía [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) resulta útil!

1. Para ciertos tipos de columnas, se necesita un poco más de información para crear correctamente la columna:

   * Para las columnas `One to Many` (unidas) y `Many to One` (agregadas), debe seleccionar las tablas y columnas.

   * Para un(a) `Same Table calculation`, debe seleccionar el campo de fecha deseado en la lista desplegable.

Si está creando una columna `One to Many` (combinada) o `Many to One` (agregada), debe seleccionar una ruta para conectar las dos tablas. En este paso, puede utilizar una ruta de acceso existente o crear una.

>[!NOTE]
>
>Recuerde definir correctamente la tabla como varios o uno.

* Si lo desea, puede aplicar [filtros](../../data-user/reports/ess-manage-data-filters.md) a la nueva columna.

* Cuando termine, haga clic en **[!UICONTROL Save]**.

La nueva columna aparece en la tabla actual con un estado `Pending`. Una vez que se complete la siguiente actualización, la columna estará disponible para usarla en métricas e informes.

## Mapa de referencia útil {#map}

Si tiene problemas para recordar cuáles son todas las entradas al crear una columna calculada, intente mantener este mapa de referencia a mano cuando esté construyendo:

![Ejemplo de configuración de columna calculada en Data Warehouse Manager](../../assets/Calculated_Columns_Example.png)

## Documentación relacionada

* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Tipos de columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md)
* [Creando  [!DNL Google ECommerce] dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
