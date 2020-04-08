---
title: Opmerkingen bij de release 2020.3.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2020.3.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2020.3.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2020.3.0
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# Opmerkingen bij de release 2020.3.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] versie 2020.3.0 beschreven.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2020.3.0 is 5 maart 2020.

## Nieuwe functies {#whats-new}

* Het logboek voor de bouwstijlstap is nu beschikbaar terwijl de bouwstijlstap loopt.
* Sommige berichten op de pagina van de details van de pijpleidingsuitvoering zijn uitgegeven voor duidelijkheid.

## Opgeloste problemen {#bug-fixes}

* Bepaalde plaatsingsconfiguraties konden logboeken voor opstellen stappen veroorzaken om niet beschikbaar te zijn als de plaatsing ontbrak.
* De specifieke mislukkingen binnen de plaatsingsstappen voor de Beheerde programma&#39;s van de Diensten konden verdere uitvoeringen veroorzaken om te ontbreken te beginnen.
* De voorlopige SonarQube-instantie die in de stap build werd gebruikt, kon niet zo nu en dan starten binnen de geconfigureerde time-out.
* In specifieke projecten, zouden de voorwerpen *ResourceResolver altijd moeten worden gesloten* een Null Uitzondering van de Aanwijzer veroorzaken; dit had echter geen invloed op de uitvoering van de pijpleiding .