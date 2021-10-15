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
source-git-commit: 78a6c939cdb7c4335891e27209b221fc3e6efec2
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 0%

---

# Uw CI/CD-pijplijn configureren {#configure-your-ci-cd-pipeline}

>[!NOTE]
>Zie [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) voor meer informatie over het configureren van CI/CD Pipeline voor Cloud Manager in AEM as a Cloud Service.

De volgende pagina verklaart hoe te om **Pipeline** te vormen. Meer conceptuele informatie over bekijken hoe de pijpleiding [CI/CD pijpleiding overzicht](ci-cd-pipeline.md) ziet.

## Videozelfstudie {#video-tutorial-one}

### Pipeline configureren in Cloud Manager {#config-pipeline-video}

De configuratie van de Pijpleiding van de Productie CI/CD bepaalt de trekker die de pijpleiding, parameters zal in werking stellen die de plaatsing van de productie en de parameters van de prestatietest controleren.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## De stroom begrijpen {#understanding-the-flow}

U kunt uw pipeline configureren vanaf de tegel **Pipelines** in de [!UICONTROL Cloud Manager]-gebruikersinterface.

De Manager van de Plaatsing is verantwoordelijk voor vestiging de pijpleiding. Als u dit doet, selecteert u eerst een vertakking in de **Git Repository**. De configuratie van de pijpleiding bestaat uit:

* het bepalen van de trekker die de pijpleiding zal beginnen.
* het definiëren van de parameters die de productielocatie bepalen.
* configureren van de testparameters voor prestaties.

## De pijplijn instellen {#setting-up-the-pipeline}

>[!CAUTION]
>
>De pijpleiding kan niet worden opstelling tot de bewaarplaats van de Git minstens één tak heeft en [Opstelling van het Programma](setting-up-program.md) volledig is.

Alvorens u begint om uw code op te stellen, moet u uw pijpleidingsmontages van [!UICONTROL Cloud Manager] vormen.

>[!NOTE]
>
>U kunt de pijpleidingsmontages na aanvankelijke opstelling veranderen.

## Een nieuwe productiepijpleiding toevoegen uit een pijplijnkaart {#adding-production-pipeline}

Zodra u opstelling uw programma hebt en minstens één milieu gebruikend [!UICONTROL Cloud Manager] UI heeft, bent u bereid om een productiepijplijn toe te voegen.

Voer de volgende stappen uit om het gedrag en de voorkeuren voor uw productiepijplijn te configureren:

1. Navigeer naar de **Pipelines**-kaart van de pagina **Program Overview**.

