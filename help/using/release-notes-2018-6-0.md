---
title: Opmerkingen bij de release 2018.6.0
seo-title: AEM Cloud Manager Release Notes for 2018.6.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2018.6.0.
seo-description: Follow this page to get information for AEM Cloud Manager Release 2018.6.0.
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
feature: Release Information
exl-id: 456f7892-c64c-4b3f-b845-15682d034aaa
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Opmerkingen bij de release 2018.6.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release beschreven voor [!UICONTROL Cloud Manager] Versie 2018.6.0 en voegt ondersteuning toe voor invalidatie van de verzender tijdens implementaties, extra meldingen en verbeteringen in de bruikbaarheid.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] Versie 2018.6.0 is 9 augustus 2018.

## Wat is er nieuw? {#what-s-new}

* **CI/CD Pipet** - Configureerbare validatie van de Ontvanger van de Dispatcher en het Blozen van het Geheime voorgeheugen op zowel Stadium als Productie tijdens CI/CD de uitvoering van de Pijpleiding. Raadpleeg het document [Productiepijpleidingen configureren](configuring-production-pipelines.md) voor meer informatie.

* **CI/CD Pipet** - Tijdens de opstelling van de pijpleiding, is het nu mogelijk om te bepalen hoe de pijpleiding zich zal gedragen wanneer het een Belangrijke mislukking in één van de kwaliteitspoorten ontmoet. Raadpleeg het document [Productiepijpleidingen configureren](configuring-production-pipelines.md) voor meer informatie.

* **CI/CD Pipet** - Tijdens pijpleidingsopstelling, is het nu mogelijk om te selecteren of u CSE Toezicht door uw CSE of om het even welke beschikbare CSE wilt worden uitgevoerd. Raadpleeg het document [Productiepijpleidingen configureren](configuring-production-pipelines.md) voor meer informatie.

* **CI/CD Pipet** - Wanneer de CI/CD pijpleiding de bedrijfsgoedkeuringsstap bereikt, zal een bericht worden verzonden naar gebruikers die worden gemachtigd om de plaatsing goed te keuren. Zie [Meldingen](notifications.md) voor meer informatie.

* **CI/CD Pipet** - Wanneer de CI/CD pijpleiding het vastgestelde programma bereikt, zal een bericht worden verzonden naar gebruikers die worden gemachtigd om het programma te plaatsen. Zie [Meldingen](notifications.md) voor meer informatie.

* **Codekwaliteitsanalyse** - Nieuwe regels om onjuist geconfigureerde uitgaande HTTP/HTTPS-aanvragen te identificeren. Zie [Aangepaste regels voor codekwaliteit](custom-code-quality-rules.md) voor meer informatie.

## Opgeloste problemen {#bug-fixes}

* In sommige gevallen is de prestatietest niet volledig verdeeld over meerdere verzenders en publicatieinstanties.
* Koptekstnavigatie is verdwenen in smalle browservensters.
* Sommige pijpleidingsmontages werden niet onbruikbaar gemaakt terwijl de pijpleiding liep.
* De verbindingen aan AEM en Controle van het lijstscherm van het Programma vervingen zowel het huidige browser lusje als opende een nieuw lusje.
* In bepaalde omstandigheden kan een langdurige goedkeuringsperiode leiden tot een mislukte implementatie.
