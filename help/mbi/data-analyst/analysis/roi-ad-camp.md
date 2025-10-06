---
title: Aumento del retorno de la inversión en sus campañas publicitarias
description: Obtenga información sobre distintos métodos para evaluar el rendimiento de la campaña.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Campañas de Advertising y ROI

[!DNL Adobe Commerce Intelligence] le permite [combinar fácilmente los datos de costos de publicidad con los datos de ingresos](../../data-analyst/importing-data/integrations/google-adwords.md) de su base de datos. Esto le ayuda a identificar qué campañas tienen el retorno de la inversión (ROI) más alto. En este tema se exploran varios métodos diferentes para evaluar el rendimiento de la campaña.

## Requisitos previos

* Importe los datos de costes de publicidad:
   * [Conecta tu [!DNL Google AdWords] a [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): Esto sincroniza tu gasto de [!DNL Adwords] en [!DNL Commerce Intelligence]
   * [Cargar otros datos de costos de publicidad](../importing-data/connecting-data/import-offline-ad-data.md): Se recomienda para canales sin conector directo a [!DNL Commerce Intelligence]
   * Si importa datos de costo de varios orígenes, puede [consolidar](../../best-practices/consolidating-your-tables.md) los datos de [!DNL Commerce Intelligence]. Simplemente [envíe un ticket de asistencia](../../guide-overview.md#Submitting-a-Support-Ticket).
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
>Ejemplo: suponiendo que gastó 20 $ en una campaña que generó 10 usuarios nuevos y 10 compradores repetidos, el coste real por usuario nuevo es de 1 $. Pero, suponiendo que todo el coste se destinó a la adquisición de nuevos usuarios, el coste por adquisición es de 2 dólares.

**1. Comience creando un gráfico que segmente el costo del anuncio por campañas:**

1. Crear un(a) [!UICONTROL Metric] que sume su gasto a lo largo del tiempo
1. Ir a [!UICONTROL Data > Metrics]
1. Seleccione `Add New Metric` y seleccione la tabla [!DNL `Adwords...`] que está registrando los datos de costo de [!DNL AdWords].
1. En el editor de métricas, asigne un nombre a la métrica (por ejemplo, [!UICONTROL AdWord Cost])
1. Con los menús desplegables, realice una **Sum** en la columna `adCost` de la tabla [!DNL Adwords...] (Cambiar) ordenada por la columna `date`.
   ![Mensaje de éxito después de agregar una nueva métrica](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Haga clic en `Back to Metric List` en la parte superior y vaya a cualquier panel.

1. Creación de un informe en el que se indique el gasto de los segmentos por campañas
1. En cualquier tablero, haga clic en [!UICONTROL Add Report > Create report]
1. Seleccione la métrica [!UICONTROL Adword Cost] que acaba de crear
1. Establecer [!UICONTROL Time period] en `All-time` y [!UICONTROL Interval] en `None`
1. En la ficha `Group by`, agregue `campaign` como [!UICONTROL grouping field] y haga clic en `Add All` en el cuadro.
1. Este informe muestra el costo total de [!DNL AdWords] por campañas

**2. Cree un informe que cuente los nuevos usuarios por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create report]**
1. Seleccione la métrica `New users` que cuenta el número de nuevos usuarios registrados a lo largo del tiempo
1. Establecer [!UICONTROL Time period] en `All-time` y [!UICONTROL Interval] en `None`
1. En la ficha `Group by`, agregue `campaign` como `grouping field` y haga clic en **`Add All`** en el cuadro
1. Este informe muestra los usuarios registrados permanentes por campañas

**3. Cree un informe que segmente la LTV promedio de usuarios por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create report]**
1. Seleccione la métrica `Average lifetime revenue` que calcula los ingresos promedio de un usuario durante su vida útil
1. Establecer [!UICONTROL Time period] en `All-time` y [!UICONTROL Interval] en `None`
1. En la ficha `Group by`, agregue `campaign` o `utm\_campaign` como [!UICONTROL grouping field] y haga clic en `Add All` en el cuadro
1. Este informe muestra los ingresos medios por duración de los usuarios según las campañas

**Por último, calcule el retorno de la inversión de la campaña reuniendo estos tres análisis en un informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Añada como entrada las tres métricas utilizadas anteriormente. A cada uno se le asigna una letra (por ejemplo,\[`A`\], \[`B`\] y \[`C`\])
1. [!UICONTROL Cost]: agregue el coste de la métrica AdWords. Se trata de la variable \[A\]. Devuelve el coste por campañas.
1. [!UICONTROL Users]: agregue la métrica Nuevos usuarios - esta es la variable \[B\]. Devuelve el número de usuarios por campañas.
1. [!UICONTROL LTV]: agregue la métrica Ingresos de duración promedio - esta es la variable \[`C`\]. Esto devuelve LTV por campañas.

1. Haga clic en el icono de ocultar situado junto a la palabra Gráfico para poder centrarse en la tabla
1. Ahora use `Add Formula` para combinar estas métricas, de la siguiente manera:
1. [!UICONTROL ROI]: escriba la fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns` y \[`C`\] `LTV by campaigns`. Devuelve la proporción de (LTV promedio del usuario - coste promedio por adquisición) / (coste promedio por adquisición)
1. [!UICONTROL Avg Return per User]: escriba la fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Devuelve el margen promedio realizado sobre un usuario calculando (LTV de usuario promedio) - (coste promedio por adquisición).
1. [!UICONTROL CPA]: escriba la fórmula **`\[A\]/\[B\]`**. Devuelve el coste por adquisición real de la campaña.
1. Otras métricas potenciales que se pueden incluir de [!DNL AdWords] datos incluyen sumas de `Impressions` y `adClicks` (de [!DNL AdWords] datos), junto con el total de `number of orders` realizadas a través de una campaña en particular.
1. También puede resultar interesante calcular el ROI en función de la LTV 30 días y 90 días después de que un usuario se registra o realiza una primera compra.

1. Puede hacer clic y arrastrar las métricas y fórmulas para reordenar las columnas del informe
1. Asigne un nombre al informe y asegúrese de guardarlo como tabla.

## Campañas de productos

¿Está ejecutando anuncios específicos de productos? Si es así, puede medir el retorno de la inversión de esas campañas calculando los ingresos / costes de productos específicos.

>[!NOTE]
>
>En este ejemplo se supone que todos los costes de campaña se utilizaron exclusivamente para generar compras de productos específicos. Suponiendo que todo el coste se haya gastado en la generación de compras, el ROI resultante corresponde al peor escenario (el coste por compra más alto). Puede estar seguro de que el ROI real es mayor que este cálculo. Ejemplo: suponiendo que gastó 20 $ en una campaña que generó 10 usuarios nuevos y 10 compras, el coste real por compra es de 1 $. Suponiendo que todo el coste se destina a adquirir nuevos usuarios, el coste por compra es de 2 dólares.

Antes de comenzar, [envíe un vale de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) para unir las siguientes dimensiones a la tabla de elementos de línea (`sales\_flat\_order\_item, order\_item`):

* Origen del pedido (si solo realiza el seguimiento del origen de referencia a nivel de usuario, únase al origen del usuario)
* Campaña del pedido (si solo rastrea el origen de referencia en el nivel de usuario, únase a la campaña del usuario)
* Medio del pedido (si solo rastrea el origen de referencia en el nivel de usuario, únase al medio del usuario)

**1. Ahora comience creando un gráfico que devuelva ingresos por campaña para productos específicos:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Seleccione la métrica `Revenue by items` que calcula los ingresos en el nivel de elementos de línea
1. Establecer [!UICONTROL Time period] en `All-time` y [!UICONTROL Interval] en `None`
1. En la ficha `Filter by`, agregue `product name 'IN'` producto `A`, producto `B`, producto `C`, ...&quot; e incluya todos los nombres de productos dirigidos por su campaña separados por una coma (por ejemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. En la ficha `Group by`, agregue `order's campaign` o `order's utm\_campaign` como campo `grouping` y haga clic en **[!UICONTROL Add All]** en el cuadro
1. Este informe muestra los ingresos de productos específicos por campañas

**2. Para calcular el retorno de la inversión, vuelva a combinar las métricas en un informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Agregue la métrica `Revenue by items`, siguiendo el filtro y agrupe por instrucciones del informe de campaña para productos específicos anterior y haga clic en **[!UICONTROL Hide]** debajo del valor escalar de la métrica
1. Ahora agregue la métrica [!DNL AdWords Cost], siguiendo el filtro y agrupe según las instrucciones del informe `Ad cost by campaigns` que exploró en la sección `User acquisition campaigns` anterior; a continuación, haga clic en **[!UICONTROL Hide]** debajo del valor escalar de la métrica
1. Con estas métricas en su lugar, agregue fórmulas:
1. [!UICONTROL ROI]: escriba la fórmula `\[A\]/\[B\]`, si `\[A\]` representa `Revenue per campaign for specific product(s)` y `\[B\]` representa `Ad cost by campaigns`. Devuelve la proporción de (ingresos para productos específicos) / (coste de la campaña)
1. [!UICONTROL Return]: escriba la fórmula `\[A\]-\[B\]`. Devuelve el margen promedio realizado sobre un usuario calculando (LTV de usuario promedio) - (coste promedio por adquisición)
   1. (Opcional) [!UICONTROL Revenue]: muestre la métrica `Revenue by items` para ver los ingresos de productos específicos por campaña
   1. (Opcional) [!UICONTROL Cost]: muestre la métrica `AdWords Cost` para ver el costo de las campañas

1. Asigne un nombre al informe y asegúrese de guardarlo como una tabla

**3. Repita los pasos 1 y 2 anteriores para cada uno de los productos o grupos de productos anunciados.**

## Documentación relacionada

* [Rastrear origen de referencia de pedidos a través de  [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de los datos de dispositivos de usuario, exploradores y SO en la base de datos](../analysis/track-usr-dev-browser.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecta tu cuenta de  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [¿Cómo funciona la atribución de  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
* [Cinco prácticas recomendadas para el etiquetado UTM en  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
