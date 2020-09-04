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
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 0%

---


# Configure your CI/CD Pipeline {#configure-your-ci-cd-pipeline}

De volgende pagina verklaart hoe te om de **Pijpleiding** te vormen. Om meer conceptuele informatie over te herzien hoe de pijpleiding de [CI/CD pijpleiding overzicht](ci-cd-pipeline.md)ziet.

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
>De pijpleiding kan niet opstelling zijn tot de bewaarplaats van het Git minstens één tak heeft en de Opstelling [van het](setting-up-program.md) Programma volledig is.

Alvorens u begint om uw code op te stellen, moet u uw pijpleidingsmontages van [!UICONTROL Cloud Manager]vormen.

>[!NOTE]
>
>U kunt de pijpleidingsmontages na aanvankelijke opstelling veranderen.

### Het vormen van de Montages van de Pijpleiding van [!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}

Zodra u opstelling uw programma gebruikend [!UICONTROL Cloud Manager] UI hebt, bent u klaar om uw pijpleiding te installeren.

Voer de volgende stappen uit om het gedrag en de voorkeuren voor uw pijplijn te configureren:

1. Klik de Pijpleiding **van de** Opstelling aan opstelling en vorm uw pijpleiding.

   ![](assets/Setup-Pipeline.png)

1. De het schermvertoningen van de Pijpleiding van de **Opstelling** .

   Met de wizard met drie stappen kunt u uw **vertakking**, **omgevingen** en **testomgeving** instellen.
Selecteer de Git-vertakking en klik op **Volgende**.

   >[!NOTE]
   >
   >Branches in de Git-opslagplaats zijn gekoppeld aan uw programma.

   ![](assets/Configure_ci-cd-2.png)


1. Open het tabblad **Omgevingen** om de opties voor **werkgebied** en **productie** te selecteren.

   U kunt de trekker bepalen om de pijpleiding te beginnen:

   * **Bij de Veranderingen** van het Git - begint de pijpleiding CI/CD wanneer er toezeggingen aan de gevormde git tak worden toegevoegd. Zelfs als u deze optie selecteert, kunt u de pijpleiding altijd manueel beginnen.
   * **Handmatig** - de UI gebruikt manueel begint de pijpleiding.

   Tijdens pijpleidingsopstelling of geef uit, heeft de Manager van de Plaatsing de optie om het gedrag van de pijpleiding te bepalen wanneer een belangrijke mislukking in om het even welke kwaliteitscates zoals de Kwaliteit van de Code, het Testen van de Veiligheid, en het Testen van Prestaties wordt ontmoet.

   Dit is handig voor klanten die meer geautomatiseerde processen willen. De beschikbare opties zijn:

* **Telkens** vragen - Dit is de standaardinstelling en u moet handmatig ingrijpen bij elke belangrijke fout.
* **Onmiddellijk** afbreken - Als deze optie is geselecteerd, wordt de pijplijn geannuleerd wanneer een belangrijke fout optreedt. Dit is in feite het emuleren van een gebruiker die elke fout handmatig afwijst.
* **Ga onmiddellijk** verder - als geselecteerd, zal de pijpleiding automatisch te werk wanneer een Belangrijke mislukking voorkomt. Dit emuleert hoofdzakelijk een gebruiker manueel goedkeurend elke mislukking.

   Nu definieert u de parameters die de productieimplementatie bepalen. De drie beschikbare opties zijn als volgt:

* **Gebruik Live goedkeuring** - een implementatie moet handmatig worden goedgekeurd door een bedrijfseigenaar, projectmanager of implementatiebeheerder via de [!UICONTROL Cloud Manager] gebruikersinterface.
* **CSE-overzicht** gebruiken - Een CSE is betrokken om de implementatie daadwerkelijk te starten. Tijdens pijpleidingsopstelling of geef uit wanneer CSE Toezicht wordt toegelaten, heeft de Manager van de Plaatsing de optie om te selecteren:

   * **Elke CSE**: verwijst naar elke beschikbare CSE
   * **Mijn CSE**: verwijst naar specifieke CSE die aan de klant of hun steun wordt toegewezen, als CSE uit het bureau is

