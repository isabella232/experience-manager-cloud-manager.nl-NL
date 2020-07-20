---
title: Opmerkingen bij de release 2020.7.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2020.7.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2020.7.0
seo-description: Volg deze pagina om informatie op te halen voor de release 2020.7.0 van AEM Cloud Manager
translation-type: tm+mt
source-git-commit: 0d46abc386460ccbaf7ba10b93286bc8e4af2395
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Opmerkingen bij de release 2020.7.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] versie 2020.7.0 beschreven.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2020.7.0 is 9 juli 2020.

## What&#39;s New {#whats-new}

* Het losmaken en koppelen van de instanties van de verzender van de ladingsbalansen tijdens productieplaatsingen werkt nu op een consistentere manier.

* De buildcontainer van Cloud Manager ondersteunt nu zowel Java 8 als Java 11.

* De pijpleidingen van de Manager van de wolk steunen nu klant-vastgestelde variabelen en geheimen.
Raadpleeg [Pipetvariabelen](/help/using/create-an-application-project.md#pipeline-variables) voor meer informatie.

## Bug Fixes {#bug-fixes}

* De opties **Annuleren** en **Opslaan** op de pagina Bewerken zonder productiepijpleiding waren niet altijd zichtbaar.

* Bepaalde fouten in het proces van de codekwaliteit kunnen ertoe leiden dat het logbestand niet correct wordt gegenereerd.

* Sommige logboeken van grote pijpleidingsstappen konden niet constant door het gebruikersinterface worden gedownload.

## Bekende problemen {#known-issues}

* Wanneer een milieu van AMS een reserve instantie bevat, verklaart het geregistreerde bericht dat de instantie neer in tegenstelling tot op standby wijze is.

* Als gevolg van een wijziging in de manier waarop de codedekking wordt berekend, is de _minimale_ versie van de Jacoco-plug-in nu 0.7.5.201505241946 (uitgebracht in mei 2015). Klanten die expliciet verwijzen naar een oudere versie ontvangen een foutbericht in het proces voor de kwaliteit van de code.
