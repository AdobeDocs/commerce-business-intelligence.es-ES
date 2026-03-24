---
title: Nueva arquitectura
description: Conozca las ventajas de pasar a una nueva arquitectura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# Nueva arquitectura

[!DNL Adobe Commerce Intelligence] equipos de productos e ingeniería se han enfocado en lograr las mejoras más amplias y solicitadas posibles durante el último año. Adobe está encantado de anunciar la disponibilidad de la nueva arquitectura de productos [!DNL Commerce Intelligence] que hará realidad estas mejoras.

## Ventajas de la nueva arquitectura

* Cree tipos de columnas en Data Warehouse, incluidas columnas calculadas con SQL.
* Las nuevas columnas están disponibles inmediatamente.
* La latencia de datos ha mejorado considerablemente.

## Ventajas técnicas

Las principales diferencias se enumeran anteriormente, pero el cambio principal es la forma en que se realizan los cálculos durante el ciclo de actualización. Los cálculos ya no se ejecutan en todas las columnas durante cada actualización; en su lugar, se ejecutan bajo demanda desde Visual Report Builder.

### Migración a la nueva arquitectura

Como las cuentas están fundamentalmente creadas de forma diferente, no hay ningún proceso automático para migrar los informes o Data Warehouse a una nueva cuenta de arquitectura. El paso a la nueva arquitectura requiere la reimplementación de la cuenta existente.

### Costo de traslado a la nueva arquitectura

¡Sin coste añadido! Adobe creará esta nueva cuenta para que inicie la reimplementación, que es gratuita durante al menos un mes. Esto le permite tener tiempo para tener ambas cuentas abiertas para que pueda realizar más fácilmente la reimplementación y garantizar que su equipo no tenga un hueco en el servicio.

### Tiempo necesario para volver a implementar la cuenta en la nueva arquitectura

Los tiempos de reimplementación varían según lo que desee reconstruir. Adobe recomienda realizar los siguientes pasos en la cuenta existente para hacerse una idea de lo que implicaría su reimplementación:

* Identifique un conjunto básico de informes/paneles.
* Identifique las métricas y dimensiones necesarias para crear esos informes.
* Identifique las columnas necesarias para volver a crear esas métricas y dimensiones.

Cuando se complete, sabrá qué datos necesita sincronizar con la nueva arquitectura de Data Warehouse para reconstruir esos informes principales.

### Obtención de ayuda

El [!DNL Adobe Commerce Intelligence] [equipo de servicios](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) puede realizar la reimplementación por un costo adicional. Póngase en contacto con su [equipo de cuenta de Adobe](../../guide-overview.md#Submitting-a-Support-Ticket) y asegúrese de proporcionar una lista de tableros o informes que desee priorizar en la creación de la nueva cuenta

### Permanecer con la arquitectura existente

Si estas funciones no son importantes para usted, puede mantener su cuenta existente. No hay costo adicional para mantener su cuenta existente. Adobe sigue admitiendo estas cuentas sin realizar cambios.