* **Gepland** - Deze optie staat de gebruiker toe om de geplande productie plaatsing toe te laten.

>[!NOTE]
>
>Als de **Geplande** optie wordt geselecteerd, kunt u uw productieleiding aan de pijpleiding **na** de werkgebiedplaatsing plannen (en de Goedkeuring **van GoLive van het** Gebruik, als dat) is toegelaten om op een te plaatsen programma te wachten. De gebruiker kan er ook voor kiezen om de productieimplementatie onmiddellijk uit te voeren.
>
>Gelieve te verwijzen naar [**opstellen uw Code**](deploying-code.md), om het plaatsingsprogramma te plaatsen of de productie onmiddellijk uit te voeren.

![](assets/configure-pipeline3.png)

>[!NOTE]
>
>De optie **CSE Oversight** gebruiken is niet beschikbaar voor alle klanten.

**Goedkeuren na implementatie van werkgebied**

Er is een facultatieve stap **goedkeuren na de Plaatsing** van het Stadium die in de Pijpleiding van de Productie kan worden gevormd.
Dit wordt toegelaten in een nieuwe optie op het **Pijpleiding geeft** scherm uit:

![](assets/post_deployment1.png)

Het wordt dan getoond als afzonderlijke stap tijdens pijpleidingsuitvoering:

![](assets/post_deployment2.png)

>[!NOTE]
>
>**Goedkeuren na de implementatie** van het werkgebied werkt net als de goedkeuring vóór de implementatie van de productie, maar vindt plaats onmiddellijk na de implementatiestap van het werkgebied, dat wil zeggen voordat tests worden uitgevoerd, in vergelijking met de goedkeuring vóór de implementatie van de productie, die wordt uitgevoerd nadat alle tests zijn voltooid.

**Validatie van verzending**

Als Manager van de Plaatsing, hebt u de kans om een reeks inhoudspaden te vormen die of **ongeldig** of **gespoeld** van het geheime voorgeheugen van de AEM Dispatcher voor te publiceren instanties zullen zijn, terwijl vestiging of het uitgeven pijpleiding.

U kunt een afzonderlijke reeks wegen voor de plaatsing van het Stadium en van de Productie vormen. Indien gevormd, zullen deze geheim voorgeheugenacties als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld. Deze instellingen gebruiken het standaardgedrag AEM Dispatcher: invalidate voert een cachevalidatie uit, net als wanneer de inhoud van de auteur wordt geactiveerd om te publiceren. flush voert een geheim voorgeheugenschrapping uit.

Over het algemeen verdient het de voorkeur de actie voor invalideren te gebruiken, maar in bepaalde gevallen is leegmaken vereist, met name bij het gebruik van AEM HTML-clientbibliotheken.

>[!NOTE]
>
>Raadpleeg [Overzicht](dispatcher-configurations.md) van verzender voor meer informatie over het in cache plaatsen van verzenders.

Voer de onderstaande stappen uit om validaties voor Dispatcher te configureren:

1. Klik **vormen** onder de rubriek van de Configuratie van de Verzender

   ![](assets/image2018-8-7_14-53-24.png)

1. Voer het pad in, selecteer de actie van **Tekst** en klik op **Toevoegen**. U kunt maximaal 100 paden per omgeving opgeven. Nadat u de paden hebt toegevoegd, klikt u op **Toepassen**.

   ![](assets/image2018-8-7_14-58-11.png)

1. Als u weer op de pagina Instellingen **** pijplijn staat, wordt een bijgewerkte samenvatting van de selecties weergegeven.

   Klik op **Opslaan** om deze configuratie voort te zetten.

   ![](assets/image2018-8-7_15-4-30.png)


