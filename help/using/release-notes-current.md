---
title: Opmerkingen bij de release 2022.3.0
description: Dit zijn de opmerkingen bij de release 2022.3.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 4a5ddf3144ec50f1a7a4ac367b5c99bc9b486752
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Opmerkingen bij de release 2022.3.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2022.3.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2022.3.0 is 10 maart 2022. De volgende release is gepland voor 7 april 2022.

## Wat is er nieuw? {#what-is-new}

* De verzoeken van HTTP van de grenzen van HTTP van activa zullen nu uit een Vaste IP waaier komen.


## Opgeloste problemen {#bug-fixes}

* De **Wijzigingen in taakverdeling overslaan** kan niet worden uitgeschakeld.
* De **Wijzigingen in taakverdeling overslaan** Deze optie is niet weergegeven op de AMS Dev-implementatie **Pipetworkflow bewerken**.
* Een subset van handmatig gemaakte it-opslagruimten had een onjuiste naamwaarde waardoor de functie voor hergebruik van bouwmateriaal niet doeltreffend was. De namen van deze opslagruimten zijn gewijzigd en gebruikers zien de gecorrigeerde naam in de API/UI van Cloud Manager.
* Bij de productie van volledige stapelleidingen werden bouwartefacten van niet-productiepijpleidingen onjuist opnieuw gebruikt.
* Wanneer het toevoegen van of het uitgeven van een pijpleiding van de codekwaliteit, worden de opties om metrische mislukkingen te behandelen niet meer getoond.
* Sommige onverwachte configuraties van pijpleidingsvariabele konden in de bouwstijlstap veroorzaken.
