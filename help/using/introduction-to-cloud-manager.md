---
title: Inleiding tot Cloud Manager
seo-title: Introduction to Cloud Manager
description: 'Deze pagina fungeert als beginpunt voor meer informatie over Cloud Manager. '
seo-description: This page serves as a starting point for learning about Adobe AEM Cloud Manager and highlights the benefits and key features.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
level: Beginner
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 3%

---

# Inleiding tot [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Inleiding tot Cloud Manager"
>abstract="Laat organisaties toe om Experience Manager in de wolk zelf te beheren. Cloud Manager biedt een kader voor doorlopende integratie en levering (CI/CD) waarmee IT-teams en implementatiepartners sneller hun updates en wijzigingen kunnen doorvoeren, zonder verlies in prestaties of veiligheid."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="Programma&#39;s maken"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="Omgevingen maken"

## Inleiding {#introduction}

[!UICONTROL Cloud Manager] voor Adobe Experience Manager biedt ontwikkelaars de mogelijkheid om effectieve klantervaringen te maken via gestroomlijnde workflows, op basis van Adobe Experience Manager best practices. CI/CD pijpleidingen die voor Adobe Experience Manager worden geoptimaliseerd, staan u toe om ontwikkelingswerkschema&#39;s eenvoudig samen te voegen door uw code in te checken en zich helemaal te bewegen aan productie-klaar zijn. Tijdens de bouwstijlfase, worden uw updates van de douanecode grondig getest gebruikend beproefde en geleerde beste praktijken om daadwerkelijke digitale ervaringen voor uw klanten te leveren. Cloud Manager gebruikt een open API-benadering en biedt u de mogelijkheid om uw systemen te integreren zonder bestaande processen en gereedschappen te onderbreken.

In deze documentatiesite worden specifiek de functies en functies beschreven van Cloud Manager voor klanten van Adobe Managed Services (AMS). De equivalente documentatie voor AEM as a Cloud Service klanten is te vinden in de [Uitvoering van aanvragen voor AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html?lang=en).

Met Cloud Manager kan uw ontwikkelingsteam het volgende benutten:

* Continue integratie/doorlopende levering van code om de tijd tot de markt te beperken van maanden/weken tot dagen/uren.

* Code-inspectie, prestatietests en beveiligingsvalidatie op basis van best practices voordat u naar de productie gaat om productieonderbrekingen tot een minimum te beperken.

* API-connectiviteit als aanvulling op bestaande DevOps-processen.

* Met de functie Automatisch schalen wordt op intelligente wijze vastgesteld dat er meer capaciteit nodig is en worden automatisch extra verzend-/publicatiesegmenten online geplaatst.

De volgende afbeelding illustreert de verwerkingsstroom van CI/CD die wordt gebruikt in [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Belangrijke functies in [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Organisaties kunnen gebruikmaken van de volgende functies: [!UICONTROL Cloud Manager]:

### Self-Service Interface {#self-service-interface}

De gebruikersinterface (UI) voor [!UICONTROL Cloud Manager] kunnen klanten eenvoudig toegang krijgen tot de cloudomgeving en de CI/CD-pijplijn voor hun Experience Manager-toepassingen en deze beheren.

Klanten definiëren toepassingsspecifieke KPI&#39;s (Key Performance Indicators) - piekpaginaweergaven per minuut en verwachte responstijd voor een paginabelasting, die uiteindelijk de basis vormen voor het meten van een geslaagde implementatie. Rollen en machtigingen voor verschillende teamleden kunnen eenvoudig worden gedefinieerd. Terwijl de nieuwe zelf-dienst interface de controle in uw handen zet, biedt het ook verbindingen aan beste praktijken en toegang tot deskundigen binnen Adobe die de noodzakelijke begeleiding kunnen verstrekken zoals nodig.

Verkennen en aan de slag gaan met [!UICONTROL Cloud Manager]s UI, zie [Eerste aanmelding](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD Pipet {#ci-cd-pipeline}

Een van de belangrijkste mogelijkheden van [!UICONTROL Cloud Manager] is de mogelijkheid om een geoptimaliseerde CI/CD-pijplijn uit te oefenen om de levering van aangepaste code of updates te versnellen, zoals het toevoegen van nieuwe componenten op de website.

Via de [!UICONTROL Cloud Manager] UI, kunnen de klanten hun CI/CD pijpleiding vormen en schoppen. Tijdens deze pijpleiding, wordt een grondig codescannen uitgevoerd om ervoor te zorgen dat slechts de toepassingen van hoge kwaliteit door aan het productiemilieu overgaan.

Meer leren over het vormen pijpleiding van [!UICONTROL Cloud Manager]s UI, zie de documenten [Productiepijpleidingen configureren](configuring-production-pipelines.md) en [Niet-productiepijpleidingen configureren.](configuring-non-production-pipelines.md)

### Flexibele implementatiemodi {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] biedt klanten flexibele en configureerbare plaatsingswijzen aan zodat kunnen zij ervaringen volgens veranderende bedrijfsvereisten leveren.

Met een automatische trekkerwijze, wordt de code automatisch opgesteld aan een milieu dat op specifieke gebeurtenissen zoals code wordt gebaseerd begaat. U kunt codeplaatsingen tijdens gespecificeerde tijdkaders, zelfs buiten kantooruren ook plannen.

Onafhankelijk van de plaatsingstrekker, worden de kwaliteitscontroles altijd uitgevoerd als deel van CI/CD pijpleidingsuitvoering, telkens als een plaatsing wordt teweeggebracht. De controles van de kwaliteit omvatten, code inspectie, veiligheidstests, en prestaties het testen die uit de doos worden geleverd zonder letterlijk inspanning van klanten of hun partners wordt vereist.

Meer over het opstellen van code en kwaliteitscontroles leren, zie [Uw code implementeren](deploying-code.md)

### Automatisch schalen {#autoscaling}

[!UICONTROL Cloud Manager] detecteert de behoefte aan extra capaciteit wanneer de productieomgeving te kampen heeft met een ongewoon hoge belasting en brengt automatisch extra capaciteit online via autoscaling.

Tijdens een autoscaling-gebeurtenis [!UICONTROL Cloud Manager] activeert automatisch het inrichtingsproces voor automatisch schalen, verzendt een melding van de gebeurtenis voor automatisch schalen en plaatst de extra capaciteit binnen minuten online. De extra capaciteit wordt geleverd in de productieomgeving, in dezelfde regio of regio&#39;s en overeenkomstig dezelfde systeemspecificaties als de actieve Dispatcher/Publish-knooppunten.

De functie voor automatisch schalen is alleen van toepassing op de laag Dispatcher/Publiceren en wordt altijd uitgevoerd met een horizontale schaalmethode, met minimaal één extra segment van een paar Dispatcher/Publish en maximaal tien segmenten. Eventuele extra capaciteit die wordt geleverd, wordt handmatig geschaald binnen een periode van tien werkdagen, zoals bepaald door de CSE (Customer Success Engineer).

>[!NOTE]
>Klanten die willen nagaan of autoscaling geschikt is voor hun toepassing, moeten contact opnemen met hun CSE of Adobe-vertegenwoordiger.
