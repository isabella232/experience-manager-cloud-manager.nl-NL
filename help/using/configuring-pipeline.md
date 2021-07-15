---
title: Uw CI/CD-pijplijn configureren
seo-title: Uw CI/CD-pijplijn configureren
description: Volg deze pagina om uw pijpleidingsmontages van de Manager van de Wolk te vormen.
seo-description: 'Voordat u begint met het implementeren van uw code, moet u de pijpleidinginstellingen configureren in AEM Cloud Manager. '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 1c103b1c43a1e5fe7a6fa27110fc692bba6fb8b2
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---

# Uw CI/CD-pijplijn configureren {#configure-your-ci-cd-pipeline}

>[!NOTE]
>Zie [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) voor meer informatie over het configureren van CI/CD Pipeline voor Cloud Manager in AEM als Cloud Service.

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

### Het vormen van de Montages van de Pijpleiding van [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

Zodra u opstelling uw programma gebruikend [!UICONTROL Cloud Manager] UI hebt, bent u klaar om uw pijpleiding te installeren.

Voer de volgende stappen uit om het gedrag en de voorkeuren voor uw pijplijn te configureren:

1. Klik **De Pijpleiding van de Opstelling** om uw pijpleiding te installeren en te vormen.

   ![](assets/Setup-Pipeline.png)

1. De **Setup Pipeline** schermvertoningen.

   Met de wizard in drie stappen kunt u uw **Branch**, **Environment** en **Testing**-omgeving instellen.
Selecteer de Git-vertakking en klik op **Volgende**.

   >[!NOTE]
   >
   >Branches in de Git-opslagplaats zijn gekoppeld aan uw programma.


1. Open het tabblad **Omgevingen** om de opties **Stage** en **Production** te selecteren.

   U kunt de trekker bepalen om de pijpleiding te beginnen:

   * **Bij de Veranderingen**  van het Git - begint de pijpleiding CI/CD wanneer er toezeggingen aan de gevormde git tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.
   * **Handmatig**  - de UI gebruikt manueel begint de pijpleiding.

   Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitscates zoals de Kwaliteit van de Code, het Testen van de Veiligheid, en het Testen van Prestaties wordt ontmoet.

   Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

* **Telkens**  vragen - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
* **Onmiddellijk**  annuleren - Als u deze optie selecteert, wordt de pijplijn geannuleerd wanneer een belangrijke fout optreedt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
* **Onmiddellijk**  goedkeuren - als geselecteerd, zal de pijpleiding automatisch te werk gaan wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.

   Nu definieert u de parameters die de productieimplementatie bepalen. De drie beschikbare opties zijn als volgt:

* **Gebruik Live goedkeuring**  - Een implementatie moet handmatig worden goedgekeurd door een bedrijfseigenaar, projectmanager of implementatiebeheerder via de  [!UICONTROL Cloud Manager] gebruikersinterface.
* **Het Toezicht**  van CSE van het gebruik - CSE wordt betrokken om de plaatsing daadwerkelijk te beginnen. Tijdens pijpleidingsopstelling of geef uit wanneer CSE Toezicht wordt toegelaten, heeft de Manager van de Plaatsing de optie om te selecteren:

   * **Elke CSE**: verwijst naar elke beschikbare CSE
   * **Mijn CSE**: verwijst naar specifieke CSE die aan de klant of hun steun wordt toegewezen, als CSE uit het bureau is

* **Gepland**  - Deze optie staat de gebruiker toe om de geplande productie plaatsing toe te laten.

>[!NOTE]
>Als **Gepland** optie wordt geselecteerd, kunt u uw productiesplaatsing aan de pijpleiding **na** de werkgebiedplaatsing (en **Gebruik GoLive Goedkeuring**, als dat is toegelaten) plannen om op een te plaatsen programma te wachten. De gebruiker kan er ook voor kiezen om de productieimplementatie onmiddellijk uit te voeren.
>
>Raadpleeg [**Uw code implementeren**](deploying-code.md) om het implementatieschema in te stellen of de productie direct uit te voeren.

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>De optie **CSE Oversight** gebruiken is niet beschikbaar voor alle klanten.

**Goedkeuren na implementatie van werkgebied**

Er is een optionele stap **Goedkeuren na implementatie van werkgebied** die kan worden geconfigureerd in de productiepijpleiding.
Dit wordt toegelaten in een nieuwe optie op **Pijpleiding geeft** scherm uit:

![](assets/post_deployment1.png)

Het wordt dan getoond als afzonderlijke stap tijdens pijpleidingsuitvoering:

![](assets/post_deployment2.png)

>[!NOTE]
>
>**Goedkeuren na** implementatie van het werkgebied is vergelijkbaar met de goedkeuringsfuncties vóór de implementatie van de productie, maar vindt direct plaats na de implementatiestap van het werkgebied, dat wil zeggen voordat er tests worden uitgevoerd, in vergelijking met de goedkeuring vóór de implementatie van de productie, die wordt uitgevoerd nadat alle tests zijn voltooid.

**Validatie van verzending**

