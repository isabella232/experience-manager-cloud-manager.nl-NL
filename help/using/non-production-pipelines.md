---
title: Niet-productiepijpleidingen configureren
description: Leer hoe u met Cloud Manager niet-productiepijpleidingen kunt maken en configureren om uw code te implementeren.
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 33ccb0f2139162845cc1b72505b6a5bfc7cf43e7
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Niet-productiepijpleidingen configureren {#configuring-non-production-pipelines}

Leer hoe u met Cloud Manager niet-productiepijpleidingen kunt maken en configureren om uw code te implementeren. Als u eerst een meer conceptueel overzicht wilt van de werking van pijpleidingen in Cloud Manager, raadpleegt u het document [CI/CD Pipelines.](/help/overview/ci-cd-pipelines.md)

## Overzicht {#overview}

Met de **Pijpleidingen** tegel in [!UICONTROL Cloud Manager]de **Implementatiebeheer** U kunt twee verschillende soorten pijpleidingen maken.

* **Productiepijpleidingen** - Een productiepijpleiding is een doelgerichte pijpleiding die bestaat uit een reeks georkestreerde stappen om de broncode helemaal in productie te nemen.
* **Niet-productiepijpleidingen** - Een niet-productiepijplijn dient vooral om code-kwaliteit scans in werking te stellen of broncode in een ontwikkelomgeving op te stellen.

Dit document richt zich op niet-productiepijpleidingen. Zie het document voor meer informatie over het configureren van productiepijpleidingen [Productiepijpleidingen configureren.](/help/using/production-pipelines.md)

Er zijn twee soorten niet-productiepijpleidingen:

* **Codekwaliteitspijplijnen** - Deze looppas codekwaliteit scant op de code in een git tak en voert de bouw en de stappen van de codekwaliteit uit.
* **Implementatiepijpleidingen** - Naast het uitvoeren van de bouw en de stappen van de codekwaliteit zoals de pijpleidingen van de codekwaliteit, stellen deze pijpleidingen de code in een non-production milieu op.

>[!NOTE]
>
>Een pijpleiding kan niet opstelling tot zijn bijbehorende git bewaarplaats minstens één tak heeft en [programma instellen](/help/getting-started/program-setup.md) is voltooid. Zie het document [Opslagplaatsen voor Cloud Manager](/help/managing-code/repositories.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.

## Een niet-productiepijpleiding toevoegen {#add-non-production-pipeline}

Nadat u uw programma hebt ingesteld en minstens één omgeving hebt gebruikt met de interface van Cloud Manager, kunt u een niet-productiepijplijn toevoegen door deze stappen uit te voeren.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie en het juiste programma.

1. Open de Pipelines-kaart vanuit het hoofdscherm van Cloud Manager. Klikken op **Toevoegen** en selecteert u **Niet-productiepijpleiding toevoegen**.

   ![Niet-productiepijpleiding toevoegen](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. Op de **Configuratie** tabblad van het **Niet-productiepijpleiding toevoegen** selecteert u het type pijplijn dat u wilt maken, of een **Codekwaliteit, pijplijn** of **Implementatiepijp**.

   ![Type pijpleiding kiezen](/help/assets/configure-pipelines/add-non-production-pipeline.png)

1. Geef een beschrijving voor de pijplijn in het dialoogvenster **Naam niet-productiepijpleiding** veld.

1. Als u ervoor kiest een **Implementatiepijp**, selecteert u de doelimplementatieomgeving in de **In aanmerking komende implementatieomgevingen** vervolgkeuzelijst.

1. Verstrek de bewaarplaats waar de pijpleiding de code zou moeten terugwinnen.

   * **Bewaarplaats** - Deze opties bepalen waarvan git de pijpleiding de code zou moeten terugwinnen.
   * **Git Branch** - Deze optie bepaalt van welke tak in de geselecteerde pijpleiding de code zou moeten terugwinnen.

1. Definieer uw implementatieopties.

   1. Onder **Implementatieactivering**, bepaalt welke gebeurtenis de pijpleiding activeert.

      * **Handmatig** - Gebruik deze optie om de pijpleiding manueel te beginnen.
      * **Wijzigingen in Git** - Deze opties beginnen de pijpleiding wanneer de verbintenissen aan de gevormde git tak worden toegevoegd. Met deze optie, kunt u de pijpleiding nog manueel zoals vereist beginnen.

   1. Voor uitzettingspijpleidingen, onder **Belangrijk gedrag metrische fouten**, definieert u het gedrag van de pijpleiding wanneer een belangrijke fout optreedt in een van de kwaliteitspoorten.

      * **Telkens vragen** - Dit is de standaardinstelling en u moet handmatig ingrijpen als een belangrijke fout optreedt.
      * **Direct mislukken** - Indien geselecteerd, zal de pijpleiding worden geannuleerd wanneer een belangrijke mislukking voorkomt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
      * **Direct doorgaan** - Indien geselecteerd, zal de pijpleiding automatisch te werk gaan wanneer een belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.

   1. **Dispatcher Configuration** - de **Implementatiebeheer** De rol kan een reeks inhoudspaden vormen die of ongeldig of uit het geheime voorgeheugen van de AEM van de Verzender zal worden gespoeld wanneer een pijpleiding in werking wordt gesteld. Deze geheim voorgeheugenacties zullen als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher. Om te vormen:

      1. Onder **PAD** geef een inhoudspad op.
      1. Onder **TYPE** selecteert u de actie die op dat pad moet worden uitgevoerd.

         * **Uitspoelen** - Een cache verwijderen.
         * **Invalidate** - Voer een cachevalidatie uit, net als wanneer inhoud wordt geactiveerd van een ontwerpinstantie naar een publicatieinstantie.
      1. Klikken **Pad toevoegen** om het opgegeven pad toe te voegen. U kunt maximaal 100 paden per omgeving toevoegen.

1. Klikken **Opslaan** om uw pijpleiding te redden.

## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen. Zie het document [Codeimplementatie](/help/using/code-deployment.md) voor meer informatie .

## Videozelfstudie {#video-tutorial}

Deze video biedt een overzicht van het proces voor het maken van pijpleidingen, dat in dit document wordt beschreven.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)
