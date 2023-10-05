---
title: Productiepijpleidingen configureren
description: Leer hoe u met Cloud Manager productiepijpleidingen kunt maken en configureren om uw code te implementeren.
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 33ccb0f2139162845cc1b72505b6a5bfc7cf43e7
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---


# Productiepijpleidingen configureren {#configuring-production-pipelines}

Leer hoe u met Cloud Manager productiepijpleidingen kunt maken en configureren om uw code te implementeren. als u eerst een meer conceptueel overzicht wilt van de werking van pijpleidingen in Cloud Manager, raadpleegt u het document [CI/CD Pipelines.](/help/overview/ci-cd-pipelines.md)

## Overzicht {#overview}

Met de **Instellingen Pipet** tegel in [!UICONTROL Cloud Manager] u kunt twee verschillende soorten pijpleidingen tot stand brengen.

* **Productiepijpleidingen** - Een productiepijpleiding is een speciaal gebouwde pijpleiding die bestaat uit een reeks georkestreerde stappen om broncode van uw git-opslagplaats helemaal in productie te nemen.
* **Niet-productiepijpleidingen** - Een niet-productiepijplijn dient vooral om code-kwaliteit scans in werking te stellen of broncode in een ontwikkelomgeving op te stellen.

Dit document richt zich op productiepijpleidingen. Zie het document voor meer informatie over het configureren van niet-productiepijpleidingen [Niet-productiepijpleidingen configureren.](/help/using/non-production-pipelines.md)

De **Implementatiebeheer** de pijpleiding moet worden opgezet . Configuratie van pijpleidingen bestaat uit:

1. Het bepalen van de trekker die de pijpleiding zal beginnen.
1. De parameters definiëren die de productieimplementatie bepalen.
1. De testparameters voor prestaties configureren.

>[!NOTE]
>
>Een pijpleiding kan niet opstelling tot zijn bijbehorende git bewaarplaats minstens één tak heeft en [programma instellen](/help/getting-started/program-setup.md) is voltooid.

## Een nieuwe productiepijpleiding toevoegen {#adding-production-pipeline}

Als u eenmaal de [!UICONTROL Cloud Manager] UI om uw programma op te zetten en minstens één milieu te hebben, bent u bereid om een productiepijplijn toe te voegen.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) en selecteert u de gewenste organisatie en het juiste programma.

1. Ga naar de **Pijpleidingen** kaart van **Programmaoverzicht** pagina en klik op **+Toevoegen** en selecteert u **Productiepijpleiding toevoegen**.

   ![Een productiepijplijn toevoegen](/help/assets/configure-pipelines/add-prod1.png)

