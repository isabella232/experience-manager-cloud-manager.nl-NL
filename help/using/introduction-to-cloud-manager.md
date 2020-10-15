---
title: Inleiding tot Cloud Manager
seo-title: Inleiding tot Cloud Manager
description: 'Deze pagina fungeert als beginpunt voor meer informatie over Cloud Manager. '
seo-description: 'Deze pagina dient als uitgangspunt voor het leren over Adobe AEM Cloud Manager en benadrukt de voordelen en belangrijkste functies. '
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: d3f17b1fd4fcc1c75836c9dd67d54e22422db120
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 4%

---


# Introduction to [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## Inleiding {#introduction}

[!UICONTROL Cloud Manager], onderdeel van de Adobe Managed Services, stelt organisaties in staat zelf Experience Manager in de cloud te beheren. Cloud Manager biedt een kader voor doorlopende integratie en levering (CI/CD) waarmee IT-teams en implementatiepartners sneller hun updates en wijzigingen kunnen doorvoeren, zonder verlies in prestaties of veiligheid.

Met behulp van het [!UICONTROL Cloud Manager] zelfbedieningsportaal voor klanten kunnen **organisaties** het volgende uitvoeren/benutten:

* **Continue integratie/doorlopende levering** van code om de tijd tot de markt te beperken van maanden/weken tot dagen/uren.
* **Codeinspectie, prestatietests en beveiligingsvalidatie** op basis van de beste praktijken voordat de productie wordt opgevoerd om productieonderbrekingen tot een minimum te beperken.
* **Automatische, geplande of handmatige implementatie** zelfs buiten kantooruren voor maximale flexibiliteit en controle.
* **De functie Automatisch schalen** detecteert op intelligente wijze de behoefte aan verhoogde capaciteit en brengt automatisch extra verzend-/publicatiesegmenten online.

De volgende afbeelding illustreert de verwerkingsstroom CI/CD die wordt gebruikt in [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Belangrijke functies in [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Organisaties kunnen de volgende functies benutten, met [!UICONTROL Cloud Manager]:

### Self-Service Interface {#self-service-interface}

De gebruikersinterface (UI) voor [!UICONTROL Cloud Manager] stelt klanten in staat om tot het wolkenmilieu en de pijpleiding CI/CD voor hun Experience Manager toepassingen gemakkelijk toegang te hebben en te beheren.

Klanten definiëren toepassingsspecifieke KPI&#39;s (Key Performance Indicators) - piekpaginaweergaven per minuut en verwachte responstijd voor een paginabelasting, die uiteindelijk de basis vormen voor het meten van een geslaagde implementatie. Rollen en machtigingen voor verschillende teamleden kunnen eenvoudig worden gedefinieerd. Terwijl de nieuwe zelf-dienst interface de controle in uw handen zet, biedt het ook verbindingen aan beste praktijken en toegang tot deskundigen binnen Adobe die de noodzakelijke begeleiding kunnen verstrekken zoals nodig.

Om te onderzoeken en begonnen met UI van [!UICONTROL Cloud Manager]s, zie [Eerste Login](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD Pipet {#ci-cd-pipeline}

Een van de belangrijkste mogelijkheden van [!UICONTROL Cloud Manager] is de mogelijkheid om een geoptimaliseerde CI/CD-pijplijn uit te voeren om de levering van aangepaste code of updates te versnellen, zoals het toevoegen van nieuwe componenten op de website.

Via de [!UICONTROL Cloud Manager] UI kunnen klanten hun CI/CD-pijpleiding configureren en afschoppen. Tijdens deze pijpleiding, wordt een grondig codescannen uitgevoerd om ervoor te zorgen dat slechts de toepassingen van hoge kwaliteit door aan het productiemilieu overgaan.

Meer leren over het vormen van pijpleiding van UI van [!UICONTROL Cloud Manager]s, zie [Vorm uw CI/CD Pijpleiding](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html).

### Flexibele implementatiemodi {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] biedt klanten flexibele en configureerbare plaatsingswijzen aan zodat kunnen zij ervaringen volgens veranderende bedrijfsvereisten leveren.

Met een automatische trekkerwijze, wordt de code automatisch opgesteld aan een milieu dat op specifieke gebeurtenissen zoals code wordt gebaseerd begaat. U kunt codeplaatsingen tijdens gespecificeerde tijdkaders, zelfs buiten kantooruren ook plannen.

Onafhankelijk van de plaatsingstrekker, worden de kwaliteitscontroles altijd uitgevoerd als deel van CI/CD pijpleidingsuitvoering, telkens als een plaatsing wordt teweeggebracht. De controles van de kwaliteit omvatten, code inspectie, veiligheidstests, en prestaties het testen die uit de doos worden geleverd zonder letterlijk inspanning van klanten of hun partners wordt vereist.

Meer over het opstellen van code en kwaliteitscontroles leren, zie [opstellen uw Code](deploying-code.md)

### Automatisch schalen {#autoscaling}

[!UICONTROL Cloud Manager] detecteert de behoefte aan extra capaciteit wanneer de productieomgeving te kampen heeft met een ongewoon hoge belasting en brengt automatisch extra capaciteit online via autoscaling.

Tijdens een autoscaling-gebeurtenis wordt het inrichtingsproces voor automatisch schalen [!UICONTROL Cloud Manager] automatisch geactiveerd, wordt een melding van de gebeurtenis voor automatisch schalen verzonden en wordt de extra capaciteit binnen minuten online geplaatst. De extra capaciteit wordt geleverd in de productieomgeving, in dezelfde regio of regio&#39;s en overeenkomstig dezelfde systeemspecificaties als de actieve Dispatcher/Publish-knooppunten.

De functie voor automatisch schalen is alleen van toepassing op de laag Dispatcher/Publiceren en wordt altijd uitgevoerd met een horizontale schaalmethode, met minimaal één extra segment van een paar Dispatcher/Publish en maximaal tien segmenten. Eventuele extra capaciteit die wordt geleverd, wordt handmatig geschaald binnen een periode van tien werkdagen, zoals bepaald door de CSE (Customer Success Engineer).

>[!NOTE]
>Klanten die willen nagaan of autoscaling geschikt is voor hun toepassing, moeten contact opnemen met hun CSE of Adobe-vertegenwoordiger.
