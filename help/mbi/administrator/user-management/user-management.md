---
title: Administración de usuarios y permisos de Adobe Commerce
description: Obtenga información sobre cómo administrar los usuarios de Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
TQID: https://experienceleague.adobe.com/T3ZdoQW35n6CAJmDlOlfDVSI1eUA--e4RKZbOMF1BWY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 0%

---

# Administrar permisos de usuario

[!DNL Adobe Commerce Intelligence] pretende ser una única fuente fiable en toda la organización. Cada usuario tiene su propio conjunto de paneles que [puede compartir con otros usuarios](../../data-user/dashboards/share-dashboard-with-users.md).

## Niveles de permisos de usuario

En [!DNL Commerce Intelligence], hay tres niveles de permisos generales que se aplican a los usuarios y que se seleccionan cuando se crea una cuenta:

* `Admin`
* `Standard`
* `Read-Only`

Estos permisos permiten a los usuarios realizar determinadas acciones o acceder a partes específicas de [!DNL Commerce Intelligence]. Esta es una tabla de lo que puede hacer cada nivel de permiso en [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Crear/administrar usuarios** | ✔ |   |   |
| **Crear resúmenes de correo electrónico** | ✔ | ✔ |   |
| **Crear/editar/compartir tableros** | ✔ | ✔ |   |
| **Ver paneles** | ✔ | ✔ | ✔ |
| **Crear/editar/eliminar informes visuales** | ✔ | ✔* |   |
| **Crear/editar/eliminar informes SQL** | ✔ |  |   |
| **Clonar tableros** | ✔ |   |   |
| **Agregar/administrar integraciones** | ✔ |   |   |
| **Acceder al Administrador de Data Warehouse** | ✔ |   |   |
| **Sincronizar/no sincronizar tablas y columnas** | ✔ |   |   |
| **Crear/editar métricas** | ✔ |   |   |
| **Crear/editar conjuntos de filtros** | ✔ |   |   |
| **Crear/editar columnas calculadas** | ✔ |   |   |
| **Crear lista de informes dependientes** | ✔ |   |   |
| **Resumen del sistema de acceso** | ✔ |   |   |
| **Acceder a la configuración de zona horaria** | ✔ |   |   |
| **Facturación de acceso** | ✔ | ✔** |   |
| **Póngase en contacto con el servicio de asistencia** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_Puede limitar el acceso de **[!UICONTROL Standard]**&#x200B;un usuario de [&#x200B; a métricas específicas](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _los usuarios pueden acceder a Facturación con una configuración de permiso adicional._
>
>Los usuarios de **[!UICONTROL Read-Only]** solo pueden _ver_ paneles que se hayan compartido con ellos; no pueden crear ni editar nada en [!DNL Commerce Intelligence], ni pueden buscar y agregar nuevos paneles a su cuenta. Adobe recomienda compartir un conjunto específico de paneles con **[!UICONTROL Read-Only]** usuarios que usted u otro miembro de su equipo mantiene. No clone un conjunto de paneles para ellos.

## Permisos adicionales: Facturación y asistencia técnica {#billingtech}

Además de los niveles generales de permisos, existen otras dos designaciones de usuarios: `Billing` y `Technical`. Estas designaciones deben utilizarse con los niveles generales de permisos.

### Factura

`Billing` usuarios tienen acceso a la página de facturación y pueden cambiar la información de pago. Además, Adobe también puede ponerse en contacto con ellos si tienen preguntas sobre facturación.

Los usuarios de `Admin` tienen acceso a la ficha `Billing` de manera predeterminada, pero los usuarios de `Standard` también pueden obtener acceso si tienen seleccionada la casilla de verificación `Billing` en su perfil.

![Página de facturación](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnico

`Technical` usuarios no tienen permisos específicos para ellos. Esta configuración solo marca un contacto técnico dentro de su organización. Adobe puede ponerse en contacto con estos usuarios si tienen preguntas técnicas.

Los usuarios de `Admin` pueden agregar nuevos usuarios a su cuenta al hacer clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** y seguir las indicaciones. Una vez creado el usuario en [!DNL Commerce Intelligence], la persona afortunada a la que está invitando recibirá instrucciones por correo electrónico sobre cómo completar el proceso de configuración de la cuenta.

En cualquier momento, `Admins` puede ver todos los usuarios de su cuenta al hacer clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página muestra los permisos del usuario y a qué métricas y paneles pueden acceder.
