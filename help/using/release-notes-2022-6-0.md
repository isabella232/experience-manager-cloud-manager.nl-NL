---
title: Opmerkingen bij de release 2022.6.0
description: Dit zijn de opmerkingen bij de release 2022.6.0 voor Cloud Manager.
feature: Release Information
source-git-commit: f202b245f35bcffa56b43f26a13b97d42fdb474e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---


# Opmerkingen bij de release 2022.6.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2022.6.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2022.6.0 is 9 juni 2022. De volgende release is gepland voor 30 juni 2022.

## Wat is er nieuw? {#what-is-new}

* Een nieuwe welkomstkaart op de landingspagina van Cloud Manager biedt gebruikers snel toegang tot zelfstudies aan boord en voortgangsgegevens voor de huurder.
   * Deze functie wordt in de week na de release van 2022.06.0 geleidelijk ingevoerd.
* [Buildartefacten kunnen nu opnieuw worden gebruikt](/help/using/setting-up-project.md#build-artifact-reuse) bij gebruik van git spiegelen.

## API-wijzigingen {#api-changes}

* De [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API is vervangen en [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) moet worden gebruikt.
   * `List Programs` blijft werken, maar het gebruik ervan zal waarschuwingsberichten in logboeken genereren.
   * Na drie maanden wordt er geen steun meer verleend.