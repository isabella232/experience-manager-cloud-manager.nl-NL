---
title: Op rollen gebaseerde machtigingen
description: Volg deze pagina voor meer informatie over Op rol gebaseerde machtigingen.
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: User Roles
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 15%

---


# Op rollen gebaseerde machtigingen {#role-based-permissions}

[!UICONTROL Cloud Manager] heeft pre-gevormde rollen met aangewezen toestemmingen. Een ontwikkelaar ontwikkelt bijvoorbeeld code en heeft de toestemming om de code naar **Git Repository** te duwen. Alternatief, heeft een bedrijfseigenaar verschillende toestemmingen die hen toestaan om de Zeer belangrijke Indicatoren van Prestaties (KPIs) te bepalen en plaatsingen goed te keuren.

## Gebruikersrollen {#user-roles}

Rolbeheer voor [!UICONTROL Cloud Manager] wordt uitgevoerd in [Adobe Admin Console](https://helpx.adobe.com/nl/enterprise/using/admin-console.html). Elke gebruiker van [!UICONTROL Cloud Manager] moet lid zijn van de IMS-organisatie van de klant en over de Adobe Managed Services-productcontext beschikken. De specifieke rollidmaatschappen worden verstrekt door de gebruiker aan een [!UICONTROL Cloud Manager] Profiel van het Product in de Admin Console toe te voegen.

Meer over hoe te om uw rollen te plaatsen zie [De Gebruikers en Rollen van de vestiging](setting-up-users-and-roles.md).

De volgende lijst bepaalt de mogelijke rollen u in de Admin Console kunt toewijzen.

| **[!UICONTROL Cloud Manager]Rol** | **Beschrijving** |
|---|---|
| Business Owner | Primaire gebruiker die de eerste [!UICONTROL Cloud Manager]-installatie heeft voltooid. Verantwoordelijk voor het bepalen van KPIs, het goedkeuren van productieplaatsingen en het met voeten treden van belangrijke 3-tier mislukkingen. |
| Program Manager | Gebruikt [!UICONTROL Cloud Manager] om teamopstelling uit te voeren, status te herzien en KPIs te bekijken. Kan belangrijke drie-titers fouten goedkeuren. |
| Deployment Manager | Beheert de implementatiebewerkingen. Gebruikt [!UICONTROL Cloud Manager] om werkgebied en productieplaatsingen uit te voeren. Kan belangrijke drie-titers fouten goedkeuren. Heeft toegang tot Git-opslagplaats. |
| Developer | Ontwikkelt en test aangepaste toepassingscode. Gebruikt hoofdzakelijk [!UICONTROL Cloud Manager] om status te bekijken. Heeft toegang tot Git-opslagplaats vastgelegd. |
| Klantsuccesvolle technicus | Over het algemeen ondersteunt het succes van klanten met AMS. Interactie met [!UICONTROL Cloud Manager] voor het uitvoeren van implementaties die toezicht van de Klant vereisen van de Ingenieur van het Succes van de Klant (CSE). |
| Inhoudsauteur | Doorgaans heeft dit geen invloed op [!UICONTROL Cloud Manager]. Deze gebruiker kan [!UICONTROL Cloud Manager] de Schakelaar van het Programma gebruiken (die van [!UICONTROL Experience Cloud]) is genavigeerd om tot Adobe Experience Manager (AEM) toegang te hebben. |

## Gebruikersmachtigingen {#user-permissions}

Elk van de rollen heeft specifieke toestemmingen, vooraf geconfigureerde taken, of toestemmingen, verbonden aan elke rol. Deze lijst maakt een lijst van de beschikbare functies en de rollen die de functie kunnen uitvoeren.

Zie [Gebruikers en rollen instellen](setting-up-users-and-roles.md) voor meer informatie over het instellen van uw gebruikers.

| Machtiging | Beschrijving | Zakelijke eigenaar | Implementatiebeheer | Programmabeheerder | Ontwikkelaar | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| Toepassing lezen | Lees Programma-KPI&#39;s. | x | x | x | x | x |
| Toepassing schrijven | Programma instellen of bewerken. | x |  |  |  |  |
| Programma toevoegen | Nieuw programma toevoegen. | x |  |  |  |  |
| Leesomgeving | Zie Omgevingsdetails. | x | x | x | x | x |
| Uitvoering maken | Start Pipeline. | x | x | x |  |  |
| Uitvoering lezen | Zie uitvoeringsstatus. | x | x | x | x | x |
| Uitvoering hervatten | Kan uitvoering hervatten wanneer gepauzeerd. | x | x | x |  | x |
| Implementatie Goedkeuren Distributie naar productie | Geef GoLive-goedkeuring op. | x | x | x |  |  |
| Implementatieschema Distribueren naar productie | Plan de Implementatie van de Productie. | x | x | x |  | x |
| Implementatie Distribueren naar productie | Implementeer de toepassing op productie wanneer deze voor CSE-toezicht wordt gepauzeerd. |  |  |  |  | x |
| Uitvoering annuleren | Huidige uitvoering annuleren. |  |  | x |  |  |
| Uitvoering heeft kwaliteitsfouten genegeerd | Belangrijke kwaliteitsfouten goedkeuren. | x | x | x |  |  |
| Pipet maken | Setup/Edit Pipeline. |  | x |  |  |  |
| Pipet gelezen | Zie details pijpleiding. | x | x | x | x | x |
| Pipet schrijven | Setup/Edit Pipeline. |  | x |  |  |  |
| Goedkeuring pijpleiding wijzigen | Hiermee kunt u de optie Bedrijfseigenaar bewerken. |  | x |  |  |  |
| De pijpleiding wijzigt Beheerde Plaatsing | Hiermee kunt u de optie CSE Oversight bewerken. |  | x |  |  |  |
| Pipet verwijderen | Staat het schrappen van een Pijpleiding toe. |  | x |  |  |  |
| Stap lezen | Zie de resultaten van metrische gegevens voor de stapkwaliteit. | x | x | x | x | x |
| Token voor persoonlijke toegang genereren | Toegangspoort. |  | x |  | x |  |

