---
title: Opmerkingen bij de release 2021.3.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2021.3.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.3.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2021.3.0
translation-type: tm+mt
source-git-commit: b5233e1932888b515d8dc26a6493cbd26686bc3c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2021.3.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.3.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.3.0 is 11 Maart, 2021.

## Wat is er nieuw?{#whats-new}

* Er is een nieuw hulpmiddel voor de kwaliteit van de code geïntroduceerd om de configuratie van de dispatcher van de klant te valideren (Hulpprogramma voor de optimalisatie van de verzender).

* Gebruikers kunnen nu hun rol(en) van de Cloud Manager zien door de optie **Rol(en) van de Cloud Manager weergeven** te selecteren na naar het pictogram Gebruikersprofiel (rechtsboven) van Unified Shell te navigeren.

* Het label **Goedkeuringsaanvraag** is voor meer duidelijkheid opnieuw gelabeld aan **Productiegoedkeuring**.

* Het **Version**-label is opnieuw gelabeld aan **Git Tag** in het uitvoeringsscherm van de productiepijplijn.

* De labels die het gedrag bepalen wanneer belangrijke metriek niet aan de bepaalde drempel voldoet, zijn geëtiketteerd om op hun ware gedrag te wijzen - onmiddellijk annuleren en Onmiddellijk goedkeuren.

* De lijsten van de klasse en van de methodevervanging zijn bijgewerkt gebaseerd op versie `2021.3.4997.20210303T022849Z-210225` van de AEM Cloud Service SDK.

## Opgeloste problemen {#bug-fixes}

* Bepaalde kwaliteitsproblemen zijn niet goed ontdekt wanneer pakketten in andere pakketten waren ingesloten.

* Wanneer de gebruiker bij gelegenheid vanaf de pagina voor de uitvoering van de pijpleiding navigeert onmiddellijk nadat een pijpleiding is gestart, wordt een foutbericht weergegeven met de mededeling dat de handeling is mislukt, hoewel de uitvoering daadwerkelijk wordt gestart.