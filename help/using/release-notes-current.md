---
title: Opmerkingen bij de release 2022.3.0
description: Dit zijn de opmerkingen bij de release 2022.3.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0d14adda454889eebbb0a875978ceeaa5ee4f7ea
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Opmerkingen bij de release 2022.3.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2022.3.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2022.3.0 is 10 maart 2022. De volgende release is gepland voor 7 april 2022.

## Wat is er nieuw? {#what-is-new}

* (Alleen Cloud Service) U kunt het logboek AEM omgeving openen met de rol Developer.
* De [`reliability_rating` kritisch metrisch](understand-your-test-results.md) is uitgeschakeld.


## Opgeloste problemen {#bug-fixes}

* [De **Wijzigingen in taakverdeling overslaan** option](configuring-production-pipelines.md#adding-production-pipeline) kan nu correct worden uitgeschakeld.
* [De **Wijzigingen in taakverdeling overslaan** option](configuring-production-pipelines.md#adding-production-pipeline) wordt nu weergegeven voor de workflow van de distributiepijplijn.
* Een subset van handmatig gemaakte git-opslagplaatsen had onjuiste naamwaarden die van invloed waren op [de functie voor hergebruik van bouwartefacten.](setting-up-project.md#build-artifact-reuse) De namen van deze opslagruimten zijn gewijzigd en gebruikers zien de gecorrigeerde naam in de API/UI van Cloud Manager.
* [Wanneer het toevoegen van of het uitgeven van een pijpleiding van de codekwaliteit,](configuring-non-production-pipelines.md) de opties voor de afhandeling van metrische fouten worden niet meer weergegeven.
* De onverwachte configuraties van de pijpleidingsvariabele veroorzaken niet meer fouten in de bouwstijlstap.
