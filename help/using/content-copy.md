---
title: Het gereedschap Inhoud kopiëren
description: Met het hulpprogramma voor het kopiëren van inhoud van Cloud Manager kunnen gebruikers op verzoek muterende inhoud kopiëren van hun AMS-gehoste AEM 6.x-productieomgevingen naar lagere omgevingen voor testdoeleinden.
exl-id: 97915e58-a1d3-453f-b5ce-cad55ed73262
source-git-commit: fe5de4e1ab5cd0d0e317cd399b8e44758a6312c4
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---


# Het gereedschap Inhoud kopiëren {#content-copy}

Met het hulpprogramma voor het kopiëren van inhoud van Cloud Manager kunnen gebruikers op verzoek muterende inhoud kopiëren van hun AMS-gehoste AEM 6.x-productieomgevingen naar lagere omgevingen voor testdoeleinden.

## Inleiding {#introduction}

De huidige, echte gegevens zijn waardevol voor het testen, de bevestiging, en de gebruiker-aanvaarding doeleinden. Met het gereedschap Inhoud kopiëren kunt u inhoud van uw productie-AMS-gehoste AEM 6.x-omgeving kopiëren naar een testomgeving.

De inhoud die moet worden gekopieerd, wordt gedefinieerd door een inhoudsset. Een inhoudsset bestaat uit een lijst met JCR-paden die de veranderbare inhoud bevatten die vanuit een bronomgeving naar een doelomgeving binnen hetzelfde programma van Cloud Manager moet worden gekopieerd. De volgende paden zijn toegestaan in een inhoudsset.

```text
/content/**
/conf/**
/etc/**
/var/workflow/models/**
```

Wanneer het kopiëren van inhoud, is het bronmilieu de bron van waarheid.

* Als de inhoud in de bestemmingsmilieu is gewijzigd, zal het door inhoud in de bron worden beschreven, als de wegen het zelfde zijn.
* Als de paden verschillend zijn, wordt de inhoud van de bron samengevoegd met de inhoud in de bestemming.

>[!NOTE]
>
>Neem contact op met uw Customer Success Engineer (CSE) om deze functie in te schakelen.

## Machtigingen {#permissions}

Als u het gereedschap Inhoud kopiëren wilt gebruiken, moet de gebruiker aan de **Implementatiebeheer** rol in de bron- en doelomgevingen.

## Een inhoudsset maken {#create-content-set}

Voordat inhoud kan worden gekopieerd, moet een inhoudsset zijn gedefinieerd. Wanneer deze is gedefinieerd, kunnen inhoudssets opnieuw worden gebruikt om inhoud te kopiëren. Ga als volgt te werk om een inhoudenset te maken.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) en selecteert u de gewenste organisatie en het juiste programma.

1. Ga naar de **Omgevingen** van het scherm **Overzicht** pagina.

1. Ga naar de **Inhoudssets** pagina van de **Omgevingen** scherm.

1. Tik of klik op de knop **Inhoudsset toevoegen** aan de rechterbovenhoek van het scherm.

   ![Inhoudssets](/help/assets/content-sets.png)

1. Op de **Details** Geef een naam en een beschrijving voor de inhoudenset op en tik of klik op **Doorgaan**.

   ![Details van inhoudsset](/help/assets/add-content-set-details.png)

1. Op de **Inhoudspaden** van de wizard, geeft u de paden op van de inhoud die u wilt wijzigen.

   1. Voer het pad in het dialoogvenster **Inclusief pad toevoegen** veld.
   1. Tik of klik op de knop **Pad toevoegen** om het pad aan de inhoudenset toe te voegen.
   1. Tik of klik op de knop **Pad toevoegen** nogmaals indien nodig.

   ![Paden toevoegen aan inhoudsset](/help/assets/add-content-set-paths.png)

1. Als u de inhoudenset moet verfijnen of beperken, kunnen subpaden worden uitgesloten.

   1. Tik of klik op de knop **Subpaden uitsluiten toevoegen** pictogram naast het pad dat u moet beperken.
   1. Voer het subpad in dat u onder het geselecteerde pad wilt uitsluiten.
   1. Tik of klik op **Pad uitsluiten**.
   1. Tik of klik op **Subpaden uitsluiten toevoegen** nogmaals om extra paden toe te voegen om deze uit te sluiten.

   ![Paden uitsluiten](/help/assets/add-content-set-paths-excluded.png)

1. U kunt de opgegeven paden desgewenst wijzigen.

   1. Tik of klik op de X naast de uitgesloten subpaden om deze te verwijderen.
   1. Tik of klik op de knop Ovaal naast de paden die u wilt tonen **Bewerken** en **Verwijderen** opties.

   ![Padlijst bewerken](/help/assets/add-content-set-excluded-paths.png)

1. Tik of klik op **Maken** om de inhoudenset te maken.

De inhoudenset kan nu worden gebruikt om inhoud tussen omgevingen te kopiëren.

>[!NOTE]
>
>U kunt maximaal 50 paden toevoegen aan een inhoudsset.
>Uitgesloten paden zijn niet beperkt.

## Een inhoudsset bewerken {#edit-content-set}

