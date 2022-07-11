---
title: Belangrijke concepten
description: Net als alle andere krachtige functies omvat Cloud Manager veel concepten en termen. Dit document geeft een overzicht van een aantal van de belangrijkste voor u bij het werken met Cloud Manager.
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 73e322cf93dc7709b7581860974079c8d94034ba
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---


# Belangrijke concepten {#key-concepts}

Net als alle andere krachtige functies omvat Cloud Manager veel concepten en termen. Dit document geeft een overzicht van een aantal van de belangrijkste voor u bij het werken met Cloud Manager.

## Toepassing {#application}

En de toepassing is de reeks aanpassingen en configuraties die door een klant worden gecreeerd om het onderliggende aan te passen [oplossing](#solution) (zoals AEM Sites of AEM Assets) voor hun specifieke gebruiksgevallen en behoeften. Een toepassing is een logische eenheid die kan bestaan uit meerdere [artefacten.](#artifact)

Een voorbeeldtoepassing is fictief [WKND-toepassing voor levensstijl.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

## Artefact {#artifact}

Een artefact is een plaatsbare eenheid en is het resultaat van wat bouwstijlproces dat broncode in één enkele eenheid omzet. Bijvoorbeeld een ZIP-bestand met de broncode.

## Artefactopslagplaats {#artifact-repository}

Een artefactopslagplaats is een opslagplaats waar klant-specifiek [artefacten](#artifact) worden opgeslagen en beveiligd.

## Omgeving {#environment}

Een omgeving is één cluster virtuele machines binnen een [programma.](#program) AEM bestaat deze uit een ontwerpinstantie (optioneel met een extra koude stand-by ontwerpinstantie), nul of meer publicatieinstanties, een of meer dispatcherinstanties en een taakverdelingsmechanisme.

## git Repository {#git-repository}

Een git-opslagplaats is een locatie waar klantspecifieke broncode wordt opgeslagen en toegankelijk is [git gebruiken.](https://git-scm.com)

## Instantie {#instance}

Een instantie is een specifieke virtuele server waarop de AEM wordt uitgevoerd [oplossing.](#solution) De instanties vertegenwoordigen één enkele logische eenheid vanuit een plaatsingsperspectief.

## Organisatie {#organization}

Een organisatie is een constructie van de Adobe die een ondernemingsklant vertegenwoordigt. Eén bedrijf kan meerdere organisaties hebben, afhankelijk van de manier waarop deze in het Adobe Identity Management System (IMS) zijn ingericht.

## Pijpleiding {#pipeline}

Een pijpleiding is een reeks plaatsingsstappen die in opeenvolging worden uitgevoerd.

## Product {#product}

Een product is een specifieke set functies binnen een [oplossing](#solution) in licentie gegeven door een organisatie. Verschil [programma&#39;s](#program) binnen een organisatie kan recht hebben op verschillende sets producten, bijvoorbeeld AEM Sites, AEM Assets of AEM Forms.

## Programma {#program}

Een programma is een reeks milieu&#39;s die een logische groepering van klanteninitiatieven steunen, gewoonlijk die aan een gekochte overeenkomsten van het de dienstniveau (SLA) beantwoorden. Elk programma heeft precies één productieomgeving en kan vele niet-productieomgevingen hebben.

## Oplossing {#solution}

Een oplossing is een van de Adobe [!UICONTROL Experience Cloud] oplossingen. Bijvoorbeeld Adobe Experience Manager, Adobe Target of Adobe Analytics.

## Stap {#step}

Een stap is een gevormde instructieset die één of andere eenheid van het werk als bouwsteen van een [pijpleiding.](#pipeline)
