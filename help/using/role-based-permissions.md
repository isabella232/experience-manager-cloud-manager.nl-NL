---
title: Op rollen gebaseerde machtigingen
description: Volg deze pagina voor meer informatie over Op rol gebaseerde machtigingen.
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
translation-type: tm+mt
source-git-commit: 9cbe8f58cf04001ba9851ba321f03c7687e58014

---


# Op rollen gebaseerde machtigingen {#role-based-permissions}

[!UICONTROL Cloud Manager] heeft pre-gevormde rollen met aangewezen toestemmingen. Een ontwikkelaar ontwikkelt bijvoorbeeld code en heeft de toestemming om de code naar de **Git Repository** te duwen. Alternatief, heeft een bedrijfseigenaar verschillende toestemmingen die hen toestaan om de Zeer belangrijke Indicatoren van Prestaties (KPIs) te bepalen en plaatsingen goed te keuren.

## Gebruikersrollen {#user-roles}

Rolbeheer voor [!UICONTROL Cloud Manager] wordt uitgevoerd in de [Adobe Admin Console](https://helpx.adobe.com/nl/enterprise/using/admin-console.html). Elke gebruiker van [!UICONTROL Cloud Manager] moet lid zijn van de IMS-organisatie van de klant en over de Adobe Managed Services-productcontext beschikken. Specifieke rollidmaatschappen worden verstrekt door de gebruiker aan een Profiel van het [!UICONTROL Cloud Manager] Product in de Console Admin toe te voegen.

Meer over hoe te om uw rollen te plaatsen zie de Gebruikers en de Rollen van de [Opstelling](setting-up-users-and-roles.md).

In de volgende tabel worden de mogelijke rollen gedefinieerd die u in de beheerconsole kunt toewijzen.

| **[!UICONTROL Cloud Manager]Rol ** | **Beschrijving** |
|---|---|
| Business Owner | Primaire gebruiker die de eerste [!UICONTROL Cloud Manager] installatie heeft voltooid. Verantwoordelijk voor het bepalen van KPIs, het goedkeuren van productieplaatsingen en het met voeten treden van belangrijke 3-tier mislukkingen. |
| Program Manager | Gebruikt [!UICONTROL Cloud Manager] om teamopstelling uit te voeren, status te herzien en KPIs te bekijken. Kan belangrijke drie-titers fouten goedkeuren. |
| Deployment Manager | Beheert de implementatiebewerkingen. Gebruikt [!UICONTROL Cloud Manager] om werkgebied en productieplaatsingen uit te voeren. Kan belangrijke drie-titers fouten goedkeuren. Heeft toegang tot Git-opslagplaats. |
| Developer | Ontwikkelt en test aangepaste toepassingscode. Wordt voornamelijk gebruikt [!UICONTROL Cloud Manager] om de status weer te geven. Heeft toegang tot Git-opslagplaats vastgelegd. |
| Klantsuccesvolle technicus | Over het algemeen ondersteunt het succes van klanten met AMS. Interactie met [!UICONTROL Cloud Manager] het doel om implementaties uit te voeren waarvoor toezicht van de Klant vereist is. |
| Inhoudsauteur | Over het algemeen heeft dit geen invloed op [!UICONTROL Cloud Manager]de interactie. Deze gebruiker kan de [!UICONTROL Cloud Manager] Programmaswitch (die vanuit [!UICONTROL Experience Cloud]) is genavigeerd, gebruiken om toegang te krijgen tot Adobe Experience Manager (AEM). |

## Gebruikersmachtigingen {#user-permissions}

Elk van de rollen heeft specifieke toestemmingen, vooraf geconfigureerde taken, of toestemmingen, verbonden aan elke rol. Deze lijst maakt een lijst van de beschikbare functies en de rollen die de functie kunnen uitvoeren.

Zie Gebruikers en rollen [instellen voor meer informatie over het instellen van uw gebruikers](setting-up-users-and-roles.md).

| Machtiging | Beschrijving | Business Owner | Deployment Manager | Program Manager | Developer | CSE |
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

