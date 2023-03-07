---
title: Aumento del retorno de la inversión en sus campañas publicitarias
description: Obtenga información sobre distintos métodos para evaluar el rendimiento de la campaña.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Campañas publicitarias y ROI

MBI le permite [combinar los datos de costes e ingresos de publicidad](../../data-analyst/importing-data/integrations/google-adwords.md) de la base de datos. Esto le ayuda a identificar qué campañas tienen el ROI más alto. Este artículo explora algunos métodos diferentes para evaluar el rendimiento de la campaña.

## Requisitos previos

* Importe los datos de costes de publicidad:
   * [Conecte su [!DNL Google AdWords] hasta [!DNL MBI]](../importing-data/integrations/google-adwords.md): Esto sincroniza su [!DNL Adwords] gastar en [!DNL MBI]
   * [Cargar otros datos de costes de publicidad](../importing-data/connecting-data/import-offline-ad-data.md): Se recomienda para canales sin un conector directo a [!DNL MBI]
   * Si importa datos de coste de varios orígenes, puede [consolidar](../../best-practices/consolidating-your-tables.md) los datos de [!DNL MBI]. Simplemente [enviar un ticket de asistencia](../../guide-overview.md).
* [Seguimiento de datos de canales de adquisición de usuarios](../analysis/google-track-user-acq.md)

## Campañas de adquisición de usuarios

Las campañas dirigidas a la adquisición de usuarios se pueden medir desde muchas perspectivas, entre ellas:

1. El número de usuarios nuevos adquiridos de las campañas
1. La tasa de conversión del registro a la compra de campañas.
1. El ROI de las campañas en función del valor promedio de duración del usuario (LTV)

Los análisis (1) y (2) anteriores se exploran en un tutorial independiente sobre [identificación de los canales de marketing principales](../analysis/most-value-source-channel.md). Aquí puede explorar el análisis (3) para medir el ROI de la campaña a lo largo del tiempo. Esto indica si los usuarios obtenidos de una campaña en particular generaron suficientes ingresos durante toda la vida útil para cubrir el coste de adquisición.

>[!NOTE]
>
>En este ejemplo se supone que todos los costes de campaña se utilizaron exclusivamente para adquirir nuevos usuarios. En realidad, el coste de su campaña también se comparte con la adquisición de visitas no convertidas, compradores repetidos y similares. Suponiendo que todo el coste se utiliza para adquirir nuevos usuarios registrados, el ROI resultante corresponde al peor escenario (coste por adquisición más alto). Puede estar seguro de que el ROI real es mayor que su cálculo.
>
>Ejemplo: suponiendo que gastó 20 $ en una campaña que generó 10 usuarios nuevos y 10 compradores repetidos, el coste real por usuario nuevo es de 1 $. Pero, suponiendo que todo el coste se destinó a la adquisición de nuevos usuarios, el coste por adquisición es de 2 dólares).

**1. Comience creando un gráfico que segmente el coste de la publicidad por campañas:**

1. Crear un [!UICONTROL Metric] que suma su gasto en el tiempo
1. Ir a [!UICONTROL Data > Metrics]
1. Seleccionar `Add New Metric` y seleccione la [!DNL `Adwords...`] que está grabando su [!DNL AdWords] datos de costes.
1. En el editor de métricas, asigne un nombre a la métrica (por ejemplo, [!UICONTROL AdWord Cost])
1. Con los menús desplegables, realice una **Sum** en el `adCost` en la columna [!DNL Adwords...] tabla (cambio) ordenada por el `date` columna.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Clic `Back to Metric List` en la parte superior y vaya a cualquier panel.

1. Creación de un informe en el que se indique el gasto de los segmentos por campañas
1. En cualquier tablero, haga clic en [!UICONTROL Add Report > Create report]
1. Seleccione el [!UICONTROL Adword Cost] métrica que acaba de crear
1. Configure las variables [!UICONTROL Time period] hasta `All-time`, y [!UICONTROL Interval] hasta `None`
1. En el `Group by` pestaña, añadir `campaign` as [!UICONTROL grouping field]y haga clic en `Add All` en la casilla.
1. Este informe muestra sus [!DNL AdWords] coste por campañas

**2. Cree un informe que cuente los nuevos usuarios por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create report]**
1. Seleccione el `New users` métrica que cuenta el número de nuevos usuarios registrados a lo largo del tiempo
1. Configure las variables [!UICONTROL Time period] hasta `All-time`, y [!UICONTROL Interval] hasta `None`
1. En el `Group by` pestaña, añadir `campaign` as `grouping field`y haga clic en **`Add All`** en la casilla
1. Este informe muestra los usuarios registrados permanentes por campañas

**3. Cree un informe que segmente el LTV del usuario promedio por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create report]**
1. Seleccione el `Average lifetime revenue` métrica que calcula los ingresos medios por duración de un usuario
1. Configure las variables [!UICONTROL Time period] hasta `All-time`, y [!UICONTROL Interval] hasta `None`
1. En el `Group by` pestaña, añadir `campaign` o `utm\_campaign` as [!UICONTROL grouping field]y haga clic en `Add All` en la casilla
1. Este informe muestra los ingresos medios por duración de los usuarios según las campañas

**Finalmente, calcule el ROI de la campaña reuniendo estos tres análisis en un informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Añada como entrada las tres métricas utilizadas anteriormente. A cada uno se le asigna una letra (por ejemplo,\[`A`\], \[`B`\] y \[`C`\])
1. [!UICONTROL Cost]: Añada el coste de la métrica AdWords. Esta es la variable \[A\]. Devuelve el coste por campañas.
1. [!UICONTROL Users]: Añada la métrica Nuevos usuarios, que es la variable \[B\]. Devuelve el número de usuarios por campañas.
1. [!UICONTROL LTV]: Añada la métrica Ingresos de duración promedio - esta es la variable \[`C`\]. Esto devuelve LTV por campañas.

