---
title: Opmerkingen bij de release 2019.1.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2019.1.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.1.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.1.0.
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Opmerkingen bij de release 2019.1.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2018.9.0 voegt steun het testen van de programma&#39;s van AEM Assets evenals extra pijpleidingstypes toe die de bouw en de stappen van de codekwaliteit in werking stellen, naar keuze opstellend aan een niet productiemilieu.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.1.0 is 17 januari 2019.

## What&#39;s New {#whats-new}

* Extra ondersteuning voor het testen van prestaties van AEM Assets. Gelieve te verwijzen om uw [CI/CD](configuring-pipeline.md)Pijler voor meer details te vormen.
* Toegevoegde ondersteuning voor pijpleidingen die alleen stappen van de bouw- en codekwaliteit uitvoeren en voor pijpleidingen die worden geïmplementeerd in niet-productieomgevingen. Gelieve te verwijzen naar **niet-Productie &amp; de sectie van de Kwaliteit van de Code slechts Pijpleidingen** in [Vorm uw CI/CD pijpleiding](configuring-pipeline.md) voor meer details.
* Extra ondersteuning voor aangepaste omgevingsvariabelen in de ontwikkelomgeving.
* Voor klanten met veelvoudige stadium of productiemilieu&#39;s, is de selectie van welk milieu als deel van de productiepijplijn zal worden opgesteld beschikbaar in [Vorm uw Cc/CD pagina van de Pijpleiding](configuring-pipeline.md) .
* httxt2dbm is toegevoegd om container te bouwen.
* Met alle Help-menu-items wordt een nieuw tabblad geopend.

## Bug Fixes {#bug-fixes}

* Tijdens het bewerken van een programma kon de selectie van alle paginasets ongedaan worden gemaakt.
* De goedkeuringsstap heeft een onjuiste naam.
* In sommige situaties is de matte van het programmalogo onjuist.
* Als alleen het pakket voor de configuratie van de verzender is gemaakt, mislukt de implementatiestap.
* Omgevingen die koude stand-by-instanties bevatten, werden niet correct verwerkt.
* Sommige beëindigde programma&#39;s verschenen op de programmaschakelaar.
* Als een nieuwe tak aan de git bewaarplaats werd toegevoegd terwijl de pijpleiding werd uitgegeven, kan het niet onmiddellijk selecteerbaar zijn geweest.
* Op sommige schermen was het pictogram Developer Connection in het menu Help niet zichtbaar.
* De tabtoets is niet correct verwerkt in het dialoogvenster voor het leegmaken van de verzendingsprogramma.

## Bekende problemen {#known-issues}

* Wanneer het openen van een programma dat Plaatsen, maar niet Activa heeft, geplaatst KPIs, zien alle gebruikers een vraag aan actiekaart met een knoop van het Programma **van de** Opstelling. Nochtans, slechts kunnen de gebruikers in de rol Bedrijfs van de Eigenaar eigenlijk op de knoop van het Programma **van de** Opstelling klikken.