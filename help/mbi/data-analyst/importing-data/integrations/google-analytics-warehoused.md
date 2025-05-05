---
title: Conectar Google Analytics Almacenados
description: Obtenga información sobre cómo los visitantes utilizan el sitio, qué contenido es atractivo, dónde salen y mucho más.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en Internet. La implementación de [!DNL Google Analytics] en el sitio web permite rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, de dónde salen los visitantes, etc. [!DNL Google Analytics Warehoused] es una integración independiente de su integración de [!DNL Google Analytics] existente. Permite un mejor análisis debido a que tiene los datos de [!DNL Google Analytics] en la Data Warehouse, que es diferente de la fuente activa de la integración de [!DNL Google Analytics] existente. El análisis de estas métricas en [!DNL Commerce Intelligence], junto con otros datos, mejora el estado general y la facilidad de uso del sitio.

## Diferencia entre GA Warehouse e integración en directo

El principal diferenciador es que una integración está almacenada ([!DNL Google Analytics Warehoused]) y la otra no ([!DNL Google Analytics Live]). En el caso de [!DNL Google Analytics Warehoused], esto permite manipular los datos de [!DNL Google Analytics] y permite combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes profundos.

Consulte [!DNL Google Analytics] campañas de publicidad para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que ha tenido varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, puede crear una columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto de combinación permite que los datos de [!DNL Google Analytics] se unan a otros datos para realizar análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únase a ellos con `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una idea completa de cuánto le está costando la participación.

Con la integración de [!DNL Google Analytics Live] por otro lado, cada gráfico de [!DNL Google Analytics] es como un pequeño silo que no se almacena en su Data Warehouse.

## Conectando [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] es una integración de `Premium`. [Póngase en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) si tiene interés en agregar esta integración a su suscripción.

1. Vaya a la página `Connections` en **[!UICONTROL Admin** > **Integrations]**.
1. Haga clic en **[!UICONTROL Add an Integration]**, ubicado en el lado derecho.
1. Haga clic en el icono [!DNL Google Analytics Warehoused]. Se abre la página de credenciales [!DNL Google Analytics].
1. Escriba sus credenciales de [!DNL Google Analytics]. Una vez completado el proceso de autorización, se le redirigirá a [!DNL Commerce Intelligence].
1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección Conexión de varios perfiles [!DNL Google Analytics] más abajo.

## Conectando varios perfiles [!DNL Google Analytics]

Es posible que tenga varios sitios web conectados a una sola cuenta de [!DNL Google Analytics], identificada por su propio identificador de perfil [!DNL Google Analytics]. En este caso, tiene la opción de incluir todos los identificadores de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el identificador de perfil [!DNL Google Analytics] de un sitio web en particular:

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al panel [!DNL Google Analytics] del sitio web en particular
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen a `p` al final de la línea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite la página [!DNL Google Analytics] [configuración de la cuenta](https://myaccount.google.com/intro).
1. En la sección `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL Commerce Intelligence].

## Documentación relacionada

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de clientes](../../analysis/web-act-cust-conversion.md)
* [Rastrear datos de adquisición de usuarios con  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