Als Manager van de Plaatsing, hebt u de kans om een reeks inhoudspaden te vormen die of **ongeldig** of **flushed** van het geheime voorgeheugen van de AEM Dispatcher voor publicatie instanties zullen zijn, terwijl het opzetten of het uitgeven pijpleiding.

U kunt een afzonderlijke reeks wegen voor de plaatsing van het Stadium en van de Productie vormen. Indien gevormd, zullen deze geheim voorgeheugenacties als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher - ongeldig maken voert een cachevalidatie uit, net als wanneer de inhoud van de auteur wordt geactiveerd om te publiceren. flush voert een geheim voorgeheugenschrapping uit.

Over het algemeen verdient het de voorkeur de actie voor invalideren te gebruiken, maar in bepaalde gevallen is leegmaken vereist, met name bij het gebruik van AEM HTML-clientbibliotheken.

>[!NOTE]
>
>Raadpleeg [Overzicht van Dispatcher](dispatcher-configurations.md) voor meer informatie over het in cache plaatsen van Dispatcher.

Voer de onderstaande stappen uit om validaties voor Dispatcher te configureren:

1. Klik **Configureer** onder de kop Configuratie van Dispatcher

   ![](assets/image2018-8-7_14-53-24.png)

1. Ga de weg in, selecteer de actie van **Type**, en klik **Add**. U kunt maximaal 100 paden per omgeving opgeven. Nadat u de paden hebt toegevoegd, klikt u op **Toepassen**.

   ![](assets/image2018-8-7_14-58-11.png)

1. Zodra u op **de pagina van de Montages van de Pijpleiding** bent, zult u een bijgewerkt overzicht van de selecties zien.

   Klik **Save** om deze configuratie voort te zetten.

   ![](assets/image2018-8-7_15-4-30.png)

1. Open het tabblad **Testen** om uw testcriteria voor uw programma te definiëren. U kunt de parameters van de prestatietest nu vormen.

   U kunt *AEM Sites* en *AEM Assets* het Testen van Prestaties vormen, afhankelijk van welke producten u vergunning hebt gegeven. Raadpleeg [Prestatietests](understand-your-test-results.md#performance-testing) voor meer informatie.

1. Klik **sparen** om de opstelling van pijpleidingsproces te voltooien.

   >[!NOTE]
   >Bovendien, zodra u opstelling de pijpleiding hebt, kunt u montages voor het zelfde nog uitgeven gebruikend **de tegel van de Pijpleiding van de Productie** van [!UICONTROL Cloud Manager] UI.

   ![](assets/Production-Pipeline.png)


## Uitsluitend pijplijnen zonder productie en codekwaliteit

Naast de hoofdpijpleiding die zich naar het stadium en de productie ontwikkelt, kunnen klanten extra pijpleidingen opzetten, die als **Niet-productiepijpleidingen** worden bedoeld. Deze pijpleidingen voeren altijd de bouw en de stappen van de codekwaliteit uit. Ze kunnen optioneel ook worden geïmplementeerd in de omgeving van Adobe Managed Services.

## Videozelfstudie {#video-tutorial-two}

### Uitsluitend pijplijnen voor beheer van wolken zonder productie en kwaliteit van code {#non-prod-video}

CI/CD de niet productiepijpleidingen zijn verdeeld in twee categorieën, de pijpleidingen van de Kwaliteit van de Code, en de pijpleidingen van de Plaatsing. Codekwaliteitpijplijnen zorgen ervoor dat alle code van een Git-vertakking wordt samengesteld en wordt geëvalueerd op basis van de codescanfunctie van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

Op het thuisscherm worden deze pijpleidingen op een nieuwe kaart vermeld:

1. Open de tegel **Niet-productiepijpleidingen** vanuit het startscherm van Cloud Manager.

   ![](/help/using/assets/non-prod-add.png)

1. Klik op **Add** knoop, om de Naam van de Pijpleiding, het Type van Pijpleiding, en de Tak van het Git te specificeren.

   Bovendien, kunt u de Trigger van de Plaatsing van de opstelling en Belangrijk Gedrag van de Mislukking van de Opties van de Pijpleiding ook plaatsen.

   ![](assets/non-prod-pipe.png)

1. Klik **sparen** en de pijpleiding wordt getoond op de kaart op het huisscherm met vijf acties:

   * **Bewerken**  - staat het uitgeven van de pijpleidingsmontages toe
   * **Details**  - toont de laatste pijpleidingsuitvoering (als er één is)
   * **Build**  - navigeert aan de uitvoeringspagina, waarvan de pijpleiding kan worden uitgevoerd
   * **Toegang tot repo-informatie** : hiermee kan de gebruiker de informatie ophalen die nodig is om toegang te krijgen tot de gegevensopslagruimte van Cloud Manager
   * **Leer meer**  - navigeert aan het begrip van de CI/CD bron van de pijpleidingsdocumentatie.

      ![](assets/prod-one.png)
   >[!NOTE]
   >
   >Terwijl de pijpleiding loopt, wordt de huidige stap getoond en slechts is de **Details** actie beschikbaar.

## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen.

Zie [Uw code implementeren](deploying-code.md) voor meer informatie.
