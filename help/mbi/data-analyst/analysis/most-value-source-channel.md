---
title: Identificación de las fuentes y canales de marketing más valiosas
description: Obtenga información sobre algunos informes que puede utilizar para descubrir los canales de marketing más valiosos.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# Identificar fuentes de marketing exitosas

Investigó a la audiencia, creó la campaña e invirtió en algunos canales de marketing. Ahora que ha pasado algún tiempo, ¿cómo funcionan esos canales? ¿Qué canal ha atraído a los usuarios más nuevos? ¿Qué fuente ha contribuido más a sus ingresos totales?

con [!DNL MBI], puede segmentar fácilmente sus ingresos y usuarios por fuente de referencia, independientemente de si corresponde a [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) o campos de datos personalizados. Esta segmentación le permitirá encontrar sus canales de mejor rendimiento e invertir mejor su presupuesto de marketing.

En este artículo, exploramos algunos informes que puede utilizar para descubrir sus canales de marketing más valiosos:

* [Nuevos usuarios por fuentes](#newusersbysource)
* [Ingresos medios de duración por fuente de usuario](#avglifetimerev)
* [Valor de pedido promedio por origen de usuario](#avgorderval)
* [Ingresos por fecha de registro de usuario y fuentes](#revbyregdateandsource)
* [Repetir pedidos por fuente de usuario](#repeatordersbysource)

## Requisitos previos {#prereqs}

Para crear los análisis de este artículo, necesita acceder a los datos de adquisición de marketing/fuente de referencia. Si todavía no lo está rastreando, deberá traer [solicitar datos de origen de referencia de [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL MBI] antes de continuar. Además, la adición de información sobre dispositivos de usuario a los análisis le permite ver qué tecnología utilizan sus referentes.

## Nuevos usuarios por fuente {#newusersbysource}

Evaluar el rendimiento de las fuentes de referencia es clave para determinar los canales más valiosos. Este informe muestra el número de usuarios recién registrados, por fuente de adquisición, a lo largo del tiempo, lo que le permite realizar un seguimiento del rendimiento de las fuentes de referencia en la adquisición de nuevos usuarios registrados.

Para crear este informe en la variable [Report Builder](../../tutorials/using-visual-report-builder.md), añada la variable **Nuevos usuarios** métrica (o una métrica equivalente que cuenta el número de usuarios nuevos a lo largo del tiempo) en el informe. A continuación, haga lo siguiente:

1. Configure las variables [!UICONTROL Time Period] al periodo de registro que desea analizar.
1. Configure las variables [!UICONTROL Interval] a mensual.
1. Establezca [!UICONTROL Group By] a la fuente de adquisición (o referencia) y seleccione las fuentes que desee incluir.
1. Para este ejemplo, se ha utilizado la variable `stacked columns` [!UICONTROL chart type].

A continuación, se muestra un recorrido visual:

![Creación de un informe Nuevos usuarios por fuente .](../../assets/New_Users_by_source.gif)

## Ingresos medios de duración por fuente de usuario {#avglifetimerev}

Encontrar los canales que atraen a nuevos usuarios es importante, pero ¿cuán valiosos son en general esos reenvíos? Este informe muestra los ingresos medios de duración de los usuarios procedentes de fuentes de adquisición específicas a lo largo del tiempo. En otras palabras, esto le permite ver si los usuarios adquiridos a partir de una fuente en particular gastan más con usted durante su vida útil que un grupo de usuarios adquiridos a partir de una fuente diferente.

Para crear este informe en el Report Builder, agregue la variable **Ingresos medios de duración** al informe. A continuación, haga lo siguiente:

1. Configure las variables [!UICONTROL Time Period] al período de tiempo que desee analizar.
1. Configure las variables [!UICONTROL Interval] a mensual.
   [!UICONTROL Group By] a la fuente de adquisición (o referencia) y seleccione las fuentes que desee incluir.
1. Para este ejemplo, se ha utilizado la variable `line chart` tipo .

Este es un tutorial visual:

![Creación de un promedio de ingresos por duración por fuente de usuario](../../assets/Lifetime_revenue_by_user_source.gif).

En este ejemplo solo se analizan los ingresos acumulados, pero también se puede replicar este análisis para ver la [!UICONTROL Number of orders] o [!UICONTROL Distinct buyers] por fuente de referencia.

## Valor de pedido promedio por origen de usuario {#avgorderval}

Para obtener una mejor idea de cuánto dinero gastan los usuarios de una fuente de adquisición específica, puede crear un informe que observe su valor de pedido promedio. Esto le permite realizar un seguimiento de si los usuarios adquiridos a partir de una fuente concreta gastan más por pedido que los usuarios de otra fuente.

Para crear este informe en el Report Builder, agregue la variable **Valor de pedido promedio** y haga lo siguiente:

1. Configure las variables [!UICONTROL Time Period] al periodo de registro que desea analizar.
1. Configure las variables [!UICONTROL Time Interval] a mensual.
1. Establezca [!UICONTROL Group By] a la fuente de adquisición (o referencia) y seleccione las fuentes que desee incluir.
1. Para este ejemplo, se ha utilizado la variable **columnas apiladas** tipo de gráfico.

Este es un tutorial visual:

![Creación de un valor de pedido promedio por informe de origen de usuario.](../../assets/Average_order_value_by_source.gif)

## Ingresos totales por fecha de registro de usuario y fuente {#revbyregdateandsource}

El análisis de ingresos de por vida que analizamos anteriormente le permite ver los ingresos promedio de por vida de los usuarios adquiridos a partir de diferentes fuentes, pero ¿qué pasa con los ingresos totales de por vida? Este informe le permite identificar cuántos ingresos generales generan los usuarios que se registraron durante un tiempo específico y a partir de una fuente específica.

Para crear este informe en el Report Builder, agregue la variable `Revenue by user registration date` métrica. Si no [crear esta métrica](../../data-user/reports/ess-manage-data-metrics.md) ya, puede hacerlo replicando el `Revenue` y cambiar el `time stamp` al `creation date`. Después de agregar la métrica, haga lo siguiente:

1. Configure las variables [!UICONTROL Time Period] al periodo de registro que desea analizar.
1. Configure las variables [!UICONTROL Time Interval] a mensual.
1. Establezca [!UICONTROL Group By] a la fuente de adquisición (o referencia) y seleccione las fuentes que desee incluir.
1. Para este ejemplo, se ha utilizado la variable `stacked columns` tipo de gráfico.

Este es un tutorial visual:

![Creación de un total de ingresos por fecha de registro de usuario e informe de origen.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Repetir pedidos por fuente de usuario {#repeatordersbysource}

El informe Promedio de valor de pedido muestra, en promedio, cuánto gastan los usuarios adquiridos a partir de un origen en particular al realizar un pedido. Sin embargo, este informe no muestra si esos mismos usuarios son clientes repetidos. Pero con las fuentes de repetición de pedidos por parte de los usuarios, puede ver si los usuarios de una fuente en particular realizan más o menos compras repetidas.

Para crear este informe en la variable [Report Builder](../../tutorials/using-visual-report-builder.md), añada la variable **Número de pedidos** y haga lo siguiente:

1. Configure las variables [!UICONTROL Time Period] al periodo de registro que desea analizar.
1. Configure las variables [!UICONTROL Time Interval] a mensual.
1. Agregue un [!UICONTROL filter] para que solo se incluyan los usuarios con pedidos repetidos:

   Número de orden del usuario bueno a 1

1. Establezca [!UICONTROL Group By] a la fuente de adquisición (o referencia) y seleccione las fuentes que desee incluir.
1. Para este ejemplo, se ha utilizado la variable `stacked columns` tipo de gráfico.

Este es un tutorial visual:

![Creación de un informe de repetición de pedidos por origen de usuario.](../../assets/Repeat_orders_by_user_source.gif)


## Ajuste {#wrapup}

En este artículo, nos referimos a algunos análisis que puede utilizar para analizar el valor de sus canales de adquisición y marketing, pero esto es solo la punta del iceberg. Si ha creado un análisis poderoso que no hemos cubierto aquí, déjenos entrar en lo que está haciendo en los comentarios.

## Relacionado {#related}

* [Origen de referencia de pedido de seguimiento mediante [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Conexión de [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Creación [!DNL Google ECommerce] dimensiones con pedidos y datos de clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
