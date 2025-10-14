---
title: Identificación De Los Canales Y Las Fuentes De Marketing Más Valiosas
description: Obtenga información sobre algunos informes que puede utilizar para descubrir los canales de marketing más valiosos.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identificación de fuentes de marketing correctas

Investigaste tu audiencia, creaste tu campaña, invertiste en algunos canales de marketing. Ahora que ha pasado algún tiempo, ¿cómo van esos canales? ¿Qué canal ha atraído a la mayoría de los usuarios nuevos? ¿Qué fuente ha contribuido más a sus ingresos totales?

Con [!DNL Adobe Commerce Intelligence], puede segmentar fácilmente sus ingresos y usuarios por origen de referencia, ya corresponda a [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en) o a campos de datos personalizados. Esta segmentación le permite encontrar los canales con mejor rendimiento e invertir mejor su presupuesto de marketing.

En este tema se exploran algunos informes que puede utilizar para descubrir los canales de marketing más valiosos:

* [Nuevos usuarios por fuentes](#newusersbysource)
* [Ingresos promedio por duración por origen de usuario](#avglifetimerev)
* [Valor de pedido promedio por origen de usuario](#avgorderval)
* [Ingresos por fecha y origen de registro de usuario](#revbyregdateandsource)
* [Repetir pedidos por origen de usuario](#repeatordersbysource)

## Requisitos previos {#prereqs}

Para generar los análisis de este tema, necesita acceder a los datos de adquisición de marketing/fuente de referencia. Si aún no lo está rastreando, debe traer [datos de origen de referencia de pedido de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) a [!DNL Adobe Commerce Intelligence] para poder continuar. Además, al agregar información del dispositivo del usuario a los análisis, puede ver qué tecnología utilizan las referencias.

## Nuevos usuarios por origen {#newusersbysource}

La evaluación del rendimiento de las fuentes de referencia es clave para determinar los canales más valiosos. Este informe muestra el número de usuarios recién registrados, por fuente de adquisición, a lo largo del tiempo, lo que le permite realizar un seguimiento del rendimiento de las fuentes de referencia al adquirir nuevos usuarios registrados.

Para crear este informe en [Report Builder](../../tutorials/using-visual-report-builder.md), agregue la métrica **Nuevos usuarios** (o una métrica equivalente que cuente el número de nuevos usuarios a lo largo del tiempo) al informe. A continuación, haga lo siguiente:

1. Establezca [!UICONTROL Time Period] en el período de registro que desee analizar.
1. Establezca [!UICONTROL Interval] en mensual.
1. Establezca [!UICONTROL Group By] en el origen de adquisición (o de referencia) y seleccione los orígenes que desea incluir.
1. Este ejemplo utiliza `stacked columns` [!UICONTROL chart type].

Este es un tutorial visual:

![Creando un informe de nuevos usuarios por origen.](../../assets/New_Users_by_source.gif)

## Ingresos promedio por duración por origen de usuario {#avglifetimerev}

Encontrar los canales que atraen a nuevos usuarios es importante, pero ¿cuán valiosas son esas referencias en general? Este informe muestra los ingresos promedio por duración de usuarios de fuentes de adquisición específicas a lo largo del tiempo. En otras palabras, esto le permite ver si los usuarios adquiridos de una fuente concreta gastan más con usted a lo largo de su vida que un grupo de usuarios adquiridos de una fuente diferente.

Para crear este informe en Report Builder, agregue la métrica **Ingresos promedio por duración** al informe. A continuación, haga lo siguiente:

1. Establezca [!UICONTROL Time Period] en el período de tiempo que desee analizar.
1. Establezca [!UICONTROL Interval] en mensual.
   [!UICONTROL Group By] al origen de adquisición (o referencia) y seleccione los orígenes que desea incluir.
1. Este ejemplo utiliza el tipo `line chart`.

Este es un tutorial visual:

![Creando un ingreso promedio de por vida por origen de usuario](../../assets/Lifetime_revenue_by_user_source.gif).

Este ejemplo solo observa los ingresos por duración, pero también puede replicar este análisis para ver [!UICONTROL Number of orders] o [!UICONTROL Distinct buyers] por origen de referencia.

## Valor de pedido promedio por origen de usuario {#avgorderval}

Para obtener una mejor idea de cuánto dinero gastan los usuarios de una fuente de adquisición específica, puede crear un informe que observe su valor de pedido promedio. Esto le permite rastrear si los usuarios adquiridos de una fuente en particular gastan más por pedido que los usuarios de otra fuente.

Para crear este informe en Report Builder, agregue la métrica **Valor de pedido promedio** y, a continuación, haga lo siguiente:

1. Establezca [!UICONTROL Time Period] en el período de registro que desee analizar.
1. Establezca [!UICONTROL Time Interval] en mensual.
1. Establezca [!UICONTROL Group By] en el origen de adquisición (o de referencia) y seleccione los orígenes que desea incluir.
1. Este ejemplo usa el tipo de gráfico **columnas apiladas**.

Este es un tutorial visual:

![Creando un valor de pedido promedio por informe de origen de usuario.](../../assets/Average_order_value_by_source.gif)

## Ingresos totales por fecha y origen de registro de usuario {#revbyregdateandsource}

El análisis de ingresos de duración que se ha cubierto anteriormente le permite observar los ingresos promedio de duración de los usuarios adquiridos de diferentes fuentes, pero ¿qué sucede con los ingresos totales de duración? Este informe permite identificar cuántos ingresos generales generan los usuarios que se registraron durante un tiempo específico y que proceden de una fuente específica.

Para crear este informe en Report Builder, agregue la métrica `Revenue by user registration date`. Si aún no ha [creado esta métrica](../../data-user/reports/ess-manage-data-metrics.md), puede hacerlo replicando la métrica `Revenue` y cambiando `time stamp` a `creation date` del usuario. Después de agregar la métrica, haga lo siguiente:

1. Establezca [!UICONTROL Time Period] en el período de registro que desee analizar.
1. Establezca [!UICONTROL Time Interval] en mensual.
1. Establezca [!UICONTROL Group By] en el origen de adquisición (o de referencia) y seleccione los orígenes que desea incluir.
1. Este ejemplo utiliza el tipo de gráfico `stacked columns`.

Este es un tutorial visual:

![Creando un informe de ingresos totales por fecha de registro de usuario y origen.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repetir pedidos por origen de usuario {#repeatordersbysource}

El informe Valor de pedido promedio muestra, de media, cuántos usuarios adquiridos de un origen determinado invierten al realizar un pedido. Sin embargo, este informe no muestra si esos mismos usuarios son clientes repetidos. Sin embargo, con las fuentes de Repetir pedidos de los usuarios, puede ver si los usuarios de una fuente en particular realizan compras más o menos repetidas.

Para crear este informe en [Report Builder](../../tutorials/using-visual-report-builder.md), agregue la métrica **Número de pedidos** y haga lo siguiente:

1. Establezca [!UICONTROL Time Period] en el período de registro que desee analizar.
1. Establezca [!UICONTROL Time Interval] en mensual.
1. Agregue un [!UICONTROL filter] para que solo se incluyan los usuarios con pedidos repetidos:

   Número de pedido del usuario mayor que 1

1. Establezca [!UICONTROL Group By] en el origen de adquisición (o de referencia) y seleccione los orígenes que desea incluir.
1. Este ejemplo utiliza el tipo de gráfico `stacked columns`.

Este es un tutorial visual:

![Creando un informe de origen de pedidos repetidos por usuario.](../../assets/Repeat_orders_by_user_source.gif)


## Ajuste {#wrapup}

En este tema se han mencionado algunos análisis que puede utilizar para analizar el valor de los canales de adquisición y marketing, pero esto es solo la punta del iceberg.

## Relacionado {#related}

* [Origen de referencia de pedido de seguimiento mediante  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Conectando tu cuenta de  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [Creando  [!DNL Google ECommerce] dimensiones con pedidos y datos de clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Prácticas recomendadas para el etiquetado UTM en  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
