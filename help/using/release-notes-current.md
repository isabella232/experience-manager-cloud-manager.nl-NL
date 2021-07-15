---
title: Opmerkingen bij de release 2021.7.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.7.0
feature: Geen informatie
source-git-commit: 1da4ceef0d89223580800d9018c46aaec51f8927
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Opmerkingen bij de release 2021.7.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.7.0 beschreven.

>[!NOTE]
>Raadpleeg [Opmerkingen bij de huidige release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) om de meest recente releaseopmerkingen voor Cloud Manager in AEM als Cloud Service te bekijken.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.7.0 is 15 Juli, 2021.
De volgende release is gepland voor 12 augustus 2021.

## Wat is er nieuw? {#whats-new}

* Klanten kunnen nu Azul 8 en 11 JDK&#39;s gebruiken voor hun buildprocessen in Cloud Manager en kunnen een van deze JDK&#39;s selecteren voor met toolketens compatibele Maven-plug-ins *of* voor de volledige uitvoering van het Maven-proces.

* Uitgaande uitgang IP zal nu het programma worden geopend het dossier van het bouwstijlstaplogboek.

* De knoppen **Git beheren** hebben een nieuwe naam **Toegang tot it-info** en het dialoogvenster is visueel vernieuwd.

* De versie van het AEM Project Archetype dat wordt gebruikt door Cloud Manager is bijgewerkt naar versie 28.

* Sommige onverwachte topologieherconfiguraties konden in gedetailleerde testrapporten resulteren die niet meer bij de pagina van de details van de pijpleidingsuitvoering beschikbaar zijn.

## Opgeloste problemen {#bug-fixes}

* Wanneer u handmatig naar de pagina met uitvoeringsdetails voor een niet-bestaande uitvoering navigeerde, werd geen fout weergegeven, alleen een eindeloos laadscherm.

* In sommige gevallen zou het automatisch opnieuw proberen van mislukte containers die in de prestaties van Plaatsen worden gebruikt niet 2 uur van kracht zijn, resulterend in een testmislukking.

## Bekende problemen {#known-issues}

Klanten die overstappen op de Azul JDK&#39;s moeten zich ervan bewust zijn dat niet alle bestaande toepassingen zonder fout zullen compileren op Azul JDK. Het wordt hoogst geadviseerd om plaatselijk vóór omschakeling te testen.