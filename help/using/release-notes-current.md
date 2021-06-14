---
title: Opmerkingen bij de release 2021.6.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.6.0
feature: Geen informatie
source-git-commit: 5ddbf718ad01b11dcba5dc2c5d1ab5d3cff2e9a9
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2021.6.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.6.0 beschreven.

>[!NOTE]
>Raadpleeg [Opmerkingen bij de huidige release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) om de meest recente releaseopmerkingen voor Cloud Manager in AEM als Cloud Service te bekijken.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.6.0 is 10 Juni, 2021.
De volgende release is gepland voor 15 juli 2021.

## Wat is er nieuw?{#whats-new}

* De activa en de Plaatsen testen zullen nu parallel lopen (indien van toepassing), daardoor verminderend de totale pijpleidingsuitvoeringstijd. Deze functie wordt de komende weken ingeschakeld voor klanten.

* Geweven Gedeelten die tijdens de bouwstijlstap worden gedownload zullen nu in het voorgeheugen ondergebracht tussen pijpleidinguitvoeringen worden. Deze functie wordt de komende weken ingeschakeld voor klanten.

* De standaardtaknaam die tijdens zowel project verwezenlijking als in het gebrek wordt gebruikt duw bevel via beheert git werkschema is veranderd in `main`.

* De ervaring met het bewerken van programma&#39;s in de gebruikersinterface is vernieuwd. Raadpleeg [Een programma bewerken](/help/using/setting-up-program.md#editing-program) voor meer informatie.

* De kwaliteitsregel `ImmutableMutableMixCheck` is bijgewerkt om `/oak:index` knopen als onveranderlijk te classificeren.

* De kwaliteitsregels `CQBP-84` en `CQBP-84--dependencies` zijn geconsolideerd in één enkele regel. Als onderdeel van deze consolidatie, identificeert het aftasten van gebiedsdelen nauwkeuriger kwesties in derdegebiedsdelen die aan AEM runtime worden opgesteld.

* In sommige situaties, zou het nalaten om Metrisch te berekenen Skipped Tests pijplijnuitvoeringen veroorzaken om te ontbreken.

## Opgeloste problemen {#bug-fixes}

* JCR-knooppuntdefinities die een nieuwe regel bevatten nadat de naam van het hoofdelement niet correct is geparseerd.

* De API voor opslagplaatsen weergeven filtert geen verwijderde opslagplaatsen.

* Er is een onjuist foutbericht weergegeven wanneer een ongeldige waarde voor de planningsstap is opgegeven.

* In sommige gevallen toen de pijpleidingsuitvoering aan productiestap werd bereikt, en de gebruiker beëindigt uitvoering, stelde het statusbericht in UI correct op wat eigenlijk aan het gebeuren was.
