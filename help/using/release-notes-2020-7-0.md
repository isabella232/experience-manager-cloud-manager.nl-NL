---
title: Opmerkingen bij de release 2020.7.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2020.7.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2020.7.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2020.7.0
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 1%

---

# Opmerkingen bij de release voor 2020.7.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2020.7.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2020.7.0 is 09 Juli, 2020.

## Wat is er nieuw?{#whats-new}

* Het losmaken en koppelen van de instanties van de verzender van de ladingsbalansen tijdens productieplaatsingen werkt nu op een consistentere manier.

* De buildcontainer van Cloud Manager ondersteunt nu zowel Java 8 als Java 11.

* De pijpleidingen van de Manager van de wolk steunen nu klant-vastgestelde variabelen en geheimen.
Raadpleeg [Variabelen pijpleiding](/help/using/build-environment-details.md#pipeline-variables) voor meer informatie.

## Opgeloste problemen {#bug-fixes}

* De opties **Annuleren** en **Opslaan** op de pagina Bewerken niet-productiepijpleiding zijn niet altijd zichtbaar.

* Bepaalde fouten in het proces van de codekwaliteit kunnen ertoe leiden dat het logbestand niet correct wordt gegenereerd.

* Sommige logboeken van grote pijpleidingsstappen konden niet constant door het gebruikersinterface worden gedownload.

## Bekende problemen {#known-issues}

* Wanneer een milieu van AMS een reserve instantie bevat, verklaart het geregistreerde bericht dat de instantie neer in tegenstelling tot op standby wijze is.

* Als gevolg van een wijziging in de manier waarop de codedekking wordt berekend, is de _minimum_-versie van de Jacoco-plug-in nu 0.7.5.201505241946 (uitgebracht in mei 2015). Klanten die expliciet verwijzen naar een oudere versie ontvangen een foutbericht in het proces voor de kwaliteit van de code.