1. Klik op **+Add** en selecteer **Productiepijplijn toevoegen**.

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **De vertoningen van de** de dialoogdoos van de Pijl van de Productie toevoegen.

   1. Voer de **Naam van de pijpleiding** in. U kunt de **Repository** en **Git Branch** kiezen.

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. U kunt **Implementatietrigger** en **Belangrijk gedrag voor metrische fouten** instellen vanuit **Implementatieopties**.

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      U kunt de volgende plaatsingstrekkers toewijzen om de pijpleiding te beginnen:

      * **Handmatig**  - de UI gebruikt manueel begint de pijpleiding.
      * **Bij de Veranderingen**  van het Git - begint de pijpleiding CI/CD wanneer er toezeggingen aan de gevormde git tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.

      Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitshates wordt ontmoet.

      Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

      * **Telkens**  vragen - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
      * **Direct**  mislukt - Als deze optie is geselecteerd, wordt de pijplijn geannuleerd wanneer een belangrijke fout optreedt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
      * **Ga onmiddellijk**  verder - als geselecteerd, zal de pijpleiding automatisch te werk wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.
   1. Selecteer **Implementatieopties**.

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **Goedkeuren na** implementatie van het werkgebied is vergelijkbaar met de goedkeuringsfuncties vóór de implementatie van de productie, maar vindt direct plaats na de implementatiestap van het werkgebied, dat wil zeggen voordat er tests worden uitgevoerd, in vergelijking met de goedkeuring vóór de implementatie van de productie, die wordt uitgevoerd nadat alle tests zijn voltooid.

      * **Bij de wijzigingen in Load Balancer** overslaan worden de wijzigingen overgeslagen.
   1. Selecteer **Dispatcher Configuration** for Stage. Ga de weg in, selecteer de actie van **Type**, en klik **voeg Weg** toe. U kunt maximaal 100 paden per omgeving opgeven.

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. Selecteer **Implementatieopties** voor Productie. Nu definieert u de parameters die de productieimplementatie bepalen.

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      De drie beschikbare opties zijn als volgt:

      * **Gebruik Live goedkeuring**  - Een implementatie moet handmatig worden goedgekeurd door een bedrijfseigenaar, projectmanager of implementatiebeheerder via de  [!UICONTROL Cloud Manager] gebruikersinterface.

      * **Gepland**  - Deze optie staat de gebruiker toe om de geplande productie plaatsing toe te laten.

         >[!NOTE]
         >Als **Gepland** optie wordt geselecteerd, kunt u uw productiesplaatsing aan de pijpleiding **na** de werkgebiedplaatsing (en **Gebruik GoLive Goedkeuring**, als dat is toegelaten) plannen om op een te plaatsen programma te wachten. De gebruiker kan er ook voor kiezen om de productieimplementatie onmiddellijk uit te voeren.
         >
         >Raadpleeg [Uw code implementeren](deploying-code.md) om het implementatieschema in te stellen of de productie direct uit te voeren.

         * **Het Toezicht**  van CSE van het gebruik - CSE wordt betrokken om de plaatsing daadwerkelijk te beginnen. Tijdens pijpleidingsopstelling of geef uit wanneer CSE Toezicht wordt toegelaten, heeft de Manager van de Plaatsing de optie om te selecteren:

            * **Elke CSE**: verwijst naar elke beschikbare CSE
            * **Mijn CSE**: verwijst naar specifieke CSE die aan de klant of hun steun wordt toegewezen, als CSE uit het bureau is
   1. Stel de **Dispatcher Configurations** voor Productie in. Ga de weg in, selecteer de actie van **Type**, en klik **voeg Weg** toe. U kunt maximaal 100 paden per omgeving opgeven.

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      Als Manager van de Plaatsing, hebt u de kans om een reeks inhoudspaden te vormen die of **ongeldig** of **flushed** van het geheime voorgeheugen van de AEM Dispatcher voor publicatie instanties zullen zijn, terwijl het opzetten of het uitgeven pijpleiding.

      U kunt een afzonderlijke reeks wegen voor de plaatsing van het Stadium en van de Productie vormen. Indien gevormd, zullen deze geheim voorgeheugenacties als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher: invalidate voert een cachevalidatie uit, net als wanneer de inhoud van de auteur wordt geactiveerd om te publiceren. flush voert een geheim voorgeheugenschrapping uit.

      Over het algemeen verdient het de voorkeur de actie voor invalideren te gebruiken, maar er kunnen zich gevallen voordoen waarin flushing vereist is, met name bij gebruik van AEM Client Libraries voor HTML.

      >[!NOTE]
      >
      >Raadpleeg [Overzicht van Dispatcher](dispatcher-configurations.md) voor meer informatie over het in cache plaatsen van Dispatcher.





1. Klik op **Doorgaan** als u alle opties hebt geselecteerd.

