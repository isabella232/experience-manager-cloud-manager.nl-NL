---
title: Uw code implementeren
seo-title: Uw code implementeren
description: 'null'
seo-description: Zodra u uw pijpleiding (bewaarplaats, milieu, en het testen milieu) hebt gevormd, bent u bereid om uw code op te stellen. Volg deze pagina voor meer informatie.
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
translation-type: tm+mt
source-git-commit: d38b6da61c552a3e9ad03dac49a64553f0cb00b4
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Uw code implementeren {#deploy-your-code}

## Code implementeren met Cloud Manager {#deploying-code-with-cloud-manager}

Nadat u de productiepijpleiding hebt geconfigureerd (opslagruimte, omgeving en testomgeving), kunt u uw code implementeren.

1. Klik op **Implementeren** in Cloud Manager om het implementatieproces te starten.

   ![](assets/Deploy1.png)

1. Het **scherm van de Uitvoering** van de Pijpleiding toont.

   Klik op **Genereren** om het proces te starten.

   ![](assets/Deploy2.png)

1. Het volledige bouwstijlproces stelt uw code op.

   De volgende fasen zijn betrokken bij het bouwproces:

   1. Werkgebiedimplementatie
   1. Werkgebiedtests
   1. Implementatie van productie

   >[!NOTE]
   >
   >Bovendien, kunt u de stappen van diverse plaatsingsprocessen herzien door logboeken, of het herzien van resultaten, voor de testende criteria te bekijken.

   De **Fase-implementatie** omvat de volgende stappen:

   * Validatie: Deze stap zorgt ervoor dat de pijpleiding wordt gevormd om de momenteel beschikbare middelen te gebruiken, bijvoorbeeld, dat de gevormde tak bestaat, zijn de milieu&#39;s beschikbaar.
   * Testen van build en eenheid: Deze stap stelt een containerized bouwstijlproces in werking. Zie [Creeer een Project](create-an-application-project.md) van de Toepassing van de AEM voor details op het bouwstijlmilieu.
   * Codescannen: Deze stap evalueert de kwaliteit van uw toepassingscode. Zie [De testresultaten](understand-your-test-results.md) begrijpen voor meer informatie over het testproces.
   * Distribueren naar werkgebied

   ![](assets/Stage_Deployment1.png)

   The **Stage Testing**, involves the following steps:

   * Beveiligingstest: Deze stap evalueert het effect van uw toepassingscode op de AEM milieu. Zie [De testresultaten](understand-your-test-results.md) begrijpen voor meer informatie over het testproces.
   * Prestatietesten: Deze stap evalueert de prestaties van uw toepassingscode. Zie [De testresultaten](understand-your-test-results.md) begrijpen voor meer informatie over het testproces.

   ![](assets/Stage_Testing1.png)

   The **Production Deployment**, involves the following steps:

   * **Goedkeuringsaanvraag** (indien ingeschakeld)
   * **Implementatie** van productieplanning (indien ingeschakeld)
   * **CSE-ondersteuning** (indien ingeschakeld)
   * **Distribueren naar productie**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >De Plaatsing **van de Productie van het** Programma wordt toegelaten terwijl het vormen van de pijpleiding.
   >
   >
   >Met deze optie kunt u de productieimplementatie plannen of op **Nu** klikken om de productieimplementatie direct uit te voeren.
   >
   >
   >De geplande datum en tijd worden gespecificeerd in termen van de tijdzone van de gebruiker.
   >
   >
   >Klik op **Bevestigen** om uw instellingen te verifiëren.

   ![](assets/Production_Deployment1.png)

   Zodra u het plaatsingsprogramma bevestigt, voltooit uw codeplaatsing.

   Het volgende scherm wordt weergegeven wanneer de optie **Nu** is geselecteerd in de bovenstaande stap.

   ![](assets/Production_Deployment2.png)

## Implementatieproces {#deployment-process}

In de volgende sectie wordt beschreven hoe AEM- en verzendingspakketten in de fase van het werkgebied en in de productiefase worden geïmplementeerd.

Cloud Manager uploadt alle doel-/*.zip-bestanden die tijdens het productieproces zijn gemaakt naar een opslaglocatie.  Deze artefacten worden teruggewonnen van deze plaats tijdens opstellen fasen van de pijpleiding.

Wanneer de Manager van de Wolk aan niet productietopologieën opstelt, is het doel de plaatsing zo snel mogelijk te voltooien en daarom worden de artefacten gelijktijdig opgesteld aan alle knopen als volgt:

1. Cloud Manager bepaalt of elk artefact een AEM- of verzendingspakket is.
1. Cloud Manager verwijdert alle verzenders van de taakverdeler om de omgeving tijdens de implementatie te isoleren.

   Tenzij anders gevormd kunt u de Veranderingen van de Balancer van de Lading in Dev en de Plaatsing van het Stadium overslaan, namelijk losmaken en stappen in zowel niet productiepijpleidingen, voor ontwikkelmilieu&#39;s, als de productiepijplijn, voor werkgebiedmilieu&#39;s vastmaken.

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >Deze functie wordt naar verwachting vooral gebruikt door 1-1-1 klanten.

1. Elk AEM artefact wordt opgesteld aan elke AEM instantie via de Manager APIs van het Pakket, met pakketgebiedsdelen die de plaatsingsorde bepalen.

   Voor meer informatie over hoe u pakketten kunt gebruiken om nieuwe functionaliteit te installeren, inhoud over te brengen tussen instanties, en file bewaarplaats inhoud, gelieve te verwijzen naar hoe te met Pakketten werken.

   >[!NOTE]
   >
   >Alle AEM artefacten worden opgesteld aan zowel de auteur als de uitgevers. Run-modes zouden hefboomwerking moeten zijn wanneer de knoop-specifieke configuraties worden vereist. Raadpleeg de uitvoeringsmodi voor meer informatie over hoe u met de uitvoeringsmodi uw AEM voor een bepaald doel kunt afstemmen.

1. Het artefact van de verzender wordt als volgt op elke verzender geïmplementeerd:

   1. Er wordt een back-up gemaakt van de huidige configuraties en deze worden naar een tijdelijke locatie gekopieerd
   1. Alle configuraties worden verwijderd, behalve de onveranderlijke bestanden. Raadpleeg Uw Dispatcher Configurations beheren voor meer informatie. Hierdoor worden de mappen gewist zodat er geen zwevende bestanden achterblijven.
   1. Het artefact wordt geëxtraheerd naar de `httpd` map.  Onveranderbare bestanden worden niet overschreven. Wijzigingen die u aanbrengt in onveranderlijke bestanden in uw it-opslagplaats, worden genegeerd op het moment van implementatie.  Deze bestanden vormen de kern van het AMS-verzenderframework en kunnen niet worden gewijzigd.
   1. Apache voert een configuratietest uit. Als er geen fouten worden gevonden, wordt de service opnieuw geladen. Als er een fout optreedt, worden de configuraties hersteld vanaf de back-up, wordt de service opnieuw geladen en wordt de fout gemeld aan Cloud Manager.
   1. Elk pad dat in de pijplijnconfiguratie is opgegeven, wordt ongeldig gemaakt of verwijderd uit het cachegeheugen van de verzender.

   >[!NOTE]
   >
   >Cloud Manager verwacht dat het artefact van de verzender de volledige bestandsset bevat.  Alle Dispatcher-configuratiebestanden moeten aanwezig zijn in de it-opslagplaats. Ontbrekende bestanden of mappen leiden tot een implementatiefout.

1. Nadat alle AEM- en verzendingspakketten naar alle knooppunten zijn geïmplementeerd, worden de verzenders weer toegevoegd aan het taakverdelingsmechanisme en is de implementatie voltooid.

   >[!NOTE]
   >
   >U kunt de veranderingen van de Balancer van de Lading in ontwikkeling en werkgebiedplaatsingen overslaan, namelijk losmaken en stappen in zowel niet productiepijpleidingen, voor ontwikkelaarmilieu&#39;s, als de productiepijplijn, voor werkgebiedmilieu&#39;s vastmaken.

### Implementatie naar productiefase {#deployment-production-phase}

Het proces voor het opstellen aan productietopologieën verschilt lichtjes om effect aan AEM bezoekers van de Plaats te minimaliseren.

Productieimplementaties volgen doorgaans dezelfde stappen als hierboven, maar op een voortschrijdende manier:

1. Implementeer AEM pakketten naar de auteur.
1. Dispatcher1 loskoppelen van het taakverdelingsmechanisme.
1. Implementeer AEM pakketten om te publiceren1 en het verzenderpakket om de verzendingscache van Dispatcher1 leeg te maken.
1. Plaats dispatcher1 terug in het taakverdelingsmechanisme.
1. Als dispatcher1 weer in bedrijf is, koppelt u dispatcher2 af van het taakverdelingsmechanisme.
1. Implementeer AEM pakketten om te publiceren2 en het verzenderpakket om de verzendingscache van Dispatcher2 leeg te maken.
1. Plaats dispatcher2 terug in het taakverdelingsmechanisme.
Dit proces gaat verder tot de plaatsing alle uitgevers en verzenders in de topologie heeft bereikt.


