---
title: Aangepaste machtigingen
description: Leer hoe u douanetoestemmingen kunt gebruiken om nieuwe profielen van de douanetoestemming met configureerbare toestemmingen tot stand te brengen om toegang tot programma's, pijpleidingen en milieu's voor de gebruikers van de Managers van de Wolk te beperken.
exl-id: a81eda9f-aa89-40ea-8e4c-52367a0a6aba
source-git-commit: 16eef51d86647ae4f2515f3f3c4cb2d15e948854
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Aangepaste machtigingen {#custom-permissions}

Leer hoe u douanetoestemmingen kunt gebruiken om nieuwe profielen van de douanetoestemming met configureerbare toestemmingen tot stand te brengen om toegang tot programma&#39;s, pijpleidingen en milieu&#39;s voor de gebruikers van de Managers van de Wolk te beperken.

## Inleiding {#introduction}

Cloud Manager heeft een set vooraf gedefinieerde rollen die de toegang tot verschillende functies van cloudbeheer bepalen:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Met aangepaste machtigingen kunnen gebruikers nieuwe aangepaste machtigingsprofielen maken met configureerbare machtigingen om de toegang voor gebruikers van Cloud Managers te beperken tot programma&#39;s, pijpleidingen en omgevingen.

>[!TIP]
>
>Zie het document voor meer informatie over vooraf gedefinieerde rollen [Op rollen gebaseerde machtigingen.](/help/requirements/role-based-permissions.md)

## Aangepaste machtigingen gebruiken {#using}

Voor het maken en gebruiken van uw eigen aangepaste machtigingen zijn drie stappen vereist:

1. [Maak een nieuw productprofiel.](#create)
1. [Wijs aangepaste machtigingen toe aan het nieuwe productprofiel.](#assign-permissions)
1. [Gebruikers toewijzen aan het nieuwe productprofiel.](#assign-users)

In deze sectie worden deze stappen beschreven. Het kan handig zijn te verwijzen naar de [Voorwaarden](#terms) en [Configureerbare machtigingen](#configurable-permissions) secties als u uw eigen aangepaste machtigingen maakt.

>[!NOTE]
>
>U moet over de rechten van de productbeheerder in Admin Console hebben om nieuwe profielen te creëren en toestemmingen voor de Manager van de Wolk te beheren.

### Een nieuw productprofiel maken {#create}

U moet eerst een nieuw productprofiel maken voordat u aangepaste machtigingen kunt toewijzen.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. Selecteer het product **AEM Managed Services**.

1. Zoeken naar en instantie met een naam die overeenkomt met het patroon `*-cloud-manager` en tik of klik om gebruikers en machtigingen te beheren.

1. U wordt omgeleid naar de **Producten** tabblad van de Admin Console, waar u gebruikers en machtigingen voor cloudbeheer kunt beheren. Tik in de Admin Console of klik op de knop **Nieuw profiel** knop.

![Knop Nieuw profiel](/help/assets/admin-console-new-profile.png)

1. Geef de algemene details over het profiel op.

   * **Naam van productprofiel** - Een beschrijvende naam voor het profiel
   * **Weergavenaam** - Een afgekorte naam die wordt weergegeven in de gebruikersinterface (opties)
   * **Beschrijving** - Een informatieve beschrijving van het profiel waarin het doel van het profiel wordt toegelicht (optioneel)
   * **Gebruikers via e-mail op de hoogte stellen** - Als deze optie is geselecteerd, worden gebruikers via e-mail op de hoogte gesteld wanneer ze uit dit profiel worden toegevoegd of verwijderd.

1. Tik of klik op **Opslaan** wanneer voltooid.

Het nieuwe productprofiel wordt opgeslagen en wordt weergegeven in de lijst met productprofielen in de Admin Console.

### Aangepaste machtigingen toewijzen aan profiel {#assign-permissions}

Nu u een nieuw productprofiel hebt, kunt u er aangepaste machtigingen aan toewijzen.

1. Tik in de Admin Console op de naam van de [nieuw productprofiel dat u zojuist hebt gemaakt.](#create)

1. Selecteer in het venster dat wordt geopend de optie **Machtigingen** om een lijst met bewerkbare machtigingen weer te geven.

   ![Bewerkbare machtigingen](/help/assets/permissions-tab.png)

1. Tik of klik op de knop **Bewerken** koppeling van een machtiging om deze te bewerken.

1. De **Rechten bewerken** wordt geopend.
   * De machtigingen die u in de vorige stap hebt geselecteerd, worden in de linkerkolom geselecteerd.
   * De machtigingsitems die beschikbaar zijn voor toewijzing voor de machtiging bevinden zich in de middelste kolom met het label **Beschikbare machtiging** Items.
   * De toegewezen toestemmingspunten zijn in de juiste kolom geëtiketteerd **Opgenomen machtigingsitems**.

   ![Machtigingsitems bewerken](/help/assets/edit-permission-items.png)

1. Tik of klik op de plusknop (`+`), pictogram naast het machtigingsitem om dit aan de kolom toe te voegen **Opgenomen machtigingsitems**.

   * Tik of klik op de knop `i` pictogram naast een machtigingsitem om er meer over te leren.

1. Tik of klik op de knop **Alles toevoegen** aan de bovenkant van de **Beschikbare machtigingen** kolom om alle machtigingen toe te voegen. Tik op dezelfde manier of klik op **Alles verwijderen** om alle eerder geselecteerde machtigingen te verwijderen.

1. Tik of klik op **Opslaan** als u klaar bent met het definiëren van de machtigingsitems voor uw nieuwe productprofiel.

Uw nieuwe productprofiel wordt nu opgeslagen met de aangepaste machtigingen.

### Gebruikers toewijzen aan aangepaste machtigingen {#assign-users}

U kunt nu gebruikers toewijzen aan het nieuwe productprofiel dat u met aangepaste machtigingen hebt gemaakt.

1. Tik in de Admin Console op de naam van de [nieuw productprofiel waaraan u zojuist aangepaste machtigingen hebt toegewezen.](#assign-permissions)

1. Selecteer in het venster dat wordt geopend de optie **Gebruikers** tab.

1. Tik of klik op de knop **Gebruikers toevoegen** en wijs gebruikers aan uw nieuw productprofiel met douanetoestemmingen toe.

Zie de sectie **Gebruikers en gebruikersgroepen toevoegen aan een productprofiel** van het document [Productprofielen beheren voor zakelijke gebruikers](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) voor meer informatie over het gebruik van de Admin Console.

## Configureerbare machtigingen {#configurable-permissions}

De volgende machtigingen zijn beschikbaar voor het maken van aangepaste profielen.

| Machtiging | Beschrijving |
|---|---|
| Programmatoegang | Gebruikers toegang geven tot programma&#39;s |
| Programmabewerking | Gebruikers mogen programma&#39;s bewerken |
| Pipet maken | Gebruikers toestaan nieuwe pijpleidingen te maken |
| Pipet verwijderen | Gebruikers toestaan pijpleidingen te verwijderen |
| Pipet bewerken | Gebruikers toestaan pijpleidingen te bewerken |
| Productieimplementaties goedkeuren/afwijzen | Gebruikers toestaan een stap voor productieimplementatie goed te keuren of af te wijzen |
| Uitvoeringen pijplijn annuleren | Laat gebruikers uitvoeren pijpleidingen annuleren |
| Start van pijplijnuitvoering | Gebruikers toestaan een nieuwe pijpleiding uit te voeren |
| Belangrijke metrische fouten negeren/negeren | Gebruikers toestaan belangrijke metrische fouten te negeren/af te wijzen |
| Plan voor productieimplementaties | Gebruikers toestaan een stap voor productieimplementatie te plannen |
| Toegang tot opslaggegevens | Gebruikers toegang geven tot dataopslag en een wachtwoord voor toegang genereren |
| Opslagplaats maken | Gebruikers toestaan nieuwe it-opslagruimten te maken |
| Opslagplaats verwijderen | Gebruikers mogen it-opslagruimten verwijderen |
| Bewerken opslagplaats | Gebruikers mogen it-opslagruimten bewerken |
| Code opslagplaats genereren | Gebruikers toestaan een project te genereren op basis van het archetype |
| Inhoud kopiëren beheren | Gebruikers toestaan bewerkingen voor het kopiëren van inhoud te beheren |

### Rechten op organisatieniveau {#organization-level}

Machtigingen op organisatieniveau verwijzen naar machtigingen die altijd worden gegeven voor alle programma&#39;s in een organisatie.

De volgende machtigingen zijn bevoegdheden op organisatieniveau:

* **Toegang tot opslaggegevens** Deze huurder/organisatie niveautoestemming staat gebruikers toe om gebruikersbenaming, wachtwoord en bewaarplaats URL voor toegang te produceren en tot klantenproject bij te dragen.
   * Gebruikersnaam en wachtwoord voor toegang tot opslagplaats zijn hetzelfde voor alle repos op de org, maar de URL van de opslagplaats is uniek voor elk programma.
   * Zie het document [Broncodeopslagplaats](/help/requirements/source-code-repository.md) voor meer informatie .

## Voorwaarden {#terms}

De volgende termen worden gebruikt bij het maken en beheren van aangepaste machtigingen en vooraf gedefinieerde rollen.

| Term | Beschrijving |
|---|---|
| Vooraf gedefinieerde machtigingen | Vooraf gedefinieerde rollen zoals **Zakelijke eigenaar**, **Implementatiebeheer**, enz. om verschillende functies van Cloud Manager te beheren. Zie het document voor meer informatie over vooraf gedefinieerde rollen [Op rollen gebaseerde machtigingen.](/help/requirements/role-based-permissions.md) |
| Aangepaste machtigingen | Cloud Manager-functies waarmee gebruikers machtigingsprofielen kunnen maken om rollen te definiëren die de ondersteunde functies van Cloud Manager besturen |
| Machtigingsprofiel | Gemaakt in de beheerconsole voor het beheer van configureerbare machtigingen die van toepassing zijn op gebruikers die deel uitmaken van het machtigingsprofiel |
| Configureerbare machtiging | Cloudbeheermachtigingen die kunnen worden geconfigureerd in machtigingsprofiel |
| Machtigingsitem | Een programma, milieu of pijpleidingsmiddel waarop een toestemming kan worden toegepast |

De punten van de toestemming verwijzen naar het werkingsgebied waar de toestemming zal worden toegepast. Doorgaans is dit een van de volgende:

| Type machtigingsitem | Voorbeeld | Beschrijving |
|---|---|---|
| Organisatie | organisatie:bedrijfA | Alle toepasselijke middelen van een organisatie. Een bron kan een programma, omgeving of pijpleiding zijn. Als de gebruiker een organisatie voor om het even welke toestemming toevoegt dan zullen alle nieuwe middelen in die organisatie ook die toestemming hebben. |
| Programma | Programma A | Alle toepasselijke middelen van een programma |
| Omgeving | Programma A: milieu | Van toepassing op een specifieke omgeving |
| Pijpleiding | Programma A : Pipeline | Van toepassing op een specifieke pijpleiding |

## Beperkingen {#limitations}

Houd rekening met de volgende beperkingen wanneer u aangepaste machtigingen gebruikt.

* A [beperkte set machtigingen is beschikbaar](#configurable-permissions) voor het maken van aangepaste profielen.
* Middelen zoals programma, milieu, pijpleiding enz. die zijn gemaakt in Cloud Manager, kan twee minuten in beslag nemen om in Admin Console weer te geven voor de configuratie van machtigingen.
* In zeldzame gevallen waarin de service met aangepaste machtigingen niet reageert, zijn vooraf gedefinieerde profielen nog steeds beschikbaar en hebben gebruikers in vooraf gedefinieerde profielen nog steeds de juiste toegang.

## Veelgestelde vragen {#faq}

### Welke machtigingsprofielen zijn vooraf gedefinieerde machtigingsprofielen?

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Zie het document voor meer informatie over vooraf gedefinieerde rollen [Op rollen gebaseerde machtigingen.](/help/requirements/role-based-permissions.md)

### Wat gebeurt er met vooraf gedefinieerde machtigingsprofielen met inleiding tot aangepaste profielen?

De standaardproductprofielen en de rollen van de wolkenmanager blijven het zelfde werken zoals voordien.

### Kan ik vooraf gedefinieerde machtigingsprofielen bewerken?

Nee, standaardprofielen kunnen niet worden bewerkt. U kunt geen machtigingen toevoegen aan of verwijderen uit het standaardmachtigingsprofiel. U kunt alleen gebruikers toevoegen aan of verwijderen uit vooraf gedefinieerde profielen.

### Moet ik vooraf gedefinieerde machtigingsprofielen verwijderen, omdat aangepaste profielen nu beschikbaar zijn?

Vooraf gedefinieerde machtigingsprofielen mogen niet uit de Admin Console worden verwijderd.

### Kan ik gebruikers toevoegen aan meerdere machtigingsprofielen?

Ja, een gebruiker kan deel uitmaken van meerdere profielen, waaronder vooraf gedefinieerde en aangepaste machtigingsprofielen. Wanneer een gebruiker aan meerdere profielen wordt toegewezen, zijn de gecombineerde machtigingen van alle toegewezen machtigingsprofielen beschikbaar voor die gebruiker.

### Wat gebeurt als een gebruiker toestemming heeft om een milieu/pijpleiding uit te geven maar geen toegang tot een programma heeft dat het milieu/de pijpleiding bevat?

In dit geval zal de gebruiker niet tot het milieu of de pijpleiding kunnen toegang hebben als zij niet hebben **Programmatoegang** machtigingen die de omgeving of pijplijn bevatten.

### Wat gebeurt er als ik zowel AEM as a Cloud Service als AMS programma&#39;s in dezelfde IMS org heb? Kan ik machtigingen van één profiel beheren? {#ams-and-aemaacs}

U moet voor elk producttype een apart profiel maken (dat wil zeggen een profiel voor AEM als Cloud Service en een profiel voor Adobe Managed Services of AMS).
