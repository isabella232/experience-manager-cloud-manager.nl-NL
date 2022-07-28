---
title: Inleiding tot Cloud Manager voor AMS
description: Begin hier om Cloud Manager voor Adobe Managed Services (AMS) te leren kennen en hoe organisaties Adobe Experience Manager in de cloud kunnen beheren.
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 14e35882765783b234ca35da14257279af5130a0
workflow-type: tm+mt
source-wordcount: '1287'
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
>De equivalente documentatie voor AEM as a Cloud Service is te vinden in de [AEM as a Cloud Service documentatie.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/home.html)

Met Cloud Manager beschikt uw ontwikkelteam over de volgende functies:

* Doorlopende integratie/doorlopende levering (CI/CD) van code om de tijd tot de markt te beperken van maanden/weken tot dagen/uren

* Codeinspectie, prestatietests en beveiligingsvalidatie op basis van best practices voordat u naar de productie gaat om productieonderbrekingen tot een minimum te beperken

* API-connectiviteit als aanvulling op bestaande DevOps-processen

* Autoscaling die intelligent de behoefte aan verhoogde capaciteit ontdekt en automatisch extra Verzender/het publiceren segmenten online brengt

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

## Optionele functies in Cloud Manager {#optional-features-in-cloud-manager}

Cloud Manager biedt extra, geavanceerde functies die gunstig kunnen zijn voor uw project, afhankelijk van de instellingen en behoeften van uw specifieke omgeving. Als deze functies u interesseren, kunt u contact opnemen met uw Customer Success Engineer (CSE) of Adobe-medewerker om verder te bespreken.

### Automatisch schalen {#autoscaling}

Wanneer de productieomgeving aan ongewoon hoge belasting onderhevig is, [!UICONTROL Cloud Manager] detecteert de behoefte aan extra capaciteit en brengt automatisch extra capaciteit online met behulp van de functie voor automatisch schalen.

In dat geval [!UICONTROL Cloud Manager] activeert automatisch het inrichtingsproces voor automatisch schalen, verzendt een melding van de gebeurtenis voor automatisch schalen en plaatst binnen enkele minuten extra capaciteit online. De extra capaciteit wordt geleverd in de productieomgeving, in dezelfde regio of regio&#39;s en overeenkomstig dezelfde systeemspecificaties als de actieve Dispatcher/publishing-knooppunten.

De functie voor automatisch schalen is alleen van toepassing op de laag Dispatcher/publishing en wordt uitgevoerd met een horizontale schaalmethode, met minimaal één extra segment van een paar Dispatcher/publishing tot maximaal tien segmenten. Eventuele extra capaciteit die wordt geleverd, wordt handmatig geschaald binnen een periode van tien werkdagen, zoals bepaald door de CSE (Customer Success Engineer).

>[!NOTE]
>
>Neem contact op met uw CSE of Adobe als u graag wilt weten of automatische schaling geschikt is voor uw toepassing.

### Blauwe/groene implementaties {#blue-green}

Blauwe/groene implementatie is een techniek die downtime en risico&#39;s vermindert door twee identieke productieomgevingen uit te voeren, die blauw en groen worden genoemd.

Op elk ogenblik, is slechts één van de milieu&#39;s levend, met het levende milieu dat al productieverkeer dient. Over het algemeen is blauw de huidige live omgeving en groen is inactief.

* Blauwe/groene implementatie is een add-on bij Ci/cd-pijpleidingen van Cloud Manager waarin een tweede set groene publicatie- en Dispatcher-instanties wordt gemaakt en gebruikt voor implementaties. De groene instanties worden vervolgens gekoppeld aan het taakverdelingsmechanisme voor de productie en de oude (blauwe) exemplaren worden verwijderd en beëindigd.
* Deze implementatie van blauw/groen behandelt instanties als voorbijgaand en elke herhaling van een blauwe/groene pijpleiding zal tot een nieuwe reeks publiceren en servers van de Verzender leiden.
* Als onderdeel van de installatie wordt een groene taakverdelingsmechanisme gemaakt. Dit taakverdelingsmechanisme wordt nooit gewijzigd en verwijst naar de groene of &quot;test&quot;-URL.
* Tijdens een blauwe/groene implementatie wordt een exacte replica van de bestaande publicatie-/Dispatcher-lagen gemaakt.

#### Blauwe/groene implementatiestroom {#flow}

Wanneer de blauwe/groene plaatsing wordt toegelaten, verschilt de plaatsingsstroom van de standaard Cloud Service plaatsingsstroom.

| Stap | Blauwe/groene implementatie | Standaardimplementatie |
|---|---|---|
| 1 | Implementatie aan auteur | Implementatie aan auteur |
| 2 | Onderbreken voor testen | - |
| 3 | Groene infrastructuur wordt gemaakt | - |
| 4 | Implementatie in groene publicatie-/verzendingslagen | Implementatie aan uitgever |
| 5 | Onderbreken voor testen (maximaal 24 uur) | - |
| 6 | Groene infrastructuur wordt toegevoegd aan het taakverdelingsmechanisme voor productie | - |
| 7 | Blauwe infrastructuur wordt verwijderd uit het productielast-taakverdelingsmechanisme- |
| 8 | Blauwe infrastructuur wordt automatisch beëindigd | - |

#### Blauw/groen implementeren {#implementing}

Alle AMS-gebruikers die Cloud Manager gebruiken voor productieimplementaties, kunnen gebruikmaken van een blauwe/groene implementatie. Het gebruik van een blauw/groene implementatie vereist echter extra validatie van uw omgevingen en installatie door een Adobe-CSE.

Als u in blauwe/groene plaatsing geinteresseerd bent, te overwegen gelieve de volgende vereisten en beperkingen en uw CSE te contacteren.

#### Eisen en beperkingen {#limitations}

* Blauw/groen is alleen beschikbaar voor publicatie/verzender-paren.
* De paren van de Verzending van de voorproef/publiceren maken geen deel uit van blauwe/groene plaatsingen.
* Elk paar Dispatcher/publish is gelijk aan elk ander paar Dispatcher/publish.
* Blauw/groen is alleen beschikbaar in de productieomgeving.
* Blauw/groen is zowel beschikbaar in AWS als in Azure.
* Blauw/groen is niet alleen beschikbaar voor klanten met middelen.
