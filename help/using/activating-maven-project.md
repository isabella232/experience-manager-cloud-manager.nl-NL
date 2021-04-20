---
title: Maven-projectversiebeheer
seo-title: Maven-projectversiebeheer
description: Meer informatie over Maven Project Version Handling.
seo-description: Volg deze pagina voor meer informatie over Maven Project Version Handling.
feature: Getting Started
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---


# Maven-projectversiebeheer {#project-version}

## Werken met beheerde projectversiebeheer {#understanding-project-version}

Voor stage- en productieimplementaties genereert Cloud Manager een unieke, incrementele versie.

Deze versie wordt gezien op de pagina van de details van de pijpleidingsuitvoering evenals de activiteitenpagina. Wanneer een bouwstijl in werking wordt gesteld, wordt het Maven project bijgewerkt om deze versie te gebruiken en een markering wordt gecreeerd in de git bewaarplaats met die versie als zijn naam.

Als de oorspronkelijke projectversie aan bepaalde criteria voldoet, voegt de bijgewerkte versie van het Maven-project zowel de oorspronkelijke projectversie als de door Cloud Manager gegenereerde versie samen. De tag gebruikt echter altijd de gegenereerde versie. Opdat deze samenvoeging plaatsvindt, moet de oorspronkelijke projectversie worden gevormd met precies drie versiesegmenten, bijvoorbeeld, 1.0.0 of 1.2.3, maar niet 1.0 of 1, en de originele versie moet niet in - SNAPSHOT eindigen.

Als de oorspronkelijke versie wel aan deze criteria voldoet, wordt de gegenereerde versie als een nieuw versiesegment toegevoegd aan de oorspronkelijke versie. De gegenereerde versie wordt ook enigszins aangepast, zodat de versie correct wordt gesorteerd en verwerkt. Bijvoorbeeld, uitgaande van een gegenereerde versie van 2019.926.121356.000020490:

| **Versie** | **versie in pom.xml** | **Opmerking** |
|---|---|---|
| 1.0.0. | 1.0.0.2019_0926_121356_000020490 | Oorspronkelijke versie met de juiste indeling |
| 1.0.0-MOMENTOPNAME | 2019 926 121356 0000020490 | Opnameversie, overschreven |
| 1 | 2019 926 121356 0000020490 | Onvolledige versie, overschreven |

>[!NOTE]
>
>Ongeacht of de oorspronkelijke versie al dan niet is opgenomen in de door Cloud Manager geïnitialiseerde versie, is de oorspronkelijke versie beschikbaar als een Maven-eigenschap met de naam *cloudManagerOriginalVersion.*
