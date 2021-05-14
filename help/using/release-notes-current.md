---
title: Opmerkingen bij de release 2021.5.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.5.0
feature: Geen informatie
source-git-commit: b9adcc700edb7ba54a92037e86e86df812c93c83
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2021.5.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.5.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.5.0 is Mei 06, 2021.
De volgende release is gepland voor 3 juni 2021.

## Wat is er nieuw?{#whats-new}

* De PackageOverlaps kwaliteitsregel ontdekt nu gevallen waar het zelfde pakket veelvoudige tijden, d.w.z. in veelvoudige ingebedde plaatsen, in de zelfde opgestelde pakketreeks werd opgesteld.

* Het eindpunt van de repository in de Public API bevat nu de Git URL.

* In de workflow van het programma Bewerken mag de gebruiker alleen niet-decimale KPI-waarden instellen.

* Intermitterende fouten die werden aangetroffen tijdens het drukken van code naar Adobe Git zijn nu opgelost.

* De ervaring met het bewerkingsprogramma is vernieuwd.

## Opgeloste problemen {#bug-fixes}

* In plaats van &#39;verwijderde&#39; variabelen te verwijderen, markeert de API voor pijpleidingvariabelen deze alleen met de status &#39;DELETED&#39;.

* Sommige kwaliteitskwesties van het type Code Smell hadden een onjuiste invloed op de beoordeling Betrouwbaarheid.

* Wanneer een pijpleidingsuitvoering tussen middernacht en 1am UTC werd begonnen, werd de artefactversie die door de Manager van de Wolk werd geproduceerd niet gewaarborgd om groter te zijn dan een versie die de vorige dag werd gecreeerd.

* Bepaalde klanten van Adobe Managed Services (AMS) konden geen nieuwe projecten maken in de Adobe I/O Developer Console met de API voor Cloud Manager.
