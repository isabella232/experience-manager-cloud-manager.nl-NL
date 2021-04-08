---
title: Opmerkingen bij de release 2021.4.0
description: Volg deze pagina om informatie op te halen voor Cloud Manager Release 2021.4.0
feature: Geen informatie
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
translation-type: tm+mt
source-git-commit: 1f7f87a4b944d1fadc708958a96a1bda7d41da5d
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 1%

---

# Opmerkingen bij de release voor 2021.4.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.4.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.4.0 is April 08, 2021.
De volgende release is gepland voor 6 mei 2021.

## Wat is er nieuw?{#whats-new}

* De time-out van de aanvraag voor de prestatietest voor virtuele gebruikers is verhoogd van 20 seconden naar 60 seconden.

* De Manage knoop van de it wordt getoond op de kaart van Pijpleidingen zelfs wanneer geen pijpleidingen zijn gevormd.

* Tijdens de plaatsingsstap van de de uitvoeringspagina van de Pijpleiding zal de gebruiker de voltooide en toekomstige plaatsingsstappen naast huidige stap in UI voor *Bezig* staat kunnen zien.

* De versie van het AEM projectarchetype dat door de Manager van de Wolk wordt gebruikt is bijgewerkt aan versie 27.

* Het foutbericht bij het starten van een pijpleiding wanneer een omgeving werd verwijderd, is verduidelijkt.

* OSGi-bundels die door Eclipse-projecten worden geleverd, zijn nu uitgesloten van regel `CQBP-84--dependencies`.

## Opgeloste problemen {#bug-fixes}

* Zeldzame, voorbijgaande fouten die bij *Activa Test* stap in de productiepijplijn kunnen voorkomen.

* Een slash in de productiecijplijn Load Test veroorzaakte een fout van 404.

* De `Runmode` controle produceerde valse positieven op niet omslagknopen.