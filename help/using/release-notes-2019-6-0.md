---
title: Opmerkingen bij de release 2019.6.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2019.6.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.6.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.6.0.
translation-type: tm+mt
source-git-commit: 7cfa0cf66efd5891263bfcc83a5149daec5c8b67

---

# Opmerkingen bij de release 2019.6.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie 2019.6.0 voegt nieuwe regels van de codekwaliteit en de nieuwe tovenaar van de Update van het Product toe. Volg de onderstaande secties voor meer informatie.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.6.0 is 20 juni 2019 .

## Nieuwe functies {#whats-new}

* De wizard Nieuwe productupdate helpt klanten een AEM-update uit te voeren. Raadpleeg de wizard [](overview-productupdate-wizard.md) Productupdates voor meer informatie.
* Regels voor de kwaliteit van de code die de structuur van de inhoud onderzoeken. Raadpleeg de kwaliteitsregels [voor](custom-code-quality-rules.md) aangepaste code voor meer informatie.
* De maximale grootte van een git-push is verhoogd tot 1 GB.

## Opgeloste problemen {#bug-fixes}

* In sommige gevallen konden geen pijpleidingen worden gestart vanwege een eerdere storing.

## Bekende problemen {#known-issues}

* De CSV-download van de codekwaliteit wordt niet altijd gesorteerd op ernst.
* De valse positieven kunnen door de regel *ConfigAndInstallShouldOnlyContainOsgiNodes* worden gemeld als de configuraties OSGi in een genestelde omslag onder een *config* omslag worden geplaatst.