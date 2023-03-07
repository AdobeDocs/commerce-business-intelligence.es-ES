---
title: ROI de marketing
description: Aprenda a configurar un tablero que realice un seguimiento del análisis de canal, incluido el retorno de la inversión en conjunto y por campaña.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# ROI de marketing

>[!NOTE]
>
>Este artículo contiene instrucciones para clientes que utilizan la arquitectura original y la nueva arquitectura. Estás en el [nueva arquitectura](../../administrator/account-management/new-architecture.md) si tiene la sección &quot;Vistas de Data Warehouse&quot; disponible después de seleccionar &quot;Administrar datos&quot; en la barra de herramientas principal.

Si está gastando dinero en publicidad en línea, quiere rastrear su retorno de este gasto y tomar decisiones basadas en datos sobre futuras inversiones. Este artículo muestra cómo configurar un tablero que realice un seguimiento del análisis de canal, incluido el retorno de la inversión en suma y por campaña.

![](../../assets/Marketing_dashboard_example.png)

Antes de empezar, debe conectar su [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), y [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) e incorporar datos adicionales sobre el gasto en publicidad en línea. Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Tablas consolidadas

**Arquitectura original:** Para reunir su gasto de varias fuentes (como [!DNL Facebook Ads] o [!DNL Google Adwords]), el Adobe recomienda crear un **tabla consolidada** de todos tus gastos publicitarios. Necesita un analista para completar este paso. Si no lo ha hecho, [presentar una solicitud de asistencia](../../guide-overview.md) con el asunto `[MARKETING ROI ANALYSIS]`y un analista crea esta tabla.

**Nueva arquitectura:** Puede seguir el ejemplo en [esta biblioteca de análisis](../../data-analyst/data-warehouse-mgr/create-dw-views.md) tema. Las tablas consolidadas ahora se conocen como Vistas de Data Warehouse en la nueva arquitectura.

## Columnas calculadas

Columnas para crear

* **`Consolidated Digital Ad Spend`** tabla
* **`Campaign name`** es creado por un analista como parte de su **[ANÁLISIS DE ROI DE MARKETING]** boleto

>[!NOTE]
>
>Consulte las diferencias de nueva arquitectura más arriba.

**Arquitecturas originales y nuevas:**

* **`sales_flat_order`** tabla
   * **`Order's GA campaign`**
      * Seleccione una definición: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Seleccione una [!UICONTROL table]: `ecommerce####`
      * Seleccione una [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Seleccione una definición: Columna combinada
      * Seleccione una [!UICONTROL table]: `ecommerce####`
      * Seleccione una [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_plain_order.increment_id = ecommerce#####.transactionId
   * **`Order's GA source`**
      * Seleccione una definición: Columna combinada
      * Seleccione una [!UICONTROL table]: `ecommerce####`
      * Seleccione una [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_plain_order.increment_id = ecommerce#####.transactionId ^




* **`customer_entity`** tabla
* **`Customer's first order GA campaign`**
   * Seleccione una definición: `Max`
   * Seleccione una [!UICONTROL table]: `sales_flat_order`
   * Seleccione una [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Seleccione una definición: `Max`
   * Seleccione una [!UICONTROL table]: `sales_flat_order`
   * Seleccione una [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_plain_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Seleccione una definición: `Max`
   * Seleccione una [!UICONTROL table]: `sales_flat_order`
   * Seleccione una [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** tabla
* **`Customer's first order GA campaign`**
   * Seleccione una definición: `Joined Column`
   * Seleccione una [!UICONTROL table]: `customer_entity`
   * Seleccione una [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Seleccione una definición: Columna combinada
   * Seleccione una [!UICONTROL table]: `customer_entity`
   * Seleccione una [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Seleccione una definición: `Joined Column`
   * Seleccione una [!UICONTROL table]: `customer_entity`
   * Seleccione una [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Métricas

* **Gasto en publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`adCost`** columna
* Ordenado por el **`date`** timestamp

* **Impresiones de publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`Impressions`** columna
* Ordenado por el **`Month`** timestamp

* **Clics en publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`adClicks`** columna
* Ordenado por el **`Month`** timestamp

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Gasto en publicidad (todo el tiempo)**
   * [!UICONTROL Metric]: Gasto en publicidad

* Métrica `A`: Gasto en publicidad
* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Adquisiciones de clientes de publicidad (todo el tiempo)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]

* Métrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **ROI del anuncio**
   * [!UICONTROL Metric]: Gasto en publicidad

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Ingresos medios a largo plazo
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Métrica `A`: `Ad Spend (hide)`
* Métrica `B`: `Ad customer acquisitions (hide)`
* Métrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Pedidos por medio de gas**
   * 

      [!UICONTROL Métrica]: `Orders`

* Métrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **ROI del anuncio por campaña**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Ingresos medios a largo plazo
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Número promedio de pedidos durante toda la vida
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica de filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* Métrica `A`: `Ad Spend` (ocultar)
* Métrica `B`: `Ad customer acquisitions`
* Métrica `C`: `Average LTV`
* Métrica `D`: `Average lifetime # of orders`
* 
   [!UICONTROL Fórmula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Métrica `H`: `adClicks`
* Métrica `I`: `Impressions`
* 
   [!UICONTROL Fórmula]: `CTR`
* 
   [!UICONTROL Fórmula]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!INTERVALO UICONTROL]: `None`
* 
   [!UICONTROL Agrupar por]: `campaign` (Utilice la campaña &quot;Primer pedido del cliente&quot; para métricas de tabla de gasto que no sean de publicidad)
* 

   [!UICONTROL Chart Type]: `Table`

Si tiene alguna pregunta mientras realiza este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### Relacionado

* [Prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../analysis/utm-attributes.md)
