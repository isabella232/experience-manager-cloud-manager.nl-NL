---
title: Opmerkingen bij de release 2023.8.0
description: Dit zijn de opmerkingen bij de release 2023.8.0 voor Cloud Manager.
feature: Release Information
source-git-commit: 26c4c945e18f21b812f65dbabc14a4e8ab9f6b43
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Opmerkingen bij de release 2023.8.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2023.8.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2023.8.0 is 10 augustus 2023. De volgende release is gepland voor 14 september 2023.

## Wat is er nieuw? {#what-is-new}

* Er zijn verbeteringen aangebracht om de begrijpelijkheid en het omgaan met foutberichten in de gebruikersinterface van Cloud Manager te verbeteren.

## Opgeloste problemen {#bug-fixes}

* Niet frequente gevallen [inhoudskopie](/help/using/content-copy.md) processen die vastlopen , zijn aangepakt .
* Er is een tijdelijk testprobleem opgelost voor klanten die geen New Relic One gebruiken.
* [De kwaliteitsregels voor aangepaste code](/help/using/custom-code-quality-rules.md) `SupportedRunmode` en `ImmutableMutableMixedPackage` uit SonarQube zijn verwijderd, omdat ze alleen van toepassing zijn op AEM as a Cloud Service.
* Gebruikers zullen niet meer geconfronteerd worden met vastgezette pijpleidingen die in bedrijf lijken te zijn.
* De **Omgevingen** wordt nu gesloten na het activeren van de **[Inhoud kopiëren](/help/using/content-copy.md)** modal.
* [Een wederuitvoering van de pijpleiding](/help/using/code-deployment.md#reexecute-deployment) is niet meer toegestaan als de vorige uitvoering geen `commitId` reeks op de bouwstijlstaat.
* Een begrijpelijker bericht wordt nu getoond voor zeldzame fouten wanneer een gebruiker op een pijpleiding in klikt **Activiteit** of **Pijpleiding** schermen.
