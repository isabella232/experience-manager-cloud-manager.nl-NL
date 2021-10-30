---
title: Uw CI/CD-pijplijn configureren
seo-title: Configure your CI/CD Pipeline
description: Volg deze pagina om uw pijpleidingsmontages van de Manager van de Wolk te vormen.
seo-description: Before you start to deploy your code, you must configure your pipeline settings from the AEM Cloud Manager.
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 2be8f290b58fff2991f876c37dd1b499bc6c5352
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Uw CI/CD-pijplijn configureren {#configure-your-ci-cd-pipeline}

>[!NOTE]
>Als u wilt leren hoe u CI/CD Pipeline voor Cloud Manager in AEM as a Cloud Service kunt configureren, raadpleegt u [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager).

De volgende pagina verklaart hoe te om te vormen **Pijpleiding**. Om meer conceptuele informatie te herzien over hoe de pijpleiding werkt zie [Overzicht van CI/CD-pijpleiding](ci-cd-pipeline.md).


## De stroom begrijpen {#understanding-the-flow}

U kunt uw pipeline configureren vanaf de tegel **Pipelines** in de [!UICONTROL Cloud Manager]-gebruikersinterface.

De Manager van de Plaatsing is verantwoordelijk voor vestiging de pijpleiding. Wanneer u dit doet, selecteert u eerst een vertakking in het menu **Git Repository**. De configuratie van de pijpleiding bestaat uit:

* het bepalen van de trekker die de pijpleiding zal beginnen.
* het definiëren van de parameters die de productielocatie bepalen.
* configureren van de testparameters voor prestaties.

## Videozelfstudie {#video-tutorial-one}

### Pipeline configureren in Cloud Manager {#config-pipeline-video}

De configuratie van de Pijpleiding van de Productie CI/CD bepaalt de trekker die de pijpleiding, parameters zal in werking stellen die de plaatsing van de productie en de parameters van de prestatietest controleren.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## De pijplijn instellen {#setting-up-the-pipeline}

>[!CAUTION]
>
>De pijplijn kan niet worden ingesteld totdat de Git-opslagplaats ten minste één vertakking en [Programma instellen](setting-up-program.md) is voltooid.

Alvorens u begint uw code op te stellen, moet u uw pijpleidingsmontages van vormen [!UICONTROL Cloud Manager].

>[!NOTE]
>
>U kunt de pijpleidingsmontages na aanvankelijke opstelling veranderen.

### Een nieuwe productiepijpleiding toevoegen uit een pijplijnkaart {#adding-production-pipeline}

Als u uw programma hebt ingesteld en minstens één omgeving hebt die [!UICONTROL Cloud Manager] UI, bent u bereid om een productiepijplijn toe te voegen.

Voer de volgende stappen uit om het gedrag en de voorkeuren voor uw productiepijplijn te configureren:

1. Ga naar de **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **+Toevoegen** en selecteert u **Productiepijpleiding toevoegen**.

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **Productiepijpleiding toevoegen** wordt weergegeven.

   1. Voer de **Naam pijpleiding**. U kunt de **Bewaarplaats** en de **Git Branch**.

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. U kunt instellen **Implementatieactivering** en **Belangrijk gedrag metrische fouten** van **Implementatieopties**.

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      U kunt de volgende plaatsingstrekkers toewijzen om de pijpleiding te beginnen:

      * **Handmatig** - het gebruiken van UI begint manueel de pijpleiding.
      * **Wijzigingen in Git** - start de CI/CD-pijplijn wanneer er verplichtingen aan de gevormde it-tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.

      Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitshates wordt ontmoet.

      Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

      * **Telkens vragen** - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
      * **Direct mislukken** - Indien geselecteerd, zal de pijpleiding worden geannuleerd wanneer een Belangrijke mislukking voorkomt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
      * **Direct doorgaan** - Indien geselecteerd, zal de pijpleiding automatisch te werk gaan wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.
   1. Selecteer **Implementatieopties**.

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **Goedkeuren na implementatie van werkgebied** functies die vergelijkbaar zijn met de goedkeuring vóór de productielocatie, maar die onmiddellijk na de stationeringsstap van het werkgebied plaatsvinden, dat wil zeggen voordat tests worden uitgevoerd, in vergelijking met de goedkeuring vóór de productielocatie, die wordt uitgevoerd nadat alle tests zijn voltooid.

      * **Wijzigingen in taakverdeling overslaan** De wijzigingen worden overgeslagen.
   1. Selecteer **Dispatcher Configuration** voor Stage. Voer het pad in en selecteer de handeling uit **Type** en klik op **Pad toevoegen**. U kunt maximaal 100 paden per omgeving opgeven.

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. Selecteer **Implementatieopties** voor Productie. Nu definieert u de parameters die de productieimplementatie bepalen.

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      De drie beschikbare opties zijn als volgt:

      * **Live goedkeuring gebruiken** - Een plaatsing moet manueel door een bedrijfseigenaar, een projectmanager, of een plaatsingsmanager via worden goedgekeurd [!UICONTROL Cloud Manager] UI.

      * **Gepland** - Met deze optie kan de gebruiker de geplande implementatie van de productie inschakelen.

         >[!NOTE]
         >Indien **Gepland** de optie wordt geselecteerd, kunt u uw productieleiding aan de pijpleiding plannen **na** de stationering van de fase (en **GoLive-goedkeuring gebruiken**, als dat is toegelaten) om op een te plaatsen programma te wachten. De gebruiker kan er ook voor kiezen om de productieimplementatie onmiddellijk uit te voeren.
         >
         >Zie [Uw code implementeren](deploying-code.md)om het implementatieschema in te stellen of de productie onmiddellijk uit te voeren.

         * **CSE-overzicht gebruiken** - Een CSE is betrokken om de implementatie daadwerkelijk te starten. Tijdens pijpleidingsopstelling of geef uit wanneer CSE Toezicht wordt toegelaten, heeft de Manager van de Plaatsing de optie om te selecteren:

            * **Elke CSE**: verwijst naar elke beschikbare CSE
            * **Mijn CSE**: verwijst naar specifieke CSE die aan de klant of hun steun wordt toegewezen, als CSE uit het bureau is
   1. Stel de **Dispatcher Configurations** voor Productie. Voer het pad in en selecteer de handeling uit **Type** en klik op **Pad toevoegen**. U kunt maximaal 100 paden per omgeving opgeven.

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      Als Manager van de Plaatsing, hebt u de kans om een reeks inhoudspaden te vormen die of **ongeldig** of **gespoeld** in het AEM Dispatcher-cachegeheugen voor publicatie-instanties, terwijl u een pijplijn instelt of bewerkt.

      U kunt een afzonderlijke reeks wegen voor de plaatsing van het Stadium en van de Productie vormen. Indien gevormd, zullen deze geheim voorgeheugenacties als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher - ongeldig maken voert een cachevalidatie uit, net als wanneer de inhoud van de auteur wordt geactiveerd om te publiceren. flush voert een geheim voorgeheugenschrapping uit.

      Over het algemeen verdient het de voorkeur de actie voor invalideren te gebruiken, maar er kunnen zich gevallen voordoen waarin flushing vereist is, met name bij gebruik van AEM Client Libraries voor HTML.

      >[!NOTE]
      >
      >Zie [Overzicht van verzending](dispatcher-configurations.md) Meer informatie over het in cache plaatsen van Dispatcher.





1. Klikken op **Doorgaan** zodra u alle opties hebt geselecteerd.

1. Selecteer uw opties in het menu **Werkgebiedtests** stap. U kunt configureren *AEM Sites* en *AEM Assets* Het Testen van prestaties, afhankelijk van welke producten u vergunning hebt gegeven. Zie [Prestatietesten](understand-your-test-results.md#performance-testing) voor meer informatie .

   1. Selecteer uw opties uit **Sites Content Delivery/Distributed Load Weight**. Zie [AEM Sites in Performance Testing](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites) voor meer informatie .

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. Selecteer uw opties uit **Distributie voor tests op middelenprestaties**. Zie [AEM Assets in Performance Testing](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets) voor meer informatie .

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. Klikken op **Opslaan** de toevoeging van een productiepijpleiding voltooien.

### Een productiepijpleiding bewerken {#editing-prod-pipeline}

U kunt de pijpleidingsconfiguraties van de **Programmaoverzicht** pagina.

Volg de stappen hieronder om de gevormde pijpleiding uit te geven:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **...** van de **Pijpleidingen** kaart en klik op **Bewerken**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. De **Productiepijpleiding bewerken** wordt weergegeven.

   1. De **Configuratie** kunt u de **Naam pijpleiding**, **Bewaarplaats**, **Git Branch**, **Implementatieactivering**, **Gedrag belangrijke metrische fout**, **Implementatieopties** en **Dispatcher Configurations**.

      >[!NOTE]
      >Zie [Opslagplaatsen toevoegen en beheren](/help/using/cloud-manager-repositories.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.


   1. De **Werkgebiedtests** biedt u een optie om de opties opnieuw te selecteren vanuit **Sites Content Delivery/Distributed Load Weight** en **Distributie voor tests op middelenprestaties**.

1. Klikken op **Bijwerken** zodra u klaar bent met het bewerken van de pijplijn.

### Aanvullende acties voor productiepijpleiding {#additional-prod-actions}

#### Een productiepijpleiding uitvoeren {#run-prod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen in werking stellen:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **...** van de **Pijpleidingen** kaart en klik op **Uitvoeren**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### Een productiepijpleiding verwijderen {#delete-prod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen schrappen:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **...** van de **Pijpleidingen** kaart en klik op **Verwijderen**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

   >[!NOTE]
   >Een gebruiker in de rol van de Manager van de Plaatsing kan de pijpleiding van de Productie op een zelfbediening manier via **Verwijderen** optie van de kaart van de Pijpleiding.

## Uitsluitend pijplijnen zonder productie en codekwaliteit

Naast de hoofdpijpleiding die naar het stadium en de productie wordt uitgerold, kunnen de klanten extra pijpleidingen opzetten, die **Niet-productiepijpleidingen**. Deze pijpleidingen voeren altijd de bouw en de stappen van de codekwaliteit uit. Ze kunnen optioneel ook worden geïmplementeerd in de omgeving van Adobe Managed Services.

## Videozelfstudie {#video-tutorial-two}

### Uitsluitend pijplijnen voor beheer van wolken zonder productie en kwaliteit van code {#non-prod-video}

CI/CD de niet productiepijpleidingen zijn verdeeld in twee categorieën, de pijpleidingen van de Kwaliteit van de Code, en de pijpleidingen van de Plaatsing. Codekwaliteitpijplijnen zorgen ervoor dat alle code van een Git-vertakking wordt samengesteld en wordt geëvalueerd op basis van de codescanfunctie van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### Een niet-productiepijpleiding toevoegen {#add-non-production-pipeline}

Op het thuisscherm worden deze pijpleidingen op een nieuwe kaart vermeld:

1. Toegang krijgen tot **Pijpleidingen** kaart van het startscherm van Cloud Manager. Klikken op **+Toevoegen** en selecteert u **Niet-productiepijpleiding toevoegen**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **Niet-productiepijpleiding toevoegen**  wordt weergegeven. Selecteer het type pijpleiding u wilt creëren, of **Codekwaliteit, pijplijn** of **Implementatiepijp**.

   Bovendien kunt u ook instellen **Implementatieactivering** en **Belangrijk gedrag metrische fouten** van **Implementatieopties**. Klikken op **Doorgaan**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. De nieuwe niet-productiepijplijn wordt nu weergegeven in de **Pijpleidingen** kaart.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   De pijpleiding wordt getoond op de kaart op het huisscherm met drie acties, zoals hieronder getoond:

   * **Toevoegen** - staat toe dat een nieuwe pijpleiding wordt toegevoegd.
   * **Repo-info openen** - stelt de gebruiker in staat de informatie op te halen die nodig is om toegang te krijgen tot de gegevensopslagruimte van Cloud Manager Git.
   * **Meer informatie** - navigeert naar inzicht in de bron van de Documentatie van de CI/CD-pijpleiding.

### Een niet-productiepijplijn bewerken {#editing-nonprod-pipeline}

U kunt de pijpleidingsconfiguraties van de **Pipelkaart** van **Programmaoverzicht** pagina.

Voer de onderstaande stappen uit om de geconfigureerde niet-productiepijplijn te bewerken:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Selecteer de niet-productiepijplijn en klik op **...**. Klikken op **Bewerken**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. De **Productiepijpleiding bewerken** wordt weergegeven waarin u het dialoogvenster **Naam pijpleiding**, **Bewaarplaats**, **Git Branch**, **Implementatieactivering**, en **Gedrag belangrijke metrische fout**.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >Zie [Opslagplaatsen toevoegen en beheren](/help/using/cloud-manager-repositories.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.

   U kunt de volgende plaatsingstrekkers toewijzen om de pijpleiding te beginnen:

   * **Handmatig** - het gebruiken van UI begint manueel de pijpleiding.
   * **Wijzigingen in Git** - start de CI/CD-pijplijn wanneer er verplichtingen aan de gevormde it-tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.

   Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitshates wordt ontmoet. Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

   * **Telkens vragen** - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
   * **Direct mislukken** - Indien geselecteerd, zal de pijpleiding worden geannuleerd wanneer een Belangrijke mislukking voorkomt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
   * **Direct doorgaan** - Indien geselecteerd, zal de pijpleiding automatisch te werk gaan wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.


1. Klikken op **Bijwerken** als u klaar bent met het bewerken van de niet-productiepijplijn.

### Aanvullende niet-productie pijplijnhandelingen {#additional-nonprod-actions}

#### Een niet-productiepijpleiding uitvoeren {#run-nonprod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen in werking stellen:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **...** van de **Pijpleidingen** kaart en klik op **Uitvoeren**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/nonprod-run1.png)

#### Schrapping van een niet-productiepijpleiding {#delete-nonprod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen schrappen:

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina.

1. Klikken op **...** van de **Pijpleidingen** kaart en klik op **Verwijderen**, zoals weergegeven in onderstaande afbeelding.

   ![](/help/using/assets/configure-pipelines/nonprod-delete.png)


## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen.

Zie [Uw code implementeren](deploying-code.md) voor meer informatie .