1. Open het tabblad **Testen** om de testcriteria voor uw programma te definiëren.

   Nu, kunt u de parameters van de prestatietest vormen.

   U kunt *AEM Sites* en *AEM Assets* Performance Testing configureren, afhankelijk van de producten waarvoor u een licentie hebt.

   **AEM Sites:**

   Cloud Manager voert het testen van de prestaties voor AEM Sites-programma&#39;s uit door pagina&#39;s (als een niet-geverifieerde gebruiker standaard) op de publicatieserver van het werkgebied aan te vragen voor een testperiode van 30 minuten en de responstijd voor elke pagina en verschillende metingen op systeemniveau te meten.

   Vóór het begin van de testperiode van 30 minuten, zal de Manager van de Wolk de milieu van het Stadium kruipen gebruikend een reeks van één of meerdere *zaad* URLs die door de Ingenieur van het Succes van de Klant wordt gevormd. Vanaf deze URL&#39;s wordt de HTML van elke pagina gecontroleerd en worden koppelingen doorlopen op een wijze die begint met het doorlopen van de breedte. Dit schuifproces is beperkt tot maximaal 5000 pagina&#39;s. De verzoeken van de kruipper hebben een vaste onderbreking van 10 seconden.

   Pagina&#39;s worden geselecteerd door drie **paginasets**; u kunt kiezen uit een van de drie sets. De verdeling van verkeer is gebaseerd op het aantal geselecteerde reeksen, dat wil zeggen, als alle drie worden geselecteerd, 33% van de totale paginameningen in de richting van elke reeks wordt gezet; als er twee zijn geselecteerd, gaat 50% naar elke set; als er één wordt geselecteerd , gaat 100 % van het verkeer naar die set .

   Stel bijvoorbeeld dat er een splitsing is van 50%/50% tussen de set Actieve pagina&#39;s populair en Nieuwe pagina&#39;s (in dit voorbeeld wordt Andere actieve pagina&#39;s niet gebruikt) en dat de set Nieuwe pagina&#39;s 3000 pagina&#39;s bevat. De paginaweergaven per minuut KPI is ingesteld op 200. Gedurende de testperiode van 30 minuten:

   * Elk van de 25 pagina&#39;s in de Populaire live paginaset wordt 240 keer - (200 * 0,5) / 25) * 30 = 120

   * Elk van de 3000 pagina&#39;s in de set Nieuwe pagina&#39;s wordt één keer geraakt - (200 * 0,5) / 3000) * 30 = 1

   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   Raadpleeg [Authenticated Performance Testing](#authenticated-performance-testing) voor meer informatie.

   **AEM Assets:**

   Cloud Manager voert de prestatietests voor AEM Assets-programma&#39;s uit door elementen gedurende een testperiode van 30 minuten herhaaldelijk te uploaden en de verwerkingstijd voor elk element en verschillende metingen op systeemniveau te meten. Met deze functie kunt u zowel afbeeldingen als PDF-documenten uploaden. De verdeling van hoeveel activa van elk type per minuut worden geupload wordt geplaatst in de Opstelling of geeft het scherm van de Pijpleiding uit.

   Als bijvoorbeeld een splitsing van 70/30 wordt gebruikt, zoals in de onderstaande afbeelding wordt getoond. Er worden 10 elementen per minuut geüpload, 7 afbeeldingen worden per minuut geüpload en 3 documenten.

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >Er is een standaardafbeelding en PDF-document, maar in de meeste gevallen willen klanten hun eigen elementen uploaden. Dit kan van de Opstelling van de Pijpleiding of het Edit scherm worden gedaan. Algemene afbeeldingsindelingen, zoals JPEG, PNG, GIF en BMP, worden ondersteund in combinatie met Photoshop-, Illustrator- en Postscript-bestanden.

1. Klik **sparen** om de opstelling van pijpleidingsproces te voltooien.

   >[!NOTE]
   >
   >Bovendien, zodra u opstelling de pijpleiding hebt, kunt u montages voor het zelfde nog uitgeven gebruikend de tegel van de Montages **van de Pijpleiding van de** Productie van de [!UICONTROL Cloud Manager] UI.

   ![](assets/Production-Pipeline.png)

### Geverifieerde prestaties testen {#authenticated-performance-testing}

AMS-klanten met geverifieerde sites kunnen een gebruikersnaam en wachtwoord opgeven die door Cloud Manager worden gebruikt voor toegang tot de website tijdens het testen van de Sites-prestaties.

De gebruikersbenaming en het wachtwoord worden gespecificeerd als Variabelen [van de](/help/using/build-environment-details.md#pipeline-variables) Pijpleiding met de namen `CM_PERF_TEST_BASIC_USERNAME` en `CM_PERF_TEST_BASIC_PASSWORD`.

Hoewel niet strikt vereist, wordt het geadviseerd om het type van koordvariabele voor de gebruikersbenaming en het geheimString veranderlijke type voor het wachtwoord te gebruiken. Als beide van deze worden gespecificeerd, zal elk verzoek van de kruipper van de prestatietest en de test virtuele gebruikers deze geloofsbrieven als Basisauthentificatie van HTTP bevatten.

Voer de volgende handelingen uit om deze variabelen in te stellen met de CLI van [Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager):

`$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>`

## Uitsluitend pijplijnen zonder productie en codekwaliteit

Naast de hoofdpijpleiding die zich naar het stadium en de productie ontwikkelt, kunnen klanten extra pijpleidingen opzetten, die **niet-productiepijpleidingen** worden genoemd. Deze pijpleidingen voeren altijd de bouw en de stappen van de codekwaliteit uit. Ze kunnen optioneel ook worden geïmplementeerd in de omgeving van Adobe Managed Services.

## Videozelfstudie {#video-tutorial-two}

### Uitsluitend pijplijnen voor beheer van wolken zonder productie en kwaliteit van code {#non-prod-video}

CI/CD de niet productiepijpleidingen zijn verdeeld in twee categorieën, de pijpleidingen van de Kwaliteit van de Code, en de pijpleidingen van de Plaatsing. Codekwaliteitpijplijnen zorgen ervoor dat alle code van een Git-vertakking wordt samengesteld en wordt geëvalueerd op basis van de codescanfunctie van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

Op het thuisscherm worden deze pijpleidingen op een nieuwe kaart vermeld:

1. Open de tegel **Niet-productiepijplijnen** vanuit het startscherm van Cloud Manager.

   ![](assets/Non-Production-Pipeline.png)

1. Klik op de knop Toevoegen om de naam van de pijplijn, het type pijplijn en de tak van de it op te geven.

   Bovendien, kunt u de Trigger van de Plaatsing van de opstelling en Belangrijk Gedrag van de Mislukking van de Opties van de Pijpleiding ook plaatsen.

   ![](assets/non-prod-pipe.png)

1. Klik **sparen** en de pijpleiding wordt getoond op de kaart op het huisscherm met drie acties:

   * **Bewerken** - hiermee kunt u de pijpleidinginstellingen bewerken
   * **Detail** - toont de laatste pijpleidingsuitvoering (als er één is)
   * **Build** - navigeert aan de uitvoeringspagina, waarvan de pijpleiding kan worden uitgevoerd

   ![](assets/Non-prod-2.png)

   >[!NOTE]
   >
   >Terwijl de pijpleiding loopt, wordt de huidige stap getoond en slechts is de actie van **Details** beschikbaar.

## De volgende stappen {#the-next-steps}

Zodra u de pijpleiding hebt gevormd, moet u uw code opstellen.

Zie [Uw code](deploying-code.md) implementeren voor meer informatie.
