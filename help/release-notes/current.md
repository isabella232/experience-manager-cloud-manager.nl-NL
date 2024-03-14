---
title: Opmerkingen bij de release 2024.3.0
description: Dit zijn de opmerkingen bij de release 2024.3.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 22730ba281f7c1c4720158a3a813c56b815a0af1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Release-aantekeningen voor Cloud Manager versie 2024.3.0 {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2024.3.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2024.3.0 is 14 maart 2024. De volgende release is gepland voor 11 april 2024.

## Wat is er nieuw? {#what-is-new}

* De details met inbegrip van IP/DNS (FQDN) informatie van groene servers worden nu getoond in de UI van de Manager van de Wolk.

## Programma voor vroegtijdige adoptie {#early-adoption}

Maak deel uit van ons programma voor vroege goedkeuring en heb de kans om een aantal van de volgende kenmerken te testen

### Breng uw eigen GitHub {#byo-github}

Als u GitHub gebruikt om uw bewaarplaatsen te beheren, [u kunt code binnen uw bewaarplaatsen van GitHub door de Manager van de Wolk nu bevestigen.](/help/managing-code/byo-github.md) Door deze integratie is het niet nodig de code consistent te synchroniseren met de opslagplaats van de Adobe en kunt u terugtrekkingsverzoeken verifiëren voordat u ze samenvoegt in de hoofdvertakkingen. Deze eigenschap is exclusief aan openbare GitHub. De steun voor zelf-ontvangen GitHub is niet beschikbaar.

Als je deze nieuwe functie wilt testen en je feedback wilt delen, stuur dan een e-mail naar `Grp-CloudManager_BYOG@adobe.com` van uw e-mailadres dat aan uw Adobe ID is gekoppeld.

## Opgeloste problemen {#bug-fixes}

* Een bug werd bevestigd wanneer de aangewezen logboeken niet tijdens de stap van de prestatietest werden geproduceerd wanneer de metrisch van het foutentarief ontbrak.
* De verbeterde logica binnen de dienst van de prestatietest die met het ontdekken van de afwezigheid van een pagina op de plaats wordt belast (404) verzekert nu vlottere, ononderbroken plaatsing.