1. De **Productiepijpleiding toevoegen** wordt geopend voor **Configuratie** tabblad waar u een aantal opties voor de pijplijn moet definiëren. Deze opties zijn gegroepeerd in inklapbare secties en worden in de volgende stappen beschreven.

   1. Geef een beschrijvende naam op voor uw pijplijn in het dialoogvenster **Naam pijpleiding** veld.

   1. Onder de **Broncode** sectie, bepaalt u waar de pijpleiding de code terugwint het zal verwerken.

      * **Bewaarplaats** - Deze optie bepaalt waarvan git repo de pijpleiding de code zou moeten terugwinnen.

      >[!TIP]
      >
      >Zie het document [Programma instellen](/help/getting-started/program-setup.md) voor meer informatie over het toevoegen en beheren van opslagruimten in Cloud Manager.

      * **Git Branch** - Deze optie bepaalt van welke tak in de geselecteerde pijpleiding de code zou moeten terugwinnen.
      * **Codelocatie** - Deze optie bepaalt de weg in de tak van de geselecteerde repo waarvan de pijpleiding de code zou moeten terugwinnen.

      ![Repo&#39;s voor de pijpleiding definiëren](/help/assets/configure-pipelines/add-prod2.png)

   1. Onder de **Omgevingen** sectie, bepaalt u wat een plaatsing teweegbrengt en hoe het per milieu zou moeten worden uitgevoerd.

      1. In de **WERKGEBIED** sectie, kunt u bepalen hoe de pijpleiding uit aan uw het opvoeren milieu voortkomt.

         * **Implementatieactivering** - U hebt de volgende opties om de plaatsingstrekkers te bepalen om de pijpleiding te beginnen.

            * **Handmatig** - Gebruik deze optie om de pijplijn handmatig te starten met de interface van Cloud Manager.
            * **Wijzigingen in Git** - Deze opties beginnen de pijpleiding CI/CD wanneer de bemoeienis aan de gevormde git tak wordt toegevoegd. Met deze optie, kunt u de pijpleiding nog manueel zoals vereist beginnen.

         * **Belangrijk gedrag metrische fouten** - Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitshates wordt ontmoet. De beschikbare opties zijn:

            * **Telkens vragen** - Dit is de standaardinstelling en u moet handmatig ingrijpen als een belangrijke fout optreedt.
            * **Direct mislukken** - Indien geselecteerd, zal de pijpleiding worden geannuleerd wanneer een belangrijke mislukking voorkomt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
            * **Direct doorgaan** - Indien geselecteerd, zal de pijpleiding automatisch te werk gaan wanneer een belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.

         ![Implementatiemarkering](/help/assets/configure-pipelines/add-prod3.png)

         * **Implementatieopties** - U kunt bepaalde implementatietaken versnellen.

            * **Goedkeuren na implementatie van werkgebied** - Deze goedkeuring vindt plaats na implementatie in de testomgeving voordat er tests worden uitgevoerd. Anders vindt goedkeuring plaats voordat de productie wordt geïmplementeerd, wat gebeurt nadat alle tests zijn voltooid.

            * **Wijzigingen in taakverdeling overslaan** - Er worden geen wijzigingen aangebracht in het taakverdelingsmechanisme.

         ![Implementatieopties stapelen](/help/assets/configure-pipelines/add-prod4.png)

         * **Dispatcher Configuration** - de **Implementatiebeheer** De rol kan een reeks inhoudspaden vormen die of ongeldig of uit het geheime voorgeheugen van de AEM van de Verzender zal worden gespoeld wanneer een pijpleiding in werking wordt gesteld. Deze geheim voorgeheugenacties zullen als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher. Om te vormen:

            1. Onder **PAD** geef een inhoudspad op.
            1. Onder **TYPE** selecteert u de actie die op dat pad moet worden uitgevoerd.

               * **Uitspoelen** - Een cache verwijderen.
               * **Invalidate** - Voer een cachevalidatie uit, net als wanneer inhoud wordt geactiveerd van een ontwerpinstantie naar een publicatieinstantie.

            1. Klikken **Pad toevoegen** om het opgegeven pad toe te voegen. U kunt maximaal 100 paden per omgeving toevoegen.

         ![Dispatcher-configuratie](/help/assets/configure-pipelines/dispatcher-stage.png)

         >[!TIP]
         >
         >Over het algemeen verdient het de voorkeur de actie voor invalideren te gebruiken, maar er kunnen zich gevallen voordoen waarin flushing vereist is, met name bij gebruik van AEM Client Libraries voor HTML.

      1. In de **PRODUCTIE** sectie, kunt u bepalen hoe de pijpleiding uit aan uw productiemilieu voortkomt.

         * **Implementatieopties** - U kunt de parameters bepalen die de productieplaatsing controleren.

            * **Live goedkeuring gebruiken** - Een implementatie moet handmatig worden goedgekeurd door een gebruiker met de **Zakelijke eigenaar**, **Projectmanager**, of **Implementatiebeheer** rol via de [!UICONTROL Cloud Manager] UI.
            * **Gepland** - Met deze optie wordt de pijpleiding vóór de implementatie van de productie gestopt, zodat deze kan worden gepland. Als deze optie wordt geselecteerd, zal de pijpleiding na plaatsing aan het opvoeren milieu stoppen en de gebruiker voor de te nemen actie vragen.
               * **Nu** - Deze optie wordt onmiddellijk ingezet voor productie, waardoor de pijpleiding effectief wordt voltooid.
               * **Datum** - Met deze optie kan de gebruiker een tijdstip plannen waarop de implementatie moet worden voltooid.
               * **Uitvoering stoppen** - Met deze optie wordt de implementatie naar de productie afgebroken.

           >[!TIP]
           >
           >Raadpleeg het document [Implementatie van code](/help/using/code-deployment.md) leren hoe te om het plaatsingsprogramma te plaatsen of de pijpleiding onmiddellijk uit te voeren.

            * **CSE-overzicht gebruiken** - Als deze optie is geselecteerd, wordt een CSE ingeschakeld om de implementatie daadwerkelijk te starten. Wanneer u een pijplijn maakt of bewerkt terwijl deze optie is ingeschakeld, wordt **Implementatiebeheer** De rol heeft de volgende opties.

               * **Elke CSE** - Met deze optie kan elke beschikbare CSE de implementatie starten.
               * **Mijn CSE** - Deze optie staat slechts specifieke CSE toe die aan de klant wordt toegewezen om de plaatsing te beginnen. Dit geldt ook voor de aangewezen back-up van de CSE als de toegewezen CSE niet beschikbaar is.

           ![Implementatieopties voor productie](/help/assets/configure-pipelines/prod-deploymentoptions.png)

         * **Dispatcher Configuration** - Definieer de configuratie van de verzender voor uw productieomgeving. De opties zijn hetzelfde als die voor de testomgeving.

1. Klikken op **Doorgaan** aan de **Werkgebiedtests** tabblad waarop u AEM Sites en AEM Assets Performance Testing kunt configureren, afhankelijk van de producten waarvoor u een licentie hebt.

   >[!TIP]
   >
   >Het document raadplegen [Testen van de codekwaliteit](/help/using/code-quality-testing.md#performance-testing) voor meer informatie over de opties op de **Werkgebiedtests** tab.

   1. Onder de **Sites Content Delivery/Distributed Load Weight** in de sectie, definieert u hoe de prestaties van sites worden getest op basis van de weging van paginaverzoeken tussen de drie paginasets, die kunnen worden in- of uitgeschakeld.

      * **Populaire actieve pagina&#39;s**
      * **Overige actieve pagina&#39;s**
      * **Nieuwe pagina&#39;s**

      ![Belastingsgewicht van sites](/help/assets/configure-pipelines/add-prod5.png)

   1. Onder de **Distributie voor tests op middelenprestaties** definieert u de testverdeling van afbeeldingen en PDF en definieert u uw eigen testelementen.

      * **Afbeeldingen** - Pas de schuifregelaar aan om de testsplitsing tussen afbeeldingen en PDF aan te passen.
      * **PDF** - Pas de schuifregelaar aan om de testsplitsing tussen afbeeldingen en PDF aan te passen.

      * Definieer uw eigen aangepaste elementen door deze te uploaden.

         1. **INDELING** - Bepaal of uw aangepaste element een PDF van een afbeelding is.
         1. **FILENAME** - Gebruik de knop voor de bestandsbrowser om een afbeelding op uw lokale computer te selecteren.
         1. **Testbestand toevoegen** - Klik om uw geselecteerde element te uploaden.

      ![Distributie van middelen testen](/help/assets/configure-pipelines/add-prod6.png)

1. Klikken **Opslaan** om het toevoegen van uw productiepijplijn te voltooien.

## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen. Zie het document [Codeimplementatie](/help/using/code-deployment.md) voor meer informatie .

## Videozelfstudie {#video-tutorial-one}

Deze video biedt een overzicht van het proces voor het maken van pijpleidingen, dat in dit document wordt beschreven.

>[!VIDEO](https://video.tv.adobe.com/v/26314/)
