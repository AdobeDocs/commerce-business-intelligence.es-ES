---
title: Conectar Google Analytics Almacenados
description: Obtenga información sobre cómo los visitantes utilizan el sitio, qué contenido es atractivo, dónde salen y mucho más.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en internet. Implementación [!DNL Google Analytics] en el sitio web le permite realizar un seguimiento de cómo utilizan el sitio los visitantes, qué contenido es atractivo, dónde abandonan el sitio los visitantes, etc. [!DNL Google Analytics Warehoused] es una integración independiente de la existente [!DNL Google Analytics] integración. Permite un mejor análisis debido a que tiene el [!DNL Google Analytics] datos en la Data Warehouse, que es diferente de la fuente activa del existente [!DNL Google Analytics] integración. Análisis de estas métricas en [!DNL Commerce Intelligence], junto con otros datos, mejora el estado general y la facilidad de uso del sitio.

## Diferencia entre GA Warehouse e integración en directo

El principal diferenciador es que se almacena una integración ([!DNL Google Analytics Warehoused]), y la otra no es ([!DNL Google Analytics Live]). En el caso de [!DNL Google Analytics Warehoused], esto permite manipular los [!DNL Google Analytics] y le ofrece la posibilidad de combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes reveladores.

Observe lo siguiente [!DNL Google Analytics] añada campañas para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que ha tenido varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, puede crear una columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto combinado permite [!DNL Google Analytics] datos que se van a unir a otros datos para llevar a cabo análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únete a él en contra `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una imagen completa de cuánto le está costando la participación.

Con el [!DNL Google Analytics Live] integración, por otro lado, cada [!DNL Google Analytics] El gráfico es como un pequeño silo que no se almacena en la Data Warehouse.

## Conectando [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] es un `Premium` Integración. [Atención al cliente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si tiene interés en añadir esta integración a su suscripción.

1. Vaya a la `Connections` página debajo de **[!UICONTROL Admin** > **Integrations]**.
1. Clic **[!UICONTROL Add an Integration]**, situado en el lado derecho.
1. Haga clic en [!DNL Google Analytics Warehoused] icono. Esto abre el [!DNL Google Analytics] página credenciales.
1. Introduzca su [!DNL Google Analytics] credenciales. Una vez completado el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].
1. Se muestra una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL Commerce Intelligence]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección Conexión múltiple [!DNL Google Analytics] perfiles de la sección siguiente.

## Conexión múltiple [!DNL Google Analytics] perfiles

Es posible que tenga varios sitios web conectados a un único [!DNL Google Analytics] cuenta, identificadas por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tiene la opción de incluir todos sus ID de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el de un sitio web en particular [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al sitio web de [!DNL Google Analytics] tablero
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen `p` al final de la línea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de cuenta](https://myaccount.google.com/intro) página.
1. En el `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Clic **[!UICONTROL revoke access]** junto a [!DNL Commerce Intelligence].

## Documentación relacionada

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de clientes](../../analysis/web-act-cust-conversion.md)
* [Seguimiento de datos de adquisición de usuarios mediante [!DNL Google Analytics] galletas](../../analysis/google-track-user-acq.md)
