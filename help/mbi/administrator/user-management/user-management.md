---
title: Administración de usuarios y permisos de Adobe Commerce
description: Obtenga información sobre cómo administrar los usuarios de Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Administrar permisos de usuario

[!DNL Adobe Commerce Intelligence] está diseñado para ser una única fuente fiable en toda la organización. Cada usuario tiene su propio conjunto de paneles, que puede [compartir con otros usuarios](../../data-user/dashboards/share-dashboard-with-users.md).

## Niveles de permisos de usuario

Entrada [!DNL Commerce Intelligence]Sin embargo, hay tres niveles de permisos generales que se aplican a los usuarios y que se seleccionan cuando se crea una cuenta:

* `Admin`
* `Standard`
* `Read-Only`

Estos permisos permiten a los usuarios realizar determinadas acciones o acceder a partes específicas de [!DNL Commerce Intelligence]. A continuación se muestra una tabla de lo que puede hacer cada nivel de permiso en [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Crear/administrar usuarios** | ✔ |   |   |
| **Crear resúmenes de correo electrónico** | ✔ | ✔ |   |
| **Crear/editar/compartir tableros** | ✔ | ✔ |   |
| **Ver paneles** | ✔ | ✔ | ✔ |
| **Crear/editar/eliminar informes visuales** | ✔ | ✔* |   |
| **Crear/editar/eliminar informes SQL** | ✔ |  |   |
| **Clonar paneles** | ✔ |   |   |
| **Agregar o administrar integraciones** | ✔ |   |   |
| **Acceso al Administrador de Datas Warehouse** | ✔ |   |   |
| **Sincronizar/dessincronizar tablas y columnas** | ✔ |   |   |
| **Crear/editar métricas** | ✔ |   |   |
| **Creación/edición de conjuntos de filtros** | ✔ |   |   |
| **Crear/editar columnas calculadas** | ✔ |   |   |
| **Creación de una lista de informes dependientes** | ✔ |   |   |
| **Resumen del sistema de acceso** | ✔ |   |   |
| **Acceder a configuración de zona horaria** | ✔ |   |   |
| **Facturación de acceso** | ✔ | ✔** |   |
| **Atención al cliente** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_Puede limitar un **[!UICONTROL Standard]**del usuario [acceso a métricas específicas](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _Los usuarios de pueden acceder a Facturación con una configuración de permisos adicional._
>
>**[!UICONTROL Read-Only]** los usuarios solo pueden _vista_ paneles que se han compartido con ellos; no pueden crear ni editar nada en [!DNL Commerce Intelligence], ni pueden buscar y agregar nuevos tableros a su cuenta. El Adobe recomienda compartir un conjunto específico de paneles con **[!UICONTROL Read-Only]** usuarios que usted u otro miembro de su equipo mantiene. No clone un conjunto de paneles para ellos.

## Permisos adicionales: Facturación y asistencia técnica {#billingtech}

Además de los niveles de permisos generales, existen otras dos designaciones de usuario: `Billing` y `Technical`. Estas designaciones deben utilizarse con los niveles generales de permisos.

### Factura

`Billing` los usuarios tienen acceso a la página de facturación y pueden cambiar la información de pago. Además, también pueden ser contactados por Adobe para preguntas de facturación.

`Admin` Los usuarios de tienen acceso a `Billing` pestaña de forma predeterminada, pero `Standard` los usuarios también pueden obtener acceso si tienen el `Billing` casilla seleccionada en su perfil.

![facturación](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnico

`Technical` los usuarios no tienen ningún permiso específico para ellos: esta configuración solo marca un contacto técnico dentro de su organización. El Adobe puede ponerse en contacto con estos usuarios si tienen preguntas técnicas.

`Admin` los usuarios pueden agregar nuevos usuarios a su cuenta haciendo clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** y siguiendo las indicaciones. Una vez creado el usuario en [!DNL Commerce Intelligence], la persona afortunada a la que invita recibirá instrucciones por correo electrónico sobre cómo completar el proceso de configuración de la cuenta.

En cualquier momento, `Admins` Puede ver todos los usuarios de su cuenta haciendo clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página muestra los permisos del usuario y a qué métricas y paneles pueden acceder.
