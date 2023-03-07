---
title: Creación de un tablero para inversores
description: Aprenda a crear un tablero para los inversores.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Crear tablero del inversor

Muchos clientes trabajan con inversores y necesitan compartir información de la plataforma, pero los paneles que crea para tomar decisiones comerciales diarias pueden no ser lo que busca un inversor. A continuación se describen algunas prácticas recomendadas para crear un tablero completo, pero sencillo, ideal para compartir con inversores activos y potenciales.

Esto es lo que necesita para crear informes para su tablero de inversores:

## Informes escalares

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Informes visuales

* **[!UICONTROL Revenue by quarter]**
   * Métrica - Ingresos
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Métrica: ingresos por primer pedido
   * Filtro: el número de pedido del usuario es igual a 1
   * Métrica 2: Ingresos de pedidos repetidos
      * Filtro: el número de pedido del usuario es bueno que 1
   * Desmarque la casilla de verificación de Varios ejes Y
   * Cambiar a gráfico de columnas apiladas
* **[!UICONTROL AOV by quarter]**
   * Métrica 1 - Ingresos
      * Ocultar esta métrica
   * Métrica 2: número de pedidos
      * Ocultar esta métrica
   * Fórmula: AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Métrica - Ingresos
   * Agrupar por nombre de cliente `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Métrica: ingresos de productos
      * Ocultar el gráfico
      * Agrupar por nombre de producto. Seleccione todos los productos.
      * Establezca el intervalo de tiempo en Todo el tiempo
      * Establezca el intervalo de tiempo en Ninguno
      * En &quot;Mostrar arriba/abajo&quot;, mostrar solo los 10 principales clasificados por Beneficio del producto
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Métrica: compradores diferentes
      * Perspectiva: acumulativa
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sesiones

Con un [!DNL Google Analytics] Integración de, puede incluir informes sobre:

* Visitas al sitio
* Tasa de conversión

Con el [Servicios de enriquecimiento de datos de Commerce](https://business.adobe.com/products/magento/magento-commerce.html), puede incluir informes sobre:

* Clientes únicos por estado/región, edad, sexo.

## Otros consejos

* Utilice un enfoque claro y conciso [convención de nomenclatura](../best-practices/naming-elements.md)
* Uso compartido del tablero con usuarios inversores
* O bien, envíelo mediante **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Cree solo un tablero. Esto hace que el contenido sea más fácil de mantener y usted sabe exactamente lo que sus inversores están mirando.

Organice sus informes cuidadosamente y preste atención a los detalles. Una vez finalizado, el tablero tiene un aspecto similar al siguiente:

![](../../mbi/assets/investor-dboard-example.png)
