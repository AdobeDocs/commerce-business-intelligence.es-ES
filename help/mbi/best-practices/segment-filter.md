---
title: Dimension de datos recomendados para la segmentación y el filtrado
description: Conozca las prácticas recomendadas para la segmentación y el filtrado.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Segmentación y filtrado

Una buena segmentación es lo que convierte una estadística superficial en una métrica empresarial que impulsa las decisiones.

¿Quiere saber quiénes son sus clientes más valiosos? ¿Cuáles son sus canales de marketing más valiosos? ¿Cuáles de sus productos se mueven más rápido y por qué? Para llegar a cualquiera de estas respuestas, debe empezar por segmentar los datos.

Este artículo cubre los segmentos esenciales que a menudo se recomiendan a los clientes. También detalla qué preguntas pueden ayudarle estos segmentos a dar respuesta. Técnicamente, los segmentos son columnas de datos de la base de datos. Entrada [!DNL MBI], se denominan dimensiones.

![](../../mbi/assets/mbi-critical-segments.png)


## Segmentos de usuario

Los segmentos de usuario le ayudan a comprender quiénes son sus usuarios y cómo se comportan.

* **Edad/Año de nacimiento**: ¿Cuántos años tienen sus usuarios? ¿Cuántos años tienen sus usuarios más activos? Normalmente tiene sentido agrupar los valores en rangos para lograr un análisis más eficaz.
* **Sexo**: ¿Los distintos géneros se relacionan de forma diferente con su sitio web?
* **Dirección**: ¿De dónde provienen los usuarios? ¿Debería enfocar sus esfuerzos de marketing a una región en particular? ¿Sus campañas publicitarias recientes han tenido el rendimiento esperado en sus regiones de destino?
* **Fuente de adquisición del cliente**\: ¿Sabe de qué canal de marketing provienen sus usuarios? ¿Hicieron clic en un anuncio o lo encontraron mediante una búsqueda? [Segmentación de datos por fuente de adquisición de usuario](../data-analyst/analysis/google-track-user-acq.md) es el primer paso para optimizar la nueva adquisición de clientes. El segundo paso es gastar más dinero en lo que funciona y matar lo que no funciona.
* **Dispositivo de registro**: ¿Se han registrado los usuarios a través de su aplicación móvil o de su sitio web? ¿iOS o Android™? ¿Su base de usuarios móviles es lo suficientemente grande como para asignar más recursos al desarrollo de su producto móvil? (Si aún no está realizando el seguimiento, consulte este tema [acerca del seguimiento del dispositivo de usuario](../data-analyst/analysis/track-usr-dev-browser.md).
* **Remitido por**: ¿Quiénes son sus principales influencers? ¿Cuántos usuarios fueron referidos directamente por otros?
* **Industria**: Si es un negocio B2B, ¿en qué industrias trabajan sus usuarios? ¿A qué organizaciones comerciales vale la pena unirse?
* **Respuestas de encuesta**: si realiza encuestas a clientes, utilice las respuestas como segmentos para obtener un nivel de creación de perfiles más profundo. Puede hacer preguntas que complementen lo que ya sabe sobre sus usuarios o confirmar sus conjeturas.
* **Cantidad de primer pedido y categoría del producto**: ¿Existe una correlación entre el primer pedido de un usuario y los patrones de compra futuros?

## Segmentos de pedidos/eventos

Los segmentos de pedidos y eventos ayudan a analizar el comportamiento y la participación del usuario a lo largo del tiempo.

* **[!UICONTROL Billing / Shipping Address]**: ¿De dónde provienen la mayoría de sus pedidos? ¿Hay alguna diferencia entre las direcciones de facturación y envío?
* **[!UICONTROL Status]**: ¿Cuántos de sus pedidos no se han completado? ¿Cuál es la proporción de pedidos pendientes en los últimos siete días?
* **[!UICONTROL Customer acquisition source]**: Más allá del seguimiento de los datos de adquisición de usuarios a nivel de usuario, también puede [realizar el seguimiento en un nivel de pedido o evento](../data-analyst/analysis/google-track-user-acq.md). Un usuario que se haya registrado a través de una fuente puede seguir accediendo a su sitio a través de otras fuentes.
* **[!UICONTROL Device]**: ¿Está aumentando el número de pedidos móviles? ¿Cuántos de sus ingresos se generan mediante compras móviles? (Si aún no está realizando el seguimiento, consulte este tema [acerca del seguimiento de datos de dispositivos de pedidos](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: ¿Cuál de sus centros de cumplimiento genera la mayor cantidad de ingresos? Si está analizando la diferencia entre la hora de pedido y la hora de envío, ¿qué centro de cumplimiento es el más receptivo?
* **[!UICONTROL Delivery Carrier]**: ¿Cuál es el transportista más popular? ¿Qué transportista tiene el menor número de artículos devueltos?
* **[!UICONTROL Discount / Coupon Codes]**: ¿Sus promociones están generando un negocio adicional? ¿Cuántos artículos adicionales compraron sus clientes además del artículo en venta? ¿Cómo afectan los cupones al valor promedio de los pedidos? ¿Cuál es su margen promedio de artículos con descuento frente a los sin descuento?
* **[!UICONTROL Satisfaction / Rating]**: ¿Cuán satisfechos están sus clientes con sus pedidos? ¿Es probable que sus clientes le recomienden negocios?

## Segmentos de producto

Los segmentos de producto le ayudan a tomar decisiones de comercialización.

* **[!UICONTROL Merchant / Brand]**: ¿Una marca específica se vende más rápido que el resto? ¿Qué marcas tienen un bajo rendimiento?
* **[!UICONTROL Type / Category]**: ¿Los distintos segmentos de usuario disfrutan de diferentes tipos de productos? ¿Qué categorías de productos generan la mayor cantidad de repeticiones comerciales?
* **[!UICONTROL Discount / Coupon Codes]**: ¿Las promociones perjudican las ventas de productos sin descuento? ¿Cómo afectan los cupones al valor percibido de sus productos?
* **[!UICONTROL Social Activity]**: ¿Existe una correlación entre el zumbido generado en las redes sociales y la cantidad vendida por un producto?
* **[!UICONTROL Size / Variant]**: ¿Cuál es la proporción de inventario que necesita de cada variante? ¿Qué variantes se pueden vender con descuentos?

Si está interesado en la comercialización, consulte [cómo usar segmentos de producto para impulsar la repetición del negocio](../data-analyst/analysis/most-value-source-channel.md).

## Establecimiento de perfiles de cliente

Es posible que los expertos en segmentación deseen ir más allá de las divisiones unidimensionales y comenzar a establecer perfiles de clientes reales. Por ejemplo, las personas de entre 13 y 24 años que se registraron a través de un dispositivo móvil pusieron en un grupo &quot;Young &amp; Mobile&quot;. ¿En qué se diferencia el comportamiento de este grupo del resto de su base de usuarios?

Este tipo de análisis es lo que los especialistas en marketing de las empresas Fortune 1000 hacen todo el día. Antes de la llegada de las plataformas de inteligencia empresarial basadas en la nube como [!DNL MBI]Sin embargo, estaba en gran medida fuera de nuestro alcance para el resto de nosotros. Afortunadamente, ya no es así.

## Seguimiento de nuevos segmentos

El primer paso para segmentar las métricas por las dimensiones anteriores es asegurarse de que está realizando un seguimiento de estos datos en la base de datos. Si no se rastrea, reúna con su equipo técnico y encuentre una manera de empezar a rastrear estos datos.

Después de confirmar que el seguimiento de los datos se realiza en la base de datos, [póngase en contacto con el equipo de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para insertar las dimensiones en el [!DNL MBI] métricas y gráficos. También puede utilizar la variable *Administración de campos* herramienta para realizar un seguimiento de estos campos en [!DNL MBI].

## Relacionado

* [Optimización de la base de datos para el análisis](../best-practices/opt-db-analysis.md)