Voer vergelijkbare stappen uit als bij het maken van een stap Inhoud. In plaats van te tikken of te klikken **Inhoudsset toevoegen** selecteert u een bestaande set in de console en selecteert u **Bewerken** in het ovaalmenu.

![Inhoudsset bewerken](/help/assets/edit-content-set.png)

Wanneer u de inhoudenset bewerkt, moet u mogelijk de geconfigureerde paden uitbreiden om de uitgesloten subpaden zichtbaar te maken.

## Inhoud kopiëren {#copy-content}

Nadat u een inhoudsset hebt gemaakt, kunt u deze gebruiken om inhoud te kopiëren. Ga als volgt te werk om inhoud te kopiëren.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) en selecteert u de gewenste organisatie en het juiste programma.

1. Ga naar de **Omgevingen** van het scherm **Overzicht** pagina.

1. Ga naar de **Inhoudssets** pagina van de **Omgevingen** scherm.

1. Selecteer een inhoudsset in de console en selecteer **Inhoud kopiëren** in het ovaalmenu.

   ![Inhoud kopiëren](/help/assets/copy-content.png)

   >[!NOTE]
   >
   >Een omgeving kan niet selecteerbaar zijn als:
   >
   >* De gebruiker beschikt niet over de juiste machtigingen.
   >* Het milieu heeft een lopende pijpleiding of een verrichting van de exemplaarinhoud lopend.

1. In de **Inhoud kopiëren** geeft u de bron en de bestemming op voor de actie Kopiëren van inhoud.

1. U kunt ervoor kiezen om de paden voor uitsluiten te verwijderen of te behouden in de doelomgeving. Selectievakje selecteren `Do not delete exclude paths from destination` als u de uitsluitingspaden wilt behouden die in de inhoudenset zijn opgegeven. Als het selectievakje uitgeschakeld blijft, worden paden uitgesloten uit de doelomgeving.

1. U kunt versiehistorie kopiëren van de paden die van bron naar doelomgeving worden gekopieerd. Selectievakje selecteren `Copy Versions` als u alle versiehistorie wilt kopiëren.

   ![Inhoud kopiëren](/help/assets/copying-content.png)

1. Tik of klik op **Kopiëren**.

Het kopieerproces wordt gestart. De status van het kopieerproces wordt weerspiegeld in de console voor de geselecteerde inhoudenset.

## Activiteit voor kopiëren van inhoud {#copy-activity}

U kunt de status van uw kopieerprocessen in de **Inhoudsactiviteit kopiëren** pagina.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) en selecteert u de gewenste organisatie en het juiste programma.

1. Ga naar de **Omgevingen** van het scherm **Overzicht** pagina.

1. Ga naar de **Inhoudsactiviteit kopiëren** pagina van de **Omgevingen** scherm.

![Activiteit voor kopiëren van inhoud](/help/assets/copy-content-activity.png)

### Statussen van inhoud kopiëren {#statuses}

Wanneer u begint inhoud te kopiëren, kan het proces een van de volgende statussen hebben.

| Status | Beschrijving |
|---|---|
| In uitvoering | De bewerking voor het kopiëren van inhoud is aan de gang |
| Mislukt | Kopiëren van inhoud is mislukt |
| Voltooid | Kopie van inhoud voltooid |

## Beperkingen {#limitations}

Het gereedschap voor het kopiëren van inhoud heeft de volgende beperkingen.

* Een inhoudkopie kan niet worden uitgevoerd van een lagere omgeving naar een hogere omgeving.
* Het kopiëren van inhoud kan alleen worden uitgevoerd binnen dezelfde laag (dus auteur of publicatie).
* Kopiëren van inhoud tussen programma&#39;s en regio&#39;s is niet mogelijk.
* Inhoudskopie voor topologie op basis van gegevensopslag in de cloud kan alleen worden uitgevoerd wanneer de bron- en doelomgeving zich op dezelfde cloudprovider en hetzelfde gebied bevinden.
* Het uitvoeren van gelijktijdige bewerkingen voor het kopiëren van inhoud in dezelfde omgeving is niet mogelijk.
* Het exemplaar van de inhoud kan niet worden uitgevoerd als er om het even welke actieve verrichting die op of het doel of bronmilieu zoals een pijpleiding CI/CD loopt.
* Per inhoudenset kunnen maximaal vijftig paden worden opgegeven. Uitgesloten paden zijn niet beperkt.
* Het gereedschap voor het kopiëren van inhoud mag niet worden gebruikt als een kloon- of spiegelgereedschap omdat het geen verplaatste of verwijderde inhoud van de bron kan bijhouden.
* Een inhoudkopie kan niet worden gepauzeerd of geannuleerd nadat deze is gestart.
* Met het gereedschap voor het kopiëren van inhoud kopieert u elementen samen met dynamische metagegevens over media van de hogere omgeving naar de geselecteerde lagere omgeving.
   * Gekopieerde elementen moeten vervolgens opnieuw worden verwerkt met de opdracht [Workflow voor DAM-procesmiddelen](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html) op de lagere omgeving om de respectieve dynamische mediasonfiguratie te gebruiken.
* Het kopiëren van inhoud gaat aanzienlijk sneller als de versiegeschiedenis niet wordt gekopieerd.
