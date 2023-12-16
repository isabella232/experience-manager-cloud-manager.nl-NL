---
title: Opmerkingen bij de release 2023.12.0
description: Dit zijn de opmerkingen bij de release 2023.12.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 2ac254508e4015fea21c4fcd087703ac5fbeeec6
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Opmerkingen bij de release 2023.12.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2023.12.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2023.12.0 is 14 december 2023. De volgende release is gepland voor 18 januari 2024.

## Wat is er nieuw? {#what-is-new}

* [Aangepaste machtigingen voor Cloud Manager](/help/using/custom-permissions.md) Hiermee kunt u nieuwe aangepaste machtigingsprofielen maken met configureerbare machtigingen om de toegang tot programma&#39;s, pijpleidingen en omgevingen voor gebruikers van Cloud Manager te beperken.
* De rollouts van updates aan [omgeving bouwen](/help/getting-started/build-environment.md) die [aangekondigd en begonnen met de release van Cloud Manager in oktober](/help/release-notes/2023/2023-10-0.md) zijn voltooid.
   * Ondersteuning voor Node 18 is toegevoegd voor [voorkant en volledige stapelleidingen.](/help/overview/ci-cd-pipelines.md)
   * Kleine Java 8-versie bijgewerkt naar `jdk1.8.0_371`.
   * Kleine Java 11-versie bijgewerkt naar `jdk-11.0.20`.
   * Maven is bijgewerkt naar versie 3.8.8
      * Maven schakelt nu alles onveilig uit `http://*` spiegels standaard.
      * [Adobe beveelt aan](/help/getting-started/build-environment.md#https-maven) gebruikers werken hun Geweven opslagplaatsen bij om HTTPS in plaats van HTTP te gebruiken.
* De basisafbeelding van de build-container is bijgewerkt naar Ubuntu 22.04.

## Programma voor vroegtijdige adoptie {#early-adoption}

Maak deel uit van ons programma voor vroege goedkeuring en heb de kans om een aantal van de volgende kenmerken te testen

### Breng uw eigen GitHub {#byo-github}

Als u GitHub gebruikt om uw bewaarplaatsen te beheren, [u kunt code binnen uw bewaarplaatsen van GitHub door de Manager van de Wolk nu bevestigen.](/help/managing-code/byo-github.md) Door deze integratie is het niet nodig de code consistent te synchroniseren met de opslagplaats van de Adobe en kunt u terugtrekkingsverzoeken verifiëren voordat u ze samenvoegt in de hoofdvertakkingen.

Als je deze nieuwe functie wilt testen en je feedback wilt delen, stuur dan een e-mail naar `Grp-CloudManager_BYOG@adobe.com` van uw e-mailadres dat aan uw Adobe ID is gekoppeld.
