---
title: Codeimplementatie
description: Leer hoe u uw code implementeert en wat er gebeurt in Cloud Manager wanneer u dat doet.
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 70e68f8af17b0acf644176c2ed3afaf8fc219063
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---


# Codeimplementatie {#code-deployment}

Leer hoe u uw code implementeert en wat er gebeurt in Cloud Manager wanneer u dat doet.

## Code implementeren met Cloud Manager {#deploying-code-with-cloud-manager}

Zodra u uw productiepijplijn met inbegrip van de noodzakelijke bewaarplaats en milieu&#39;s hebt gevormd, bent u bereid om uw code op te stellen.

1. Klikken **Implementeren** van Cloud Manager om het implementatieproces te starten.

   ![De knop Implementeren](/help/assets/Deploy1.png)

1. De **Uitvoering pijpleiding** schermweergaven. Klikken **Opbouwen** om het proces te starten.

   ![Knop Samenstellen](/help/assets/Deploy2.png)

Het bouwstijlproces begint het proces van de codeplaatsing met inbegrip van de volgende stappen:

* Werkgebiedimplementatie
* Werkgebied testen
* Implementatie van productie

U kunt de stappen van diverse plaatsingsprocessen herzien door logboeken, of het herzien van resultaten, voor de testende criteria te bekijken.

## Implementatiestappen {#deployment-steps}

