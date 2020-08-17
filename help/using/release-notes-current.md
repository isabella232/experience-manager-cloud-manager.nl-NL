---
title: Opmerkingen bij de release 2020.8.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2020.8.0
description: Volg deze pagina om informatie op te halen voor Cloud Manager Release 2020.8.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2020.8.0
translation-type: tm+mt
source-git-commit: c2f5caf50f2e20c07807369aee7914c17fded4de
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Opmerkingen bij de release 2020.8.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] versie 2020.8.0 beschreven.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2020.8.0 is 6 augustus 2020.

## What&#39;s New {#whats-new}

Verificatie-gebonden Private Maven Repositories worden nu ondersteund.

## Bug Fixes {#bug-fixes}

* Enkele onnodige en ongewenste SonarQube-plug-ins werden uitgevoerd als onderdeel van het scannen van codekwaliteit.

* Op de pagina van de pijpleiding uitvoerde, was de taknaam onjuist geformatteerd.

* Wanneer het opstellen aan topologieën met één enkele publiceren, één enkele verzender en een koude stand-by auteur, werd de verzender fout verwijderd uit het ladingsverdelingsmechanisme.

* In sommige gevallen werden voltooide executies van pijpleidingen niet met succes geregistreerd als voltooid, waardoor nieuwe executies van de pijpleiding werden voorkomen.

* De executies van pijpleidingen zouden af en toe *vastzitten* als gevolg van interne communicatieproblemen.

* De knopinfo op de programmakaarten was niet consistent correct.

* Er is een kleurfout opgetreden op de pagina **Overzicht** .

* Het Testen van de Prestaties van Plaatsen steunt nu het facultatieve gebruik van authentificatie.

* De caches van de verzender voor auteurinstanties worden automatisch leeggemaakt wanneer de berichtconfiguraties door de Manager van de Wolk worden opgesteld.

