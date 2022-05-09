---
title: Uw code implementeren
seo-title: Deploy your Code
description: Geeft een overzicht van het implementatieproces in Cloud Manager
seo-description: Learn how to deploy your code once you have configured your pipeline (repository, environment, and testing environment)
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: Code Deployment
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 9a9d7067a1369e80ccf9b2925369a466b3da2901
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Uw code implementeren {#deploy-your-code}

## Code implementeren met Cloud Manager {#deploying-code-with-cloud-manager}

>[!NOTE]
>Ga voor meer informatie over het implementeren van code voor Cloud Manager in AEM as a Cloud Service naar [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager).

Nadat u de productiepijpleiding hebt geconfigureerd (opslagruimte, omgeving en testomgeving), kunt u uw code implementeren.

1. Klikken **Implementeren** van Cloud Manager om het implementatieproces te starten.

   ![](assets/Deploy1.png)

1. De **Uitvoering pijpleiding** weergegeven.

   Klikken **Opbouwen** om het proces te starten.

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
   * Testen van build en eenheid: Deze stap stelt een containerized bouwstijlproces in werking. Zie [Inzicht in de omgeving van de build](/help/using/build-environment-details.md) voor meer informatie over de ontwikkelomgeving.
   * Codescannen: Deze stap evalueert de kwaliteit van uw toepassingscode. Zie [De testresultaten begrijpen](understand-your-test-results.md) voor meer informatie over het testproces.
   * Distribueren naar werkgebied

   ![](assets/Stage_Deployment1.png)

   De **Werkgebiedtests**, omvat de volgende stappen:

   * Beveiligingstest: Deze stap evalueert het effect van uw toepassingscode op de AEM milieu. Zie [De testresultaten begrijpen](understand-your-test-results.md) voor meer informatie over het testproces.
   * Prestatietesten: Deze stap evalueert de prestaties van uw toepassingscode. Zie [De testresultaten begrijpen](understand-your-test-results.md) voor meer informatie over het testproces.

   ![](assets/Stage_Testing1.png)

   De **Implementatie van productie**, omvat de volgende stappen:

   * **Goedkeuringsaanvraag** (indien ingeschakeld)
   * **Implementatie van planningsproductie** (indien ingeschakeld)
   * **CSE-ondersteuning** (indien ingeschakeld)
   * **Distribueren naar productie**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >De **Implementatie van planningsproductie** wordt toegelaten terwijl het vormen van de pijpleiding.
   >
   >
   >Met deze optie kunt u uw productieimplementatie plannen of op **Nu** de productie onmiddellijk te implementeren.
   >
   >
   >De geplande datum en tijd worden gespecificeerd in termen van de tijdzone van de gebruiker.
   >
   >
   >Klikken **Bevestigen** om uw instellingen te verifiëren.

   ![](assets/Production_Deployment1.png)

   Zodra u het plaatsingsprogramma bevestigt, voltooit uw codeplaatsing.

   Het volgende scherm wordt weergegeven wanneer **Nu** is geselecteerd in de bovenstaande stap.

   ![](assets/Production_Deployment2.png)

## Tijdstippen {#timeouts}

Er wordt een time-out toegepast in de volgende stappen als er op feedback van gebruikers wordt gewacht:

| Stap | Time-out |
|--- |--- |
| Testen van de codekwaliteit | 14 dagen |
| Beveiligingstests | 14 dagen |
| Prestatietesten | 14 dagen |
| Goedkeuringsaanvraag | 14 dagen |
| Implementatie van planningsproductie | 14 dagen |
| CSE-ondersteuning | 14 dagen |

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
   1. Het artefact wordt geëxtraheerd naar de `httpd` directory.  Onveranderbare bestanden worden niet overschreven. Wijzigingen die u aanbrengt in onveranderlijke bestanden in uw it-opslagplaats, worden genegeerd op het moment van implementatie.  Deze bestanden vormen de kern van het AMS-verzenderframework en kunnen niet worden gewijzigd.
   1. Apache voert een configuratietest uit. Als er geen fouten worden gevonden, wordt de service opnieuw geladen. Als er een fout optreedt, worden de configuraties hersteld vanaf de back-up, wordt de service opnieuw geladen en wordt de fout gemeld aan Cloud Manager.
   1. Elk pad dat in de pijplijnconfiguratie is opgegeven, wordt ongeldig gemaakt of verwijderd uit het cachegeheugen van de verzender.

   >[!NOTE]
   >Cloud Manager verwacht dat het artefact van de verzender de volledige bestandsset bevat.  Alle Dispatcher-configuratiebestanden moeten aanwezig zijn in de it-opslagplaats. Ontbrekende bestanden of mappen leiden tot een implementatiefout.

1. Nadat alle AEM- en verzendingspakketten naar alle knooppunten zijn geïmplementeerd, worden de verzenders weer toegevoegd aan het taakverdelingsmechanisme en is de implementatie voltooid.

   >[!NOTE]
   >U kunt de veranderingen van de Balancer van de Lading in ontwikkeling en werkgebiedplaatsingen overslaan, namelijk losmaken en stappen in zowel niet productiepijpleidingen, voor ontwikkelaarmilieu&#39;s, als de productiepijplijn, voor werkgebiedmilieu&#39;s vastmaken.

### Implementatie naar productiefase {#deployment-production-phase}

Het proces voor het opstellen aan productietopologieën verschilt lichtjes om effect aan AEM bezoekers van de Plaats te minimaliseren.

Productieimplementaties volgen doorgaans dezelfde stappen als hierboven, maar op een voortschrijdende manier:

1. Implementeer AEM pakketten naar de auteur.
1. Dispatcher1 loskoppelen van het taakverdelingsmechanisme.
1. Implementeer AEM pakketten om te publiceren1 en het verzendingspakket om dispatcher1 parallel in de cache van de uitlijningsdispatcher te plaatsen.
1. Plaats dispatcher1 terug in het taakverdelingsmechanisme.
1. Als dispatcher1 weer in bedrijf is, koppelt u dispatcher2 af van het taakverdelingsmechanisme.
1. Implementeer AEM pakketten om te publiceren2 en het verzendingspakket naar dispatcher2 in parallel, uitlijningscachegeheugen.
1. Plaats dispatcher2 terug in het taakverdelingsmechanisme.
Dit proces gaat verder tot de plaatsing alle uitgevers en verzenders in de topologie heeft bereikt.

## Uitvoermodus noodleiding {#emergency-pipeline}

In kritieke situaties moeten klanten van Adobe Managed Services mogelijk codewijzigingen implementeren in hun werkgebied- en productieomgeving zonder te wachten tot een volledige testcyclus van Cloud Manager is uitgevoerd.

Om deze situaties aan te pakken, kan de productiepijplijn van de Manager van de Wolk in een uitvoeren *noodsituatie* in. Wanneer deze modus wordt gebruikt, worden de beveiligings- en prestatieteststappen niet uitgevoerd; alle andere stappen, met inbegrip van om het even welke gevormde goedkeuringsstappen, worden uitgevoerd zoals op de normale wijze van de pijpleidingsuitvoering.

>[!NOTE]
>Mogelijkheid tot uitvoering van de noodpijpleiding wordt op programmasleutel geactiveerd door de succestechnici van de klant.

### Uitvoermodus voor noodpijpleiding gebruiken {#using-emergency-pipeline}

Wanneer u een productiepijpuitvoering start en deze functie is geactiveerd, kunt u de uitvoering starten in de normale modus of in de noodmodus vanuit het dialoogvenster, zoals in de onderstaande afbeelding wordt getoond.

![](assets/execution-emergency1.png)

Bovendien, die de pagina bekijken van de details van de pijpleidingsuitvoering voor een uitvoering die in noodmodus in werking wordt gesteld, toont de broodkruimels bij de bovenkant van het scherm een indicator dat de noodwijze voor deze bepaalde uitvoering werd gebruikt.

![](assets/execution-emergency2.png)

Het maken van een pijpleiding kan op deze noodwijze ook door de Manager API van de Wolk of CLI worden gedaan. Om een uitvoering op de Wijze van de Noodsituatie te beginnen, leg een verzoek van de PUT aan het uitvoeringsparameter van de pijpleiding met de vraagparameter voor `?pipelineExecutionMode=EMERGENCY` of, bij gebruik van de CLI:

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

>[!IMPORTANT]
>Gebruiken `--emergency` markering moet mogelijk worden bijgewerkt naar de laatste `aio-cli-plugin-cloudmanager` versie.

## Een productieimplementatie opnieuw uitvoeren {#Reexecute-Deployment}

Heruitvoering van de productieleidingsstap wordt ondersteund voor uitvoeringen waarbij de productieleidingsstap is voltooid. Het type voltooiing is niet belangrijk - de implementatie kan succesvol zijn (alleen voor AMS-programma&#39;s), geannuleerd of mislukt. Dit gezegd zijnde, wordt verwacht dat het primaire gebruiksgeval gevallen is waarin de productielocatie om tijdelijke redenen is mislukt. De heruitvoering leidt tot een nieuwe uitvoering gebruikend de zelfde pijpleiding. Deze nieuwe uitvoering bestaat uit drie stappen:

1. Bevestig stap - dit is hoofdzakelijk de zelfde bevestiging die tijdens een normale pijpleidingsuitvoering voorkomt.
1. De bouwstijlstap - in de context van een heruitvoering, kopieert de bouwstijlstap artefacten, niet echt voert een nieuw bouwstijlproces uit.
1. De stap van de productieleiding - dit gebruikt de zelfde configuratie en de opties zoals de stap van de productieleiding in een normale pijpleidingsuitvoering.

De bouwstijlstap kan lichtjes verschillend geëtiketteerd in UI zijn om erop te wijzen dat het artefacten kopieert, niet herbouwt.

![](assets/Re-deploy.png)

Beperkingen:

* Het opnieuw uitvoeren van de stap van de productieplaatsing zal slechts bij de laatste uitvoering beschikbaar zijn.
* Heruitvoering is niet beschikbaar voor terugdraaiacties.
* Als de laatste uitvoering een terugdraaiuitvoering is, is wederuitvoering niet mogelijk.
* Als de laatste uitvoering een uitvoering van een push-update is, is het niet mogelijk deze opnieuw uit te voeren.
* Als de laatste uitvoering is mislukt op een willekeurig punt vóór de stap voor de implementatie van de productie, is het niet mogelijk de productie opnieuw uit te voeren.

### API opnieuw uitvoeren {#Reexecute-API}

### Identificatie van een uitvoering van de uitvoering

Om te bepalen of een uitvoering een uitvoering is die opnieuw wordt uitgevoerd, kan het triggerveld worden gecontroleerd. De waarde ervan zal *RE_EXECUTE*.

### Nieuwe uitvoering activeren

Om een heruitvoering te activeren, moet een verzoek van de PUT aan de Verbinding van het HAL &lt; (<http://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> op de status van de stap Implementeren van de productie. Als deze koppeling aanwezig is, kan de uitvoering vanaf die stap opnieuw worden gestart. Als dit niet het geval is, kan de uitvoering niet vanaf die stap opnieuw worden gestart. In de aanvankelijke versie, zal deze verbinding slechts ooit op de productie zijn opstellen stap maar de toekomstige versies kunnen het beginnen van de pijpleiding van andere stappen steunen. Voorbeeld:

```Javascript
 {
  "_links": {
    "http://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


De syntaxis van de HAL-koppeling *href*  bovenstaande waarde is niet bedoeld als referentiepunt. De werkelijke waarde moet altijd worden gelezen van de HAL-koppeling en niet worden gegenereerd.

Een *PUT* verzoek aan dit eindpunt zal resulteren in een *201* de nieuwe executie zal , indien succesvol en als responsinstantie , worden voorgesteld . Dit is vergelijkbaar met het starten van een normale uitvoering via de API.
