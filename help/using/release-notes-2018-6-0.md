---
title: Opmerkingen bij de release 2018.6.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2018.6.0
description: Deze pagina volgen voor informatie over Cloud Manager Release 2018.6.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2018.6.0.
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Opmerkingen bij de release voor 2018.6.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2018.6.0 beschreven en wordt ondersteuning toegevoegd voor validatie van verzenders tijdens implementaties, aanvullende meldingen en verbeteringen in de bruikbaarheid.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2018.6.0 is 9 Augustus, 2018.

## Wat is er nieuw?{#what-s-new}

* **CI/CD Pipeline**  - De configureerbare Invalidatie van de Verzender en het Geheime flushing van het Geheime voorgeheugen op zowel Stadium als Productie tijdens CI/CD de uitvoering van de Pijpleiding. Gelieve te verwijzen naar [vorm uw CI/CD Pijpleiding](configuring-pipeline.md) om meer te leren.

* **CI/CD Pijpleiding**  - Tijdens pijpleidingsopstelling, is het nu mogelijk om te bepalen hoe de pijpleiding zich zal gedragen wanneer het een Belangrijke mislukking in één van de kwaliteitspoorten ontmoet. Gelieve te verwijzen naar [vorm uw CI/CD Pijpleiding](configuring-pipeline.md) om meer te leren.

* **CI/CD de Pijpleiding**  - tijdens pijpleidingsopstelling, is het nu mogelijk om te selecteren of u CSE Toezicht door uw CSE of om het even welke beschikbare CSE wilt worden uitgevoerd. Gelieve te verwijzen naar [vorm uw CI/CD Pijpleiding](configuring-pipeline.md) om meer te leren.

* **CI/CD Pijpleiding**  - wanneer de CI/CD pijpleiding de bedrijfsgoedkeuringsstap bereikt, zal een bericht worden verzonden naar gebruikers die worden gemachtigd om de plaatsing goed te keuren. Raadpleeg [Meldingen](notifications.md) voor meer informatie.

* **CI/CD Pijpleiding**  - wanneer de CI/CD pijpleiding de planningsreeks bereikt, zal een bericht worden verzonden naar gebruikers die gemachtigd zijn om het programma te plaatsen. Raadpleeg [Meldingen](notifications.md) voor meer informatie.

* **Analyse**  van de Kwaliteit van de code - Nieuwe regels om verkeerd gevormde uitgaande HTTP/HTTPS- verzoeken te identificeren. Raadpleeg [Aangepaste regels voor codekwaliteit](custom-code-quality-rules.md) voor meer informatie.

## Opgeloste problemen {#bug-fixes}

* In sommige gevallen is de prestatietest niet volledig verdeeld over meerdere verzenders en publicatieinstanties.
* Koptekstnavigatie is verdwenen in smalle browservensters.
* Sommige pijpleidingsmontages werden niet onbruikbaar gemaakt terwijl de pijpleiding liep.
* De verbindingen aan AEM en Controle van het lijstscherm van het Programma vervingen zowel het huidige browser lusje als opende een nieuw lusje.
* In bepaalde omstandigheden kan een langdurige goedkeuringsperiode leiden tot een mislukte implementatie.
