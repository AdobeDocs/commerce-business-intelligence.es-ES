---
title: ROI de marketing
description: Obtenga información sobre cómo configurar un tablero que rastree su análisis de canal, incluido el ROI en conjunto y por campaña.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# ROI de marketing

>[!NOTE]
>
>Este artículo contiene instrucciones para clientes que utilizan la arquitectura original y la nueva arquitectura. Usted está en el [nueva arquitectura](../../administrator/account-management/new-architecture.md) si tiene disponible la sección &quot;Vistas de Data Warehouse&quot; después de seleccionar &quot;Administrar datos&quot; en la barra de herramientas principal.

Si gasta dinero en publicidad en línea, inevitablemente querrá rastrear su retorno en este gasto y tomar decisiones basadas en datos sobre futuras inversiones. En este artículo, demostramos cómo configurar un panel que realice un seguimiento del análisis de canal, incluido el ROI en conjunto y por campaña.

![](../../assets/Marketing_dashboard_example.png)

Antes de comenzar, debe conectar con su [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)y [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) además de incorporar cualquier dato adicional sobre gastos de publicidad en línea. Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Tablas consolidadas

**Arquitectura original:** Para reunir el gasto de varias fuentes (como [!DNL Facebook Ads] o [!DNL Google Adwords]), se recomienda crear un **tabla consolidada** de todo el gasto en publicidad. Necesitará un analista para completar este paso por usted. Si todavía no lo ha hecho, [presentar una solicitud de asistencia](../../guide-overview.md) con el asunto `[MARKETING ROI ANALYSIS]`, y un analista creará esta tabla.

**Nueva arquitectura:** Puede seguir el ejemplo establecido en [esta biblioteca de análisis](../../data-analyst/data-warehouse-mgr/create-dw-views.md) tema. Las tablas consolidadas ahora se conocen como Vistas de Data Warehouse de la nueva arquitectura.

## Columnas calculadas

Columnas que crear

* **`Consolidated Digital Ad Spend`** tabla
* **`Campaign name`** será creado por un analista como parte de su **[ANÁLISIS DE ROI DE MARKETING]** ticket

>[!NOTE]
>
>Consulte más arriba para ver las nuevas diferencias de arquitectura.

**Arquitecturas originales y nuevas:**

* **`sales_flat_order`** tabla
   * **`Order's GA campaign`**
      * Seleccione una definición: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Seleccione un [!UICONTROL table]: `ecommerce####`
      * Seleccione un [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Seleccione una definición: Columna unida
      * Seleccione un [!UICONTROL table]: `ecommerce####`
      * Seleccione un [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_plana_order.increment_id = ecommerce####.transactionId
   * **`Order's GA source`**
      * Seleccione una definición: Columna unida
      * Seleccione un [!UICONTROL table]: `ecommerce####`
      * Seleccione un [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_plana_order.increment_id = ecommerce####.transactionId ^




* **`customer_entity`** tabla
* **`Customer's first order GA campaign`**
   * Seleccione una definición: `Max`
   * Seleccione un [!UICONTROL table]: `sales_flat_order`
   * Seleccione un [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Seleccione una definición: `Max`
   * Seleccione un [!UICONTROL table]: `sales_flat_order`
   * Seleccione un [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_plana_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Seleccione una definición: `Max`
   * Seleccione un [!UICONTROL table]: `sales_flat_order`
   * Seleccione un [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** tabla
* **`Customer's first order GA campaign`**
   * Seleccione una definición: `Joined Column`
   * Seleccione un [!UICONTROL table]: `customer_entity`
   * Seleccione un [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Seleccione una definición: Columna unida
   * Seleccione un [!UICONTROL table]: `customer_entity`
   * Seleccione un [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Seleccione una definición: `Joined Column`
   * Seleccione un [!UICONTROL table]: `customer_entity`
   * Seleccione un [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Métricas

* **Gasto en publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`adCost`** column
* Solicitado por el **`date`** timestamp

* **Impresiones de publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`Impressions`** column
* Solicitado por el **`Month`** timestamp

* **Clics en publicidad**
* En el **`Consolidated Digital Ad Spend`** tabla
* Esta métrica realiza una **Sum**
* En el **`adClicks`** column
* Solicitado por el **`Month`** timestamp

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a métricas](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Gasto en publicidad (todo el tiempo)**
   * [!UICONTROL Metric]: Gasto en publicidad

* Métrica `A`: Gasto en publicidad
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Adjuntar adquisiciones de clientes (todo el tiempo)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]

* Métrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **ROI de los anuncios**
   * [!UICONTROL Metric]: Gasto en publicidad

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Ingresos medios de duración
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Métrica `A`: `Ad Spend (hide)`
* Métrica `B`: `Ad customer acquisitions (hide)`
* Métrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [Intervalo !UICONTROL]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Pedidos por medio de ga**
   * 

      [!UICONTROL Métrica]: `Orders`

* Métrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **ROI de los anuncios por campaña**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Ingresos medios de duración
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
   * [!UICONTROL Metric]: Cantidad promedio de pedidos acumulados
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Lógica del filtro: ([`A`] O [`B`] O [`C`]) Y [`D`]
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
   [Intervalo !UICONTROL]: `None`
* 
   [!UICONTROL Grupo por]: `campaign` (Usar la campaña &quot;del primer pedido del cliente&quot; para métricas de tabla que no sean de gasto publicitario)
* 

   [!UICONTROL Chart Type]: `Table`

Si tiene alguna pregunta al crear este análisis, o simplemente desea contactar con nuestro equipo de servicios profesionales, [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### Relacionado

* [Prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../analysis/utm-attributes.md)
