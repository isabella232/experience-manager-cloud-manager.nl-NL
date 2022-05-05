---
title: Opmerkingen bij de release 2022.5.0
description: Dit zijn de opmerkingen bij de release 2022.5.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0ddfd152cb15731882d198d043dd8897b5073ab4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Opmerkingen bij de release 2022.5.0 van Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2022.5.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2022.5.0 is 5 mei 2022. De volgende release is gepland voor 9 juni 2022.

## Wat is er nieuw? {#what-is-new}

Toegang tot het logbestand voor AEM omgeving kan worden uitgevoerd met de rol van de ontwikkelaar.

## Opgeloste problemen {#bug-fixes}

* Een subset van handmatig gemaakte it-opslagruimten had een onjuiste naamwaarde waardoor de functie voor hergebruik van bouwmateriaal niet doeltreffend was. De namen van deze opslagruimten zijn gewijzigd en gebruikers zien de gecorrigeerde naam in de API/UI van Cloud Manager.
* Bij de productie van volledige stapelleidingen werden bouwartefacten van niet-productiepijpleidingen onjuist opnieuw gebruikt.
* Wanneer het toevoegen van of het uitgeven van een pijpleiding van de codekwaliteit, worden de opties om metrische mislukkingen te behandelen niet meer getoond.
* Sommige onverwachte configuraties van pijpleidingsvariabele konden fouten in de bouwstijlstap veroorzaken.
