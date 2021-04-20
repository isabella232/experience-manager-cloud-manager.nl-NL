---
title: Opmerkingen bij de release 2019.6.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2019.6.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.6.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.6.0.
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# Opmerkingen bij de release voor 2019.6.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie 2019.6.0 voegt nieuwe regels van de codekwaliteit en nieuwe tovenaar van de Update van het Product toe. Volg de onderstaande secties voor meer informatie.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.6.0 is 20 juni 2019.

## Wat is er nieuw?{#whats-new}

* De nieuwe wizard Productupdates helpt klanten een AEM update uit te voeren. Raadpleeg [Wizard Productupdates](overview-productupdate-wizard.md) voor meer informatie.
* Regels voor de kwaliteit van de code die de structuur van de inhoud onderzoeken. Raadpleeg [Aangepaste regels voor codekwaliteit](custom-code-quality-rules.md) voor meer informatie.
* De maximale grootte van een git-push is verhoogd tot 1 GB.

## Opgeloste problemen {#bug-fixes}

* In sommige gevallen konden geen pijpleidingen worden gestart vanwege een eerdere storing.

## Bekende problemen {#known-issues}

* De CSV-download van de codekwaliteit wordt niet altijd gesorteerd op ernst.
* De valse positieven kunnen door de *regel ConfigAndInstallShouldOnlyContainOsgiNodes* worden gemeld als de configuraties OSGi in een genestelde omslag onder een *config* omslag worden geplaatst.