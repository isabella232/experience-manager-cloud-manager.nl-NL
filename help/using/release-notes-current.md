---
title: Opmerkingen bij de release 2021.3.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2021.3.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.3.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2021.3.0
translation-type: tm+mt
source-git-commit: fde8cbd22ff36e0d30409f68e8a0523c814ccf90
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2021.3.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.3.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.3.0 is 11 Maart, 2021.
De volgende release is gepland voor 8 april 2021.

## Wat is er nieuw?{#whats-new}

* Gebruikers met de vereiste machtigingen kunnen het programma nu bewerken, zodat zij het volgende op een zelfbedieningsmanier kunnen doen:

   * Voeg de oplossing van Plaatsen aan een bestaand programma met Activa (of vice versa) toe.
   * Sites (of Middelen) verwijderen uit een bestaand programma met zowel Sites als Middelen.
   * Het toevoegen (terug) van een oplossing kan aan het bestaande programma of als nieuw Programma worden gedaan.

* Er is een nieuw hulpmiddel [Dispatcher Optimization Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) geïntroduceerd om de configuratie van de klantdispatcher te valideren.

* Gebruikers kunnen nu hun rol(en) van de Cloud Manager zien door de optie **Rol(en) van de Cloud Manager weergeven** te selecteren na naar het pictogram Gebruikersprofiel (rechtsboven) van Unified Shell te navigeren.

* Het label **Goedkeuringsaanvraag** is voor meer duidelijkheid opnieuw gelabeld aan **Productiegoedkeuring**.

* Het **Version**-label is opnieuw gelabeld aan **Git Tag** in het uitvoeringsscherm van de productiepijplijn.

* De etiketten die het gedrag bepalen wanneer de belangrijke metriek niet de bepaalde drempel ontmoeten zijn opnieuw geëtiketteerd om op hun ware gedrag te wijzen - **annuleert onmiddellijk** en **goedkeuren Onmiddellijk**. Verwijs naar [Vormend de Montages van de Pijpleiding](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) voor meer details.

* De lijsten van de klasse en van de methodevervanging zijn bijgewerkt gebaseerd op versie `2021.3.4997.20210303T022849Z-210225` van de AEM Cloud Service SDK.

## Opgeloste problemen {#bug-fixes}

* Bepaalde kwaliteitsproblemen zijn niet goed ontdekt wanneer pakketten in andere pakketten waren ingesloten.

* Wanneer de gebruiker bij gelegenheid vanaf de pagina voor de uitvoering van de pijpleiding navigeert onmiddellijk nadat een pijpleiding is gestart, wordt een foutbericht weergegeven met de mededeling dat de handeling is mislukt, hoewel de uitvoering daadwerkelijk wordt gestart.