---
title: Opmerkingen bij de release 2020.3.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2020.3.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2020.3.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2020.3.0
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 1%

---

# Opmerkingen bij de release voor 2020.3.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2020.3.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2020.3.0 is Maart 05, 2020.

## Wat is er nieuw?{#whats-new}

* Het logboek voor de bouwstijlstap is nu beschikbaar terwijl de bouwstijlstap loopt.
* Sommige berichten op de pagina van de details van de pijpleidingsuitvoering zijn uitgegeven voor duidelijkheid.

## Opgeloste problemen {#bug-fixes}

* Bepaalde plaatsingsconfiguraties konden logboeken voor opstellen stappen veroorzaken om niet beschikbaar te zijn als de plaatsing ontbrak.
* Specifieke fouten in de implementatiestappen voor Managed Services-programma&#39;s kunnen ertoe leiden dat latere executies niet beginnen.
* De voorlopige SonarQube-instantie die in de bouwstap wordt gebruikt, kon soms niet binnen de geconfigureerde time-out worden gestart.
* In specifieke projecten, zouden de *voorwerpen ResourceResolver altijd moeten worden gesloten* een Uitzondering van de Wijzerplaat van de Null veroorzaken; dit had echter geen invloed op de uitvoering van de pijpleiding .