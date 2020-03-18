---
title: Opmerkingen bij de release 2018.8.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2018.8.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2018.8.0.
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2018.8.0.
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b

---


# Opmerkingen bij de release 2018.8.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2018.8.0 voegt steun voor het teweegbrengen van de pijpleiding toe CI/CD automatisch op git begaat en een nieuwe tovenaar voor het creëren van toepassingsprojecten in git die op het Archieftype van het Project AEM wordt gebaseerd.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2018.8.0 is 4 oktober 2018.

## Nieuwe functies {#what-s-new}

* **De Opstelling** van het programma - Nieuwe tovenaar om een toepassingsproject in git tot stand te brengen gebruikend het Archieftype van het Project AEM gelieve te verwijzen naar [Create een Project](create-an-application-project.md) van de Toepassing AEM om meer te leren.

* **CI/CD Pipeline** - De volgende veranderingen worden toegevoegd aan CI/CD Pijpleiding. Gelieve te verwijzen naar [vorm uw CI/CD Pijpleiding](configuring-pipeline.md) om meer te leren.

   * Bij de Trekker van de Veranderingen van het Git, die de pijpleiding CI/CD begint wanneer er toezeggingen aan de gevormde git tak worden toegevoegd.
   * Kaarten op het huisscherm verbinden nu diep in specifieke secties van de pagina van de pijpleidingsuitvoering.
   * De pagina van de activiteit maakt nu een lijst van de specifieke tak die voor elke uitvoering wordt gebruikt.
   * De pagina Activiteit geeft nu de duur in uren en minuten aan.
   * De pagina voor het uitvoeren van de pijpleiding geeft nu de versie/tagnaam weer die voor de uitvoering is gemaakt.
   * Apache Maven-versie bijgewerkt naar 3.5.3.

* **Navigatie** - De volgende wijzigingen worden toegevoegd aan de [!UICONTROL Cloud Manager]code.

   * De verbinding van middelen in globale navigatie zal aan Runbook in Sharepoint navigeren.
   * Het menu Help is opnieuw ingedeeld en bevat meer [!UICONTROL Cloud Manager]specifieke inhoud.

## Opgeloste problemen {#bug-fixes}

* Bepaalde details in het dialoogvenster Prestaties testen zijn niet zichtbaar in Firefox.
* Time-outs tussen interne systemen zouden er soms toe leiden dat implementatiefouten worden gemeld.
* De pictogramkleur op de pagina Activiteit was niet correct voor sommige succesvolle pijpleidingsuitvoeringen.
* In sommige gevallen wordt in het dialoogvenster voor het testen van prestaties dezelfde meting meerdere malen weergegeven.
* Als een nieuwe instantie werd toegevoegd nadat de pijpleiding CI/CD was begonnen, zou de plaatsing niet op de pas gecreëerde instantie worden uitgevoerd.

## Bekende problemen {#known-issues}

* De takken die gebruikend de Tovenaar van het Project van de Toepassing worden gecreeerd kunnen geen streepjes bevatten.
* Meldingen worden mogelijk niet consistent geladen op de [!UICONTROL Experience Cloud] berichtzijbalk. Meldingen zijn echter wel zichtbaar in de map [!UICONTROL Experience Cloud] en worden, indien geconfigureerd, nog steeds verzonden via e-mail.

