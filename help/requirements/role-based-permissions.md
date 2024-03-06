---
title: Op rollen gebaseerde machtigingen
description: Meer informatie over de vooraf geconfigureerde, op rollen gebaseerde machtigingen van Cloud Manager voor het beheren van toegang tot uw cloudbronnen.
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 10297789ac8f905f242ac52bdc6fc4812b989e8a
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---


# Op rollen gebaseerde machtigingen {#role-based-permissions}

[!UICONTROL Cloud Manager] heeft pre-gevormde rollen met aangewezen toestemmingen. Een ontwikkelaar ontwikkelt bijvoorbeeld code en heeft de toestemming om de code door te sturen naar de git-opslagplaats. Een bedrijfseigenaar heeft verschillende toestemmingen die hen toestaan om de belangrijkste prestatiesindicatoren (KPIs) te bepalen en plaatsingen goed te keuren.

>[!NOTE]
>
>In deze documentatie worden op rollen gebaseerde machtigingen voor Cloud Manager for Adobe Managed Services (AMS) beschreven.
>
>De equivalente documentatie voor AEM as a Cloud Service vindt u in het document [Inleiding tot Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/concepts/cloud-manager-introduction.html#role-based-permissions) in de AEM as a Cloud Service documentatie.

## Gebruikersrollen {#user-roles}

Rolbeheer voor [!UICONTROL Cloud Manager] wordt uitgevoerd met de [Admin Console.](https://helpx.adobe.com/nl/enterprise/using/admin-console.html) Elke gebruiker van [!UICONTROL Cloud Manager] moet lid zijn van de IMS-organisatie van de klant en de Adobe Managed Services Product Context hebben. Specifieke rollidmaatschappen worden verstrekt door de gebruiker aan een [!UICONTROL Cloud Manager] productprofiel in de Admin Console.

Meer informatie over hoe te om uw rollen te plaatsen zie het document [Gebruikers en rollen instellen.](/help/requirements/users-and-roles.md)

Deze lijst maakt een lijst van de rollen u in de Admin Console kunt toewijzen.

| [!UICONTROL Cloud Manager] Rol | Beschrijving |
|---|---|
| Business Owner | Dit is de primaire gebruiker die de eerste [!UICONTROL Cloud Manager] De opstelling en is verantwoordelijk voor het bepalen van KPIs, het goedkeuren van productieplaatsingen, en het met voeten treden van belangrijke 3-tier mislukkingen wanneer noodzakelijk. |
| Program Manager | Deze gebruiker gebruikt [!UICONTROL Cloud Manager] om teamopstelling uit te voeren, revisiestatus, KPIs te bekijken, en kan belangrijke 3 rijmislukkingen goedkeuren wanneer noodzakelijk. |
| Deployment Manager | Deze gebruiker beheert de implementatiebewerkingen met [!UICONTROL Cloud Manager] om fase en productieplaatsingen uit te voeren, kan belangrijke drie-laag mislukkingen goedkeuren wanneer nodig, en heeft toegang tot de git bewaarplaats. |
| Developer | Deze gebruiker ontwikkelt en test de code van de douanetoepassing, hoofdzakelijk gebruik [!UICONTROL Cloud Manager] om plaatsingsstatus te bekijken, en toegang tot de git bewaarplaats te begaan. |
| Klantsuccesvolle technicus | Deze gebruiker steunt over het algemeen klantensucces voor klanten AMS en wisselt met [!UICONTROL Cloud Manager] voor het uitvoeren van implementaties waarvoor toezicht van de Klant vereist is. |
| Inhoudsauteur | Deze gebruiker communiceert doorgaans niet met [!UICONTROL Cloud Manager], maar kan de [!UICONTROL Cloud Manager] programma wwitcher (navigeer van [!UICONTROL Experience Cloud]) voor toegang tot Adobe Experience Manager (AEM). |

## Gebruikersmachtigingen {#user-permissions}

Elk van de rollen heeft specifieke bijbehorende preconfigured toestemmingen. Deze lijst maakt een lijst van de beschikbare toestemmingen en de rollen die hen kunnen uitvoeren.


| Machtiging | Beschrijving | Business Owner | Deployment Manager | Program Manager | Developer | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| Toepassing lezen | KPI&#39;s van programma lezen | x | x | x | x | x |
| Toepassing schrijven | Programma instellen of bewerken | x |  |  |  |  |
| Programma toevoegen | Nieuw programma toevoegen | x |  |  |  |  |
| Leesomgeving | Zie omgevingsdetails | x | x | x | x | x |
| Uitvoering maken | Pijpleiding starten | x | x | x |  |  |
| Uitvoering lezen | Zie uitvoeringsstatus | x | x | x | x | x |
| Uitvoering hervatten | Kan uitvoering hervatten wanneer gepauzeerd | x | x | x |  | x |
| Implementatie Goedkeuren Distributie naar productie | Live goedkeuring bieden | x | x | x |  |  |
| Implementatieschema Distribueren naar productie | Implementatie van productieplanning | x | x | x |  | x |
| Implementatie Distribueren naar productie | Toepassing implementeren op productie wanneer gepauzeerd voor CSE-toezicht |  |  |  |  | x |
| Uitvoering annuleren | Huidige uitvoering annuleren |  |  | x |  |  |
| Uitvoering heeft kwaliteitsfouten genegeerd | Belangrijke kwaliteitsgate-fouten goedkeuren | x | x | x |  |  |
| Pipet maken | Gasleiding instellen/bewerken |  | x |  |  |  |
| Pipet gelezen | Zie details over pijpleidingen | x | x | x | x | x |
| Pipet schrijven | Opstelling/geeft pijpleiding uit. |  | x |  |  |  |
| Goedkeuring pijpleiding wijzigen | Hiermee kunt u de optie Bedrijfseigenaar bewerken |  | x |  |  |  |
| Door pijplijn beheerde implementatie wijzigen | Staat het uitgeven van de CSE toezichtoptie toe |  | x |  |  |  |
| Pipet verwijderen | Staat pijpleiding toe schrapping |  | x |  |  |  |
| Stap lezen | Zie de resultaten van de metrische gegevens voor de stapkwaliteit | x | x | x | x | x |
| Token voor persoonlijke toegang genereren | Toegangsuitrusting |  | x |  | x |  |

Raadpleeg het document voor meer informatie over het instellen van uw gebruikers [Gebruikers en rollen instellen.](/help/requirements/users-and-roles.md)
