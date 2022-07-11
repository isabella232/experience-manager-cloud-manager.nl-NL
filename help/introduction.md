---
title: Inleiding tot Cloud Manager voor AMS
description: Begin hier om Cloud Manager voor Adobe Managed Services (AMS) te leren kennen en hoe organisaties Adobe Experience Manager in de cloud kunnen beheren.
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 3%

---


# Inleiding tot [!UICONTROL Cloud Manager] voor AMS {#introduction-to-cloud-manager}

Begin hier om Cloud Manager for Adobe Manage Services (AMS) te leren kennen en hoe organisaties Adobe Experience Manager in de cloud kunnen beheren.

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Inleiding tot Cloud Manager voor AMS"
>abstract="Laat organisaties toe om Adobe Experience Manager in de wolk zelf te beheren. Cloud Manager biedt een kader voor doorlopende integratie en levering (CI/CD) waarmee IT-teams en implementatiepartners sneller hun updates en wijzigingen kunnen doorvoeren, zonder verlies in prestaties of veiligheid."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="Programma&#39;s maken"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="Omgevingen maken"

## Inleiding {#introduction}

[!UICONTROL Cloud Manager] voor Adobe Experience Manager biedt ontwikkelaars de mogelijkheid om effectieve klantervaringen te maken via gestroomlijnde workflows, op basis van Adobe Experience Manager best practices. CI/CD pijpleidingen die voor Adobe Experience Manager worden geoptimaliseerd staan u toe om ontwikkelingswerkschema&#39;s gemakkelijk samen te voegen door uw code eenvoudig te controleren die dan helemaal tot productie-klaar kan bewegen. Tijdens de bouwstijlfase, worden uw updates van de douanecode grondig getest tegen beste praktijken om betrouwbare toepassingen voor uw klanten te leveren. Cloud Manager maakt gebruik van een open API-benadering en biedt u de mogelijkheid om uw systemen te integreren zonder bestaande processen en gereedschappen te onderbreken.

>[!NOTE]
>
>In deze documentatie worden specifiek de functies en functies van Cloud Manager voor Adobe Managed Services (AMS) beschreven.
>
>De equivalente documentatie voor AEM as a Cloud Service is te vinden in de [AEM as a Cloud Service documentatie.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html)

Met Cloud Manager beschikt uw ontwikkelteam over de volgende functies:

* Doorlopende integratie/doorlopende levering (CI/CD) van code om de tijd tot de markt te beperken van maanden/weken tot dagen/uren

* Codeinspectie, prestatietests en beveiligingsvalidatie op basis van best practices voordat u naar de productie gaat om productieonderbrekingen tot een minimum te beperken

* API-connectiviteit als aanvulling op bestaande DevOps-processen

* Autoscaling die intelligent de behoefte aan verhoogde capaciteit ontdekt en automatisch online extra verzenders/het publiceren segmenten brengt

Dit beeld illustreert de CI/CD processtroom die in wordt gebruikt [!UICONTROL Cloud Manager]:

![Cd/cd-stroom](/help/assets/screen_shot_2018-05-12at73843pm.png)

## Belangrijke functies in [!UICONTROL Cloud Manager] {#key-features-in-cloud-manager}

Hieronder vindt u een dieper overzicht van de belangrijkste functies van Cloud Manager.

### Self-Service Interface {#self-service-interface}

De gebruikersinterface (UI) voor [!UICONTROL Cloud Manager] kunt u eenvoudig toegang krijgen tot de cloudomgeving en de CI/CD-pijplijn voor uw Adobe Experience Manager-toepassingen en deze beheren.

U definieert toepassingsspecifieke prestatiekernindicatoren (KPI&#39;s) (zoals piekpaginaweergaven per minuut en verwachte responstijd voor een paginabelasting) die de basis vormen voor het meten van een geslaagde implementatie. Rollen en machtigingen voor verschillende teamleden kunnen eenvoudig worden gedefinieerd. De zelfbedieningsinterface plaatst controle in uw handen, maar het biedt ook verbindingen aan beste praktijkmiddelen en toegang tot deskundigen binnen Adobe aan die de noodzakelijke begeleiding kunnen verstrekken zoals nodig.

Verkennen en aan de slag gaan met [!UICONTROL Cloud Manager]De gebruikersinterface van het document, zie [Eerste aanmelding.](/help/getting-started/first-time-login.md)

### CI/CD Pipet {#ci-cd-pipeline}

Een van de belangrijkste mogelijkheden van [!UICONTROL Cloud Manager] is de mogelijkheid om een geoptimaliseerde CI/CD-pijplijn uit te oefenen om de levering van aangepaste code of updates te versnellen, zoals het toevoegen van nieuwe componenten op de website.

Via de [!UICONTROL Cloud Manager] UI, kunt u uw CI/CD pijpleiding vormen en schoppen. Als deel van deze pijpleiding, wordt een grondig codescannen uitgevoerd om ervoor te zorgen dat slechts de toepassingen van uitstekende kwaliteit door aan het productiemilieu overgaan.

Meer leren over het vormen pijpleiding van [!UICONTROL Cloud Manager]s UI, zie de documenten [Productiepijpleidingen configureren](/help/using/production-pipelines.md) en [Niet-productiepijpleidingen configureren.](/help/using/non-production-pipelines.md)

### Flexibele implementatiemodi {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] biedt flexibele en configureerbare plaatsingswijzen zodat kunt u ervaringen op veranderende bedrijfsvereisten leveren.

Met een automatische trekkerwijze, wordt de code automatisch opgesteld aan een milieu dat op specifieke gebeurtenissen zoals code wordt gebaseerd begaat. U kunt codeplaatsingen tijdens gespecificeerde tijdkaders, zelfs buiten kantooruren ook plannen.

Onafhankelijk van de plaatsingstrekker, worden de kwaliteitscontroles altijd uitgevoerd als deel van CI/CD pijpleiding uitvoering telkens als een plaatsing wordt teweeggebracht. De controles van de kwaliteit omvatten, code inspectie, veiligheidstests, en prestaties het testen, allen die uit de doos zonder inspanning worden geleverd van u of uw partners wordt vereist.

Meer informatie over het opstellen van code en kwaliteitscontroles, zie het document [Code implementeren.](/help/using/code-deployment.md)

### Automatisch schalen {#autoscaling}

wanneer de productieomgeving te kampen heeft met een ongewoon hoge belasting, [!UICONTROL Cloud Manager] detecteert de behoefte aan extra capaciteit en brengt automatisch extra capaciteit online met behulp van de functie voor automatisch schalen.

In dat geval [!UICONTROL Cloud Manager] activeert automatisch het inrichtingsproces voor automatisch schalen, verzendt een melding van de gebeurtenis voor automatisch schalen en plaatst binnen enkele minuten extra capaciteit online. De extra capaciteit wordt geleverd in de productieomgeving, in dezelfde regio of regio&#39;s en overeenkomstig dezelfde systeemspecificaties als de actieve verzender/publicatieknooppunten.

De functie voor automatisch schalen is alleen van toepassing op de verzender/publicatielaag en wordt uitgevoerd met een horizontale schaalmethode, met minimaal één extra segment van een verzender/publicatiepaar tot maximaal tien segmenten. Eventuele extra capaciteit die wordt geleverd, wordt handmatig geschaald binnen een periode van tien werkdagen, zoals bepaald door de CSE (Customer Success Engineer).

>[!NOTE]
>
>Klanten die willen nagaan of autoscaling geschikt is voor hun toepassing, moeten contact opnemen met hun CSE of Adobe-vertegenwoordiger.
