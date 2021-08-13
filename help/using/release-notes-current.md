---
title: Opmerkingen bij de release 2021.8.0
description: Volg deze pagina om informatie op te halen voor Cloud Manager Release 2021.8.0
feature: Geen informatie
source-git-commit: c4deb06615652736ff7584566507a2b42a88bfb1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# Opmerkingen bij de release 2021.8.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.8.0 beschreven.

>[!NOTE]
>Raadpleeg [Opmerkingen bij de huidige release](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) om de meest recente releaseopmerkingen voor Cloud Manager in AEM als Cloud Service te bekijken.

## Releasedatum {#release-date}

De Releasedatum voor [!UICONTROL Cloud Manager] Versie 2021.8.0 is 12 augustus 2021.
De volgende release is gepland voor 9 september 2021.

## Wat is er nieuw? {#whats-new}

* Self-service mogelijkheid om gebruikers in staat te stellen meerdere opslagruimten te maken en te beheren via de interface van Cloud Manager.

* SonarQube leest onnodig gegevens over de git-geschiedenis. Op grote codebasis, zou dit tot een onnodige bouwstijlprestaties kunnen leiden.

* Er is nu een API beschikbaar om het Geweven gebiedsdeelheidsgeheime voorgeheugen per pijpleiding ongeldig te maken.

* De versie van het AEM Project Archetype dat wordt gebruikt door Cloud Manager is bijgewerkt naar versie 29.

## Opgeloste problemen {#bug-fixes}

* Af en toe, wanneer een pijpleiding tweemaal om één of andere reden wordt teweeggebracht, resulteert het in één van de uitvoeringen die met *geen status van de pijpleidingsuitvoering kan bijwerken* fout.