Een aantal acties komt tijdens elke stap van de plaatsing voor, die in deze sectie worden beschreven. Zie de sectie [Implementatieproces — details](#deployment-process) voor technische details van hoe de code zelf achter de schermen wordt opgesteld.

### Implementatiestap werkgebied {#stage-deployment}

De **Werkgebiedimplementatie** De stap omvat de volgende acties:

* **Validatie**: Deze stap zorgt ervoor dat de pijpleiding wordt gevormd om de momenteel beschikbare middelen te gebruiken, bijvoorbeeld dat de gevormde tak bestaat en dat de milieu&#39;s beschikbaar zijn.
* **Testen van build en eenheid**: Deze stap voert een inperkt bouwstijlproces in werking. Zie het document [De Build-omgeving](/help/getting-started/build-environment.md) voor meer informatie.
* **Codescannen**: Deze stap evalueert de kwaliteit van uw toepassingscode. Zie het document [Testresultaten begrijpen](/help/using/code-quality-testing.md) voor meer informatie over het testproces.
* **Distribueren naar werkgebied**

![Werkgebiedimplementatie](/help/assets/Stage_Deployment1.png)

### Teststap werkgebied {#stage-testing}

De **Werkgebied testen** De stap omvat de volgende acties:

* **Beveiligingstests**: Deze stap evalueert het effect van uw code op de AEM. Zie het document [Testresultaten begrijpen](/help/using/code-quality-testing.md) voor meer informatie over het testproces.
   * **Prestatietesten**: Deze stap evalueert de prestaties van uw code. Zie [Testresultaten begrijpen](/help/using/code-quality-testing.md) voor meer informatie over het testproces.

  ![Werkgebied testen](/help/assets/Stage_Testing1.png)

### Implementatiestap voor productie {#production-deployment}

De **Implementatie van productie** stap, omvat de volgende acties:

* **Goedkeuringsaanvraag**
   * Deze optie wordt toegelaten terwijl het vormen van de pijpleiding.
   * Met deze optie kunt u uw productieimplementatie plannen of op **Nu** de productie onmiddellijk uit te voeren.
* **Implementatie van planningsproductie**
   * Deze optie wordt toegelaten terwijl het vormen van de pijpleiding.
   * De geplande datum en tijd worden gespecificeerd in termen van de tijdzone van de gebruiker.
     ![Implementatie plannen](/help/assets/Production_Deployment1.png)
* **CSE-ondersteuning** (indien ingeschakeld)
* **Distribueren naar productie**

![Implementatie van productie](/help/assets/Prod_Deployment1.png)

Zodra uw plaatsing volledig is, is uw code in zijn gerichte milieu en u kunt de logboeken bekijken.

![Implementatie voltooid](/help/assets/Production_Deployment2.png)

## Tijdstippen {#timeouts}

Er wordt een time-out toegepast in de volgende stappen als er op feedback van gebruikers wordt gewacht:

| Stap | Time-out |
|--- |--- |
| Testen van de codekwaliteit | 7 dagen |
| Beveiligingstests | 7 dagen |
| Prestatietesten | 7 dagen |
| Goedkeuringsaanvraag (fase) | 7 dagen |
| Goedkeuringsaanvraag (productie) | 14 dagen |
| Implementatie van planningsproductie | 14 dagen |
| Implementatie van beheerde productie | 14 dagen |

## Implementatieproces — details {#deployment-process}

Cloud Manager uploadt alle doel-/*.zip-bestanden die tijdens het productieproces zijn gemaakt naar een opslaglocatie. Deze artefacten worden teruggewonnen van deze plaats tijdens opstellen fasen van de pijpleiding.

Wanneer de Manager van de Wolk aan niet productietopologieën opstelt, is het doel de plaatsing zo snel mogelijk te voltooien en daarom worden de artefacten gelijktijdig opgesteld aan alle knopen als volgt:

1. Cloud Manager bepaalt of elk artefact een AEM- of verzendingspakket is.
1. Cloud Manager verwijdert alle verzenders van het taakverdelingsmechanisme om de omgeving tijdens de implementatie te isoleren.

   * Tenzij anders geconfigureerd, kunt u wijzigingen in het taakverdelingsmechanisme in ontwikkelings- en staging-implementaties overslaan, d.w.z. voor ontwikkelomgeving, stappen loskoppelen en koppelen in zowel niet-productiepijpleidingen als voor de staging-omgeving in de productiepijplijn.

   ![Load balancer overslaan](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >Deze functie wordt naar verwachting vooral gebruikt door 1-1-1 klanten.

1. Elk AEM artefact wordt opgesteld aan elke AEM instantie via de Manager APIs van het Pakket, met pakketgebiedsdelen die de plaatsingsorde bepalen.

   * Voor meer informatie over hoe u pakketten kunt gebruiken om nieuwe functionaliteit te installeren, inhoud over te brengen tussen instanties, en file bewaarplaats inhoud, gelieve te verwijzen naar het document [Package Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)

   >[!NOTE]
   >
   >Alle AEM artefacten worden opgesteld aan zowel de auteur als de uitgevers. De wijzen van de looppas zouden moeten worden leveraged wanneer de knoop-specifieke configuraties worden vereist. Als u meer wilt weten over de manier waarop u met de uitvoeringsmodi uw AEM voor een bepaald doel kunt instellen, raadpleegt u de [De sectie van Wijzen van de looppas van het document die aan AEM as a Cloud Service opstelt.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)

1. Het artefact van de verzender wordt als volgt op elke verzender geïmplementeerd:

   1. Van de huidige configuraties wordt een back-up gemaakt en naar een tijdelijke locatie gekopieerd.
   1. Alle configuraties worden verwijderd, behalve de onveranderlijke bestanden. Het document raadplegen [Dispatcher Configurations](/help/getting-started/dispatcher-configurations.md) voor meer informatie . Hierdoor worden de mappen gewist zodat er geen zwevende bestanden achterblijven.
   1. Het artefact wordt geëxtraheerd naar de `httpd` directory. Onveranderbare bestanden worden niet overschreven. Wijzigingen die u aanbrengt in onveranderlijke bestanden in uw it-opslagplaats, worden genegeerd op het moment van implementatie. Deze bestanden vormen de kern van het AMS-verzenderframework en kunnen niet worden gewijzigd.
   1. Apache voert een configuratietest uit. Als er geen fouten worden gevonden, wordt de service opnieuw geladen. Als er een fout optreedt, worden de configuraties hersteld vanaf de back-up, wordt de service opnieuw geladen en wordt de fout gemeld aan Cloud Manager.
   1. Elk pad dat in de pijplijnconfiguratie is opgegeven, wordt ongeldig gemaakt of verwijderd uit het cachegeheugen van de verzender.

   >[!NOTE]
   >
   >Cloud Manager verwacht dat het artefact van de verzender de volledige bestandsset bevat. Alle Dispatcher-configuratiebestanden moeten aanwezig zijn in de it-opslagplaats. Ontbrekende bestanden of mappen leiden tot een implementatiefout.

1. Nadat alle AEM- en verzendingspakketten naar alle knooppunten zijn geïmplementeerd, worden de verzenders weer toegevoegd aan het taakverdelingsmechanisme en is de implementatie voltooid.

   >[!NOTE]
   >
   >U kunt veranderingen in het taakverdelingsmechanisme in ontwikkeling en het opvoeren van Plaatsingen, d.w.z. voor ontwikkelomgeving overslaan, stappen in zowel niet productiepijpleidingen losmaken en vastmaken, als voor het opvoeren van milieu de productiepijpleiding.

### Implementatie naar productiefase {#deployment-production-phase}

Het proces voor het opstellen aan productietopologieën verschilt lichtjes om effect aan AEM plaatsbezoekers te minimaliseren.

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

In kritieke situaties moeten Adobe Managed Services-klanten mogelijk codewijzigingen implementeren in hun werkgebied- en productieomgeving zonder te wachten tot een volledige testcyclus van Cloud Manager wordt uitgevoerd.

Om deze situaties aan te pakken, kan de productiepijplijn van de Manager van de Wolk op een noodwijze worden uitgevoerd. Als deze modus wordt gebruikt, worden de stappen voor de beveiligings- en prestatietest niet uitgevoerd. Alle andere stappen, met inbegrip van om het even welke gevormde goedkeuringsstappen, worden uitgevoerd zoals op de normale wijze van de pijpleidingsuitvoering.

>[!NOTE]
>
>De functie voor de uitvoering van de noodpijpleiding wordt per programma geactiveerd door de succestechnici van de Klant.

### Uitvoermodus voor noodpijpleiding gebruiken {#using-emergency-pipeline}

Wanneer het beginnen van een uitvoering van de productiepijplijn, als de eigenschap van de spoedpijpleiding uitvoeringswijze voor het programma is geactiveerd, kunt u de uitvoering op of normale of noodwijze van een dialoogdoos beginnen.

![Opties voor pijpleidingen uitvoeren](/help/assets/execution-emergency1.png)

Wanneer het bekijken van de pagina van de details van de pijpleidingsuitvoering voor een uitvoering die op noodwijze wordt in werking gesteld, tonen de broodkruimels bij de bovenkant van het scherm een indicator dat de pijpleiding op noodwijze uitvoert.

![Breedkruimels in de noodmodus](/help/assets/execution-emergency2.png)

Het uitvoeren van een pijpleiding op noodwijze kan ook door de Manager API van de Wolk of CLI worden gedaan. Als u een uitvoering wilt starten in de noodmodus, dient u een `PUT` verzoek aan het de uitvoeringseindpunt van de pijpleiding met de vraagparameter `?pipelineExecutionMode=EMERGENCY` of, bij gebruik van de CLI:

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## Het opnieuw uitvoeren van een Plaatsing van de Productie {#reexecute-deployment}

In zeldzame gevallen kunnen de stappen van de productielocatie om voorbijgaande redenen ontbreken. In dergelijke gevallen wordt heruitvoering van de productieleidingsstap ondersteund zolang de productieleidingsstap is voltooid, ongeacht het type voltooiing (bv. succesvol, geannuleerd of niet succesvol). De heruitvoering leidt tot een nieuwe uitvoering gebruikend de zelfde pijpleiding die uit drie stappen bestaat.

1. **De stap validate** - Dit is in wezen de zelfde bevestiging die tijdens een normale pijpleidingsuitvoering voorkomt.
1. **De bouwstijlstap** - In de context van een heruitvoering kopieert de bouwstap artefacten en voert geen nieuw bouwstijlproces uit.
1. **De productieleidingsstap** - Dit gebruikt de zelfde configuratie en de opties zoals de stap van de productieplaatsing in een normale pijpleidingsuitvoering.

In dergelijke omstandigheden waarin een wederuitvoering mogelijk is, biedt de statuspagina van de productiepijpleiding de **Opnieuw uitvoeren** naast de gebruikelijke **Buildlog downloaden** -optie.

![De optie Opnieuw uitvoeren in het venster Overzicht van de pijplijn](/help/assets/re-execute.png)

>[!NOTE]
>
>In een heruitvoering, wordt de bouwstijlstap geëtiketteerd in UI om erop te wijzen dat het artefacten kopieert, niet re-bouwt.

### Beperkingen {#limitations}

* Het opnieuw uitvoeren van de stap van de productieplaatsing is slechts beschikbaar voor de laatste uitvoering.
* Heruitvoering is niet beschikbaar voor terugdraaiacties of het uitvoeren van push-updates.
* Als de laatste uitvoering is mislukt op een willekeurig punt vóór de stap voor de implementatie van de productie, is het niet mogelijk de productie opnieuw uit te voeren.


### API opnieuw uitvoeren {#reexecute-api}

U kunt niet alleen gebruikmaken van de interface, maar ook van [De API voor Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) om wederuitvoeringen in gang te zetten en executies te identificeren die als wederuitvoeringen werden teweeggebracht.

#### Een nieuwe uitvoering activeren {#triggering}

Als u een nieuwe uitvoering wilt activeren, kunt u een `PUT` Het verzoek moet aan de HAL-link worden gedaan `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` op de productie opstellen stapstaat.

* Als deze koppeling aanwezig is, kan de uitvoering vanaf die stap opnieuw worden gestart.
* Als dit niet het geval is, kan de uitvoering niet vanaf die stap opnieuw worden gestart.

Deze verbinding is slechts ooit beschikbaar voor de productie stelt stap op.

```javascript
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

De syntaxis van de HAL-koppeling `href` De waarde is slechts een voorbeeld en de daadwerkelijke waarde zou altijd van de verbinding van HAL moeten worden gelezen en niet geproduceerd.

Een `PUT` verzoek aan dit eindpunt zal resulteren in een `201` de nieuwe executie zal , indien succesvol en als responsinstantie , worden voorgesteld . Dit is vergelijkbaar met het starten van een normale uitvoering via de API.

#### Een nieuwe uitvoering identificeren {#identifying}

Herhaalde uitvoeringen kunnen worden geïdentificeerd door de waarde `RE_EXECUTE` in de `trigger` veld.
