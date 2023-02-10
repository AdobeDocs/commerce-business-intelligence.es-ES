---
title: Conectar Google Analytics Almacén
description: Aprenda a rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, dónde abandonan los visitantes, etc.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en Internet. Implementación [!DNL Google Analytics] en el sitio web permite rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, dónde abandonan los visitantes, etc. [!DNL Google Analytics Warehoused] es una integración independiente de nuestra [!DNL Google Analytics] integración. Permitirá un mejor análisis debido a que el [!DNL Google Analytics] los datos de su Data Warehouse, que son diferentes de la fuente en directo de la fuente existente [!DNL Google Analytics] integración. Analizar estas métricas en [!DNL MBI], junto con otros datos, mejorará el estado general y la capacidad de uso de su sitio.

## Diferencia entre GA Warehouse y la integración activa

El diferenciador principal es que se almacena una integración ([!DNL Google Analytics Warehoused]) y el otro no es ([!DNL Google Analytics Live]). En el caso de [!DNL Google Analytics Warehoused], esto permite la manipulación de su [!DNL Google Analytics] y le permite combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes descriptivos.

Veamos [!DNL Google Analytics] campañas publicitarias para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que tenía varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, podemos crear una nueva columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de la iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto de la combinación permite [!DNL Google Analytics] datos que se van a unir a otros datos para realizar análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únela a `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una imagen completa de la cantidad de compromiso que le está costando.

Con la variable [!DNL Google Analytics Live] integración, por otro lado, cada [!DNL Google Analytics] es como un pequeño silo que no está almacenado en su [!DNL MBI] almacén de datos.

## Conexión [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] es `Premium` Integración. [Contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) si tiene interés en añadir esta integración a su suscripción.

1. Vaya a la `Connections` página debajo de **[!UICONTROL Admin** > **Integrations]**.
1. Haga clic en **[!UICONTROL Add a Add Integration]**, situado en el lado derecho de la pantalla.
1. Haga clic en el [!DNL Google Analytics Warehoused] icono. Se abrirá la variable [!DNL Google Analytics] credenciales .
1. Escriba la [!DNL Google Analytics] credenciales. Una vez completado el proceso de autorización, se le redirigirá de nuevo a [!DNL MBI].
1. Se mostrará una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL MBI]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte [!DNL Google Analytics] a continuación.

## Conexión múltiple [!DNL Google Analytics] perfiles

Es posible que tenga varios sitios web conectados a una sola [!DNL Google Analytics] cuenta, identificada por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tendrá la opción de incluir todos sus ID de perfil en [!DNL MBI]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión [!DNL Google Analytics]
1. Vaya al sitio web en particular [!DNL Google Analytics] tablero
1. Busque la dirección URL: el ID de perfil corresponde a los 8 números siguientes `p` al final de la línea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconexión [!DNL Google Analytics Warehoused] from [!DNL MBI] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de la cuenta](https://www.google.com/accounts/) página.
1. En el `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL MBI].

## Documentación relacionada

* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Conexión [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de los clientes](../../analysis/web-act-cust-conversion.md)
* [Seguimiento de datos de adquisición de usuarios mediante [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
