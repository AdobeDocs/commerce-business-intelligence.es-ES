---
title: Creación de un tablero para inversores
description: Aprenda a crear un panel para inversores.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Generar panel de inversores

Muchos de nuestros clientes están trabajando con inversores y necesitan compartir información desde la plataforma con ellos, pero los tableros que usted crea para tomar decisiones comerciales diarias pueden no ser lo que un inversor está buscando. Aquí explicamos algunas prácticas recomendadas para crear un panel que sea completo pero simple, ideal para compartir con inversores activos y potenciales.

Esto es lo que debe crear informes para el panel del inversor:

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
   * Métrica: ingresos por primera vez en el pedido
   * Filtro: el número de orden del usuario es igual a 1
   * Métrica 2: ingresos de orden de repetición
      * Filtro: el número de pedido del usuario es bueno a 1
   * Desmarque la casilla de verificación de varios ejes Y
   * Cambio en un gráfico de columnas apiladas
* **[!UICONTROL AOV by quarter]**
   * Métrica 1 - Ingresos
      * Ocultar esta métrica
   * Métrica 2 - Número de pedidos
      * Ocultar esta métrica
   * Fórmula - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Métrica - Ingresos
   * Agrupar por cliente `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Métrica - Ingresos del producto
      * Ocultar el gráfico
      * Agrupar por nombre de producto. Seleccione todos los productos.
      * Establezca el intervalo de tiempo en Todo el tiempo
      * Establezca el intervalo de tiempo en Ninguno
      * En &quot;Mostrar arriba/abajo&quot;, mostrar solo los 10 primeros ordenados por beneficio del producto
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Métrica: compradores distintos
      * Perspectiva: acumulativa
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sesiones

Con un [!DNL Google Analytics] integración, puede incluir informes sobre:

* Visitas al sitio
* Tasa de conversión

Con la variable [Servicios de enriquecimiento de datos del comercio](https://business.adobe.com/products/magento/magento-commerce.html), puede incluir informes sobre:

* Clientes únicos por estado/región, edad, sexo.

## Otras sugerencias

* Utilice un [convención de nomenclatura](../best-practices/naming-elements.md)
* Compartir el panel con los usuarios inversores
* O envíelo a través de **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Crear solo un tablero. Esto hará que el contenido sea más fácil de mantener, y sabrá exactamente lo que sus inversores están viendo.

Organice los informes con cuidado y preste atención a los detalles. Una vez completado, el tablero tendrá un aspecto similar al siguiente:

![](../../mbi/assets/investor-dboard-example.png)
