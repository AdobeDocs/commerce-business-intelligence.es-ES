---
title: Nueva arquitectura
description: Conozca las ventajas de pasar a una nueva arquitectura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nueva arquitectura

[!DNL Adobe Commerce Intelligence] equipos de productos e ingeniería se han enfocado en lograr las mejoras más amplias y solicitadas posibles durante el último año. A Adobe le complace anunciar la disponibilidad de la nueva arquitectura de productos [!DNL Commerce Intelligence] que hará realidad estas mejoras.

## Ventajas de la nueva arquitectura

* Cree tipos de columnas en la Data Warehouse, incluidas columnas calculadas con SQL.
* Las nuevas columnas están disponibles inmediatamente.
* La latencia de datos ha mejorado considerablemente.

## Ventajas técnicas

Las principales diferencias se enumeran anteriormente, pero el cambio principal es la forma en que se realizan los cálculos durante el ciclo de actualización. Los cálculos ya no se ejecutan en cada columna durante cada actualización; en su lugar, se ejecutan bajo demanda desde el Report Builder visual.

### Migración a la nueva arquitectura

Como las cuentas se crean de forma fundamentalmente diferente, no hay ningún proceso automático para migrar la Data Warehouse o los informes a una nueva cuenta de arquitectura. El paso a la nueva arquitectura requiere la reimplementación de la cuenta existente.

### Costo de traslado a la nueva arquitectura

¡Sin coste añadido! Adobe creará esta nueva cuenta para que inicie la reimplementación, que es gratuita durante al menos un mes. Esto le permite tener tiempo para tener ambas cuentas abiertas para que pueda realizar más fácilmente la reimplementación y garantizar que su equipo no tenga un hueco en el servicio.

### Tiempo necesario para volver a implementar la cuenta en la nueva arquitectura

Los tiempos de reimplementación varían según lo que desee reconstruir. Adobe recomienda realizar los siguientes pasos en la cuenta existente para hacerse una idea de lo que implicaría su reimplementación:

* Identifique un conjunto básico de informes/paneles.
* Identifique las métricas y dimensiones necesarias para crear esos informes.
* Identifique las columnas necesarias para volver a crear esas métricas y dimensiones.

Cuando se complete, sabrá qué datos necesita sincronizar con la nueva Data Warehouse de arquitectura para reconstruir esos informes principales.

### Obtención de ayuda

El [!DNL Adobe Commerce Intelligence] [equipo de servicios](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) puede realizar la reimplementación por un costo adicional. Póngase en contacto con su [equipo de cuenta de Adobe](../../guide-overview.md#Submitting-a-Support-Ticket) y asegúrese de proporcionar una lista de tableros o informes que desee priorizar al crear en la nueva cuenta

### Permanecer con la arquitectura existente

Si estas funciones no son importantes para usted, puede mantener su cuenta existente. No hay costo adicional para mantener su cuenta existente. El Adobe sigue admitiendo esas cuentas sin realizar cambios.