1. Selecteer uw opties in de stap **Werkgebiedtests**. U kunt *AEM Sites* en *AEM Assets* het Testen van Prestaties vormen, afhankelijk van welke producten u vergunning hebt gegeven. Raadpleeg [Prestatietests](understand-your-test-results.md#performance-testing) voor meer informatie.

   1. Selecteer uw opties bij **Sites Content Delivery/Distributed Load Weight**. Zie [AEM Sites in Performance Testing](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites) voor meer informatie.

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. Selecteer uw opties bij **Elementprestaties testen Distributie**. Zie [AEM Assets in Performance Testing](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets) voor meer informatie.

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. Klik op **Opslaan** om het toevoegen van een productiepijplijn te voltooien.

### Een productiepijpleiding bewerken {#editing-prod-pipeline}

U kunt de pijpleidingsconfiguraties van de **pagina van het Overzicht van het Programma** uitgeven.

Volg de stappen hieronder om de gevormde pijpleiding uit te geven:

1. Navigeer naar **Pipelines**-kaart van de pagina **Program Overview**.

1. Klik op **..** van **Pipelines** kaart en klik op **Edit**, zoals aangetoond in hieronder figuur.

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. Het dialoogvenster **Productiepijplijn bewerken** wordt weergegeven.

   1. Met het tabblad **Configuratie** kunt u de **Naam van pijpleiding**, **Bewaarplaats**, **Git Branch**, **Implementatiestriger**, **Gedrag van belangrijke metriefout** bijwerken , **Implementatieopties** en **Dispatcher Configurations**.

      >[!NOTE]
      >Zie [Opslagplaatsen toevoegen en beheren](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.


   1. Het **tabblad Werkgebiedtests** biedt u een optie om uw opties opnieuw te selecteren via **Sites Content Delivery/Distributed Load Weight** en **Assets Performance Testing Distribution**.

1. Klik op **Update** zodra u klaar bent met het uitgeven van de pijpleiding.

### Aanvullende acties voor productiepijpleiding {#additional-prod-actions}

#### Een productiepijpleiding uitvoeren {#run-prod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen in werking stellen:

1. Navigeer naar **Pipelines**-kaart van de pagina **Program Overview**.

1. Klik op **..** van **Pipelines** kaart en klik op **Run**, zoals aangetoond in hieronder figuur.

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### Een productiepijpleiding verwijderen {#delete-prod}

U kunt de productiepijpleiding van de kaart van Pijpleidingen schrappen:

1. Navigeer naar **Pipelines**-kaart van de pagina **Program Overview**.

1. Klik op **..** van **Pipelines** kaart en klik op **Delete**, zoals aangetoond in hieronder figuur.

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

## Uitsluitend pijplijnen zonder productie en codekwaliteit

Naast de hoofdpijpleiding die zich naar het stadium en de productie ontwikkelt, kunnen klanten extra pijpleidingen opzetten, die als **Niet-productiepijpleidingen** worden bedoeld. Deze pijpleidingen voeren altijd de bouw en de stappen van de codekwaliteit uit. Ze kunnen optioneel ook worden geïmplementeerd in de omgeving van Adobe Managed Services.

## Videozelfstudie {#video-tutorial-two}

### Uitsluitend pijplijnen voor beheer van wolken zonder productie en kwaliteit van code {#non-prod-video}

CI/CD de niet productiepijpleidingen zijn verdeeld in twee categorieën, de pijpleidingen van de Kwaliteit van de Code, en de pijpleidingen van de Plaatsing. Codekwaliteitpijplijnen zorgen ervoor dat alle code van een Git-vertakking wordt samengesteld en wordt geëvalueerd op basis van de codescanfunctie van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### Een niet-productiepijpleiding toevoegen {#add-non-production-pipeline}

Op het thuisscherm worden deze pijpleidingen op een nieuwe kaart vermeld:

1. Open de **Pipelines**-kaart vanuit het startscherm van Cloud Manager. Klik op **+Add** en selecteer **Niet-productiepijplijn toevoegen**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **De vertoningen van de**  de dialoogdoos van de Pijl van de Niet-Productie toevoegen. Selecteer het type pijplijn dat u wilt maken, **Code Quality Pipeline** of **Deployment Pipeline**.

   Daarnaast kunt u **Implementatietrigger** en **Belangrijk gedrag voor metrische fouten** instellen vanuit **Implementatieopties**. Klik op **Doorgaan**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. De nieuwe niet-productiepijplijn wordt nu weergegeven in de **Pipelines**-kaart.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   De pijpleiding wordt getoond op de kaart op het huisscherm met drie acties, zoals hieronder getoond:

   * **Voeg toe**  - staat het toevoegen van een nieuwe pijpleiding toe.
   * **Toegang tot repo-informatie** : hiermee kan de gebruiker de informatie ophalen die nodig is om toegang te krijgen tot de gegevensopslagruimte van Cloud Manager Git.
   * **Leer meer**  - navigeert aan het begrip van de CI/CD bron van de pijpleidingsdocumentatie.

### Een niet-productiepijplijn bewerken {#editing-nonprod-pipeline}

U kunt de pijpleidingsconfiguraties van **Pipelines kaart** van **Overzicht van het Programma** pagina uitgeven.

Voer de onderstaande stappen uit om de geconfigureerde niet-productiepijplijn te bewerken:

1. Navigeer naar **Pipelines**-kaart van de pagina **Program Overview**.

1. Selecteer de niet-productiepijplijn en klik op **..**. Klik op **Edit**, zoals aangetoond in het hieronder cijfer.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. Het dialoogvenster **Productiepijplijn bewerken** wordt weergegeven waarmee u de **Naam van pijpleiding**, **Opslagplaats**, **Git Branch**, **Activeringstrigger** en **Belangrijk gedrag voor meetgegevens a11/>.**

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >Zie [Opslagplaatsen toevoegen en beheren](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.

   U kunt de volgende plaatsingstrekkers toewijzen om de pijpleiding te beginnen:

   * **Handmatig**  - de UI gebruikt manueel begint de pijpleiding.
   * **Bij de Veranderingen**  van het Git - begint de pijpleiding CI/CD wanneer er toezeggingen aan de gevormde git tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.

   Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitshates wordt ontmoet. Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

   * **Telkens**  vragen - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
   * **Direct**  mislukt - Als deze optie is geselecteerd, wordt de pijplijn geannuleerd wanneer een belangrijke fout optreedt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
   * **Ga onmiddellijk**  verder - als geselecteerd, zal de pijpleiding automatisch te werk wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.


1. Klik op **Update** zodra u klaar bent met het uitgeven van de niet-productiepijplijn.


## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen.

Zie [Uw code implementeren](deploying-code.md) voor meer informatie.