1. Haga clic en el icono de ocultar situado junto a la palabra Gráfico para poder centrarse en la tabla
1. Ahora utilice `Add Formula` para combinar estas métricas, haga lo siguiente:
1. [!UICONTROL ROI]: introduzca la fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns`, y \[`C`\] `LTV by campaigns`. Devuelve la proporción de (LTV promedio del usuario - coste promedio por adquisición) / (coste promedio por adquisición)
1. [!UICONTROL Avg Return per User]: introduzca la fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Devuelve el margen promedio realizado sobre un usuario calculando (LTV de usuario promedio) - (coste promedio por adquisición).
1. [!UICONTROL CPA]: introduzca la fórmula **`\[A\]/\[B\]`**. Devuelve el coste por adquisición real de la campaña.
1. Otras métricas potenciales que se deben incluir en [!DNL AdWords] los datos incluyen sumas de  `Impressions` y `adClicks` (desde [!DNL AdWords] datos), junto con el total `number of orders` realizado mediante una campaña determinada.
1. También puede resultar interesante calcular el ROI en función de la LTV 30 días y 90 días después de que un usuario se registra o realiza una primera compra.

1. Puede hacer clic y arrastrar las métricas y fórmulas para reordenar las columnas del informe
1. Asigne un nombre al informe y asegúrese de guardarlo como tabla.

## Campañas de productos

¿Está ejecutando anuncios específicos de productos? Si es así, puede medir el retorno de la inversión de esas campañas calculando los ingresos / costes de productos específicos.

>[!NOTE]
>
>En este ejemplo se supone que todos los costes de campaña se utilizaron exclusivamente para generar compras de productos específicos. Suponiendo que todo el coste se haya gastado en la generación de compras, el ROI resultante corresponde al peor escenario (el coste por compra más alto). Puede estar seguro de que el ROI real es mayor que este cálculo. Ejemplo: suponiendo que gastó 20 $ en una campaña que generó 10 usuarios nuevos y 10 compras, el coste real por compra es de 1 $. Suponiendo que todo el coste se destinó a adquirir nuevos usuarios, el coste por compra es de 2 $).*

Antes de empezar, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para unir las siguientes dimensiones a la tabla de elementos de línea (`sales\_flat\_order\_item, order\_item`):

* Origen del pedido (si solo realiza el seguimiento del origen de referencia a nivel de usuario, únase al origen del usuario)
* Campaña del pedido (si solo rastrea el origen de referencia en el nivel de usuario, únase a la campaña del usuario)
* Medio del pedido (si solo rastrea el origen de referencia en el nivel de usuario, únase al medio del usuario)

**1. Ahora comience creando un gráfico que devuelva ingresos por campaña para productos específicos:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Seleccione el `Revenue by items` métrica que calcula los ingresos en el nivel de artículos de línea
1. Configure las variables [!UICONTROL Time period] hasta `All-time`, y [!UICONTROL Interval] hasta `None`
1. En el `Filter by` pestaña, añadir `product name 'IN'` Product `A`, Producto `B`, Producto `C`, ...&quot; e incluya todos los nombres de productos a los que se dirija la campaña separados por coma (por ejemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. En el `Group by` pestaña, añadir `order's campaign` o `order's utm\_campaign` as `grouping` y haga clic en **[!UICONTROL Add All]** en la casilla
1. Este informe muestra los ingresos de productos específicos por campañas

**2. Para calcular el retorno de la inversión, vuelva a combinar las métricas en un informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Añada el `Revenue by items` métrica, siguiendo las instrucciones de filtro y agrupar por de la campaña para productos específicos informe anterior y haga clic en **[!UICONTROL Hide]** por debajo del valor escalar de la métrica
1. Ahora añada el [!DNL AdWords Cost] métrica, siguiendo las instrucciones de filtro y agrupar por del `Ad cost by campaigns` informe que ha explorado en `User acquisition campaigns` sección anterior; a continuación, haga clic en **[!UICONTROL Hide]** por debajo del valor escalar de la métrica
1. Con estas métricas en su lugar, agregue fórmulas:
1. [!UICONTROL ROI]: introduzca la fórmula `\[A\]/\[B\]`, si `\[A\]` representa `Revenue per campaign for specific product(s)` y `\[B\]` representa `Ad cost by campaigns`. Devuelve la proporción de (ingresos para productos específicos) / (coste de la campaña)
1. [!UICONTROL Return]: introduzca la fórmula `\[A\]-\[B\]`. Devuelve el margen promedio realizado sobre un usuario calculando (LTV de usuario promedio) - (coste promedio por adquisición)
1. (Opcional) [!UICONTROL Revenue]: mostrar `Revenue by items` métrica para ver los ingresos de productos específicos por campañas
1. (Opcional) [!UICONTROL Cost]: mostrar `AdWords Cost` métrica para ver el coste de las campañas

1. Asigne un nombre al informe y asegúrese de guardarlo como una tabla

**3. Repita los pasos 1 y 2 anteriores para cada uno de los productos o grupos de productos anunciados.**

## Documentación relacionada

* [Rastrear origen de referencia de pedido mediante [!DNL Google Analytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../analysis/track-usr-dev-browser.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../analysis/utm-attributes.md)
* [Cinco prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
