---
title: Modelado de datos MongoDB
description: Aprenda a evitar patrones de datos que planteen un problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] Modelado de datos

Cuándo [!DNL MBI] extrae [!DNL MongoDB] datos, esos datos se traducen en un modelo relacional.

Las malas noticias: Aunque la mayoría de los patrones de datos no plantean un problema, hay algunos que, debido a la traducción a un modelo relacional, [!DNL MBI] no admite.

La buena noticia: todos estos patrones pueden evitarse.

## Matrices subanidadas {#subnested}

Si su colección tiene el aspecto del ejemplo siguiente, [!DNL MBI] solo replica los datos en la matriz de elementos. No se extraen datos de la matriz de subelementos.

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

Las colecciones que incluyen objetos con claves de objeto variables no se replican en [!DNL MBI]. Por ejemplo:

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
