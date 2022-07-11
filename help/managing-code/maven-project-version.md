---
title: Maven-projectversiebeheer
description: Leer hoe Maven het versioning van projecten in de Manager van de Wolk behandelt.
exl-id: a1d676e0-27cc-4b0d-8799-527c0520946a
source-git-commit: 9312999660b324f0f9d2b44dfbf49c4813a3a6e9
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---


# Maven-projectversiebeheer {#project-version}

Leer hoe Maven het versioning van projecten in de Manager van de Wolk behandelt.

## Hoe Maven projectversies afhandelt {#how-maven}

Voor implementatie van testfasen en productie genereert Cloud Manager een unieke, incrementele versie.

Deze versie wordt gezien op de pagina van de details van de pijpleidingsuitvoering evenals de activiteitenpagina. Wanneer een bouwstijl in werking wordt gesteld, wordt het Maven project bijgewerkt om deze versie te gebruiken en een markering wordt gecreeerd in de git bewaarplaats met die versie als zijn naam.

Als de oorspronkelijke projectversie aan bepaalde criteria voldoet, voegt de bijgewerkte versie van het Maven-project zowel de oorspronkelijke projectversie als de door Cloud Manager gegenereerde versie samen. De tag gebruikt echter altijd de gegenereerde versie. Deze samenvoeging vindt pas plaats als de oorspronkelijke projectversie is samengesteld met precies drie versiesegmenten, bijvoorbeeld `1.0.0` of `1.2.3`, maar niet `1.0` of `1`en mag de oorspronkelijke versie niet eindigen in `-SNAPSHOT`.

>[!NOTE]
>
>Deze oorspronkelijke versie van het project moet statisch worden ingesteld in het dialoogvenster `<version>` element van het hoogste niveau `pom.xml` bestand in de vertakking van de it-opslagplaats.

Als de originele versie aan deze criteria voldoet, zal de geproduceerde versie aan de originele versie als nieuw versiesegment worden toegevoegd. De gegenereerde versie wordt ook enigszins aangepast, zodat de versie correct wordt gesorteerd en verwerkt. Bijvoorbeeld, veronderstellend een geproduceerde versie van `2019.926.121356.0000020490`:

| Versie | Versie in `pom.xml` | Opmerking |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Oorspronkelijke versie met de juiste indeling |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | Opnameversie, overschreven |
| `1` | `2019.926.121356.0000020490` | Onvolledige versie, overschreven |

>[!NOTE]
>
>Ongeacht of de oorspronkelijke versie is opgenomen in de door Cloud Manager geïnitialiseerde versie, de oorspronkelijke versie is beschikbaar als een Maven-eigenschap met de naam `cloudManagerOriginalVersion`.
