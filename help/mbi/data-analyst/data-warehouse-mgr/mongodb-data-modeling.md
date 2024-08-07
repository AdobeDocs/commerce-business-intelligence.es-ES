---
title: Modelado de datos MongoDB
description: Aprenda a evitar patrones de datos que planteen un problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# Modelado de datos de [!DNL MongoDB]

Cuando [!DNL Adobe Commerce Intelligence] extrae [!DNL MongoDB] datos, estos se traducen en un modelo relacional.

Las malas noticias: aunque la mayoría de los patrones de datos no plantean ningún problema, hay algunos que no son compatibles con [!DNL Commerce Intelligence], debido a la traducción a un modelo relacional.

La buena noticia: todos estos patrones pueden evitarse.

## Matrices subanidadas {#subnested}

Si su colección se parece al ejemplo siguiente, [!DNL Commerce Intelligence] solo replica los datos en la matriz de elementos. No se extraen datos de la matriz de subelementos.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Claves de objeto variable {#varobjectkeys}

Las colecciones que incluyen objetos con claves de objeto variables no se replican en [!DNL Commerce Intelligence]. Por ejemplo:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Esto suele ocurrir cuando se está utilizando un objeto y sería más apropiado utilizar una matriz. Ahora, vuelva a trabajar en el ejemplo anterior:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
