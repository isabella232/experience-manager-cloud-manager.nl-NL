---
title: Opmerkingen bij de release 2020.8.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2020.8.0
description: Volg deze pagina om informatie op te halen voor Cloud Manager Release 2020.8.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2020.8.0
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# Opmerkingen bij de release voor 2020.8.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2020.8.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2020.8.0 is Augustus 06, 2020.

## Wat is er nieuw?{#whats-new}

Verificatie-gebonden Private Maven Repositories worden nu ondersteund.

## Opgeloste problemen {#bug-fixes}

* Enkele onnodige en ongewenste SonarQube-plug-ins werden uitgevoerd als onderdeel van het scannen van codekwaliteit.

* Op de pagina van de pijpleiding uitvoerde, was de taknaam onjuist geformatteerd.

* Wanneer het opstellen aan topologieën met één enkele publiceren, één enkele verzender en een koude stand-by auteur, werd de verzender fout verwijderd uit het ladingsverdelingsmechanisme.

* In sommige gevallen werden voltooide executies van pijpleidingen niet met succes geregistreerd als voltooid, waardoor nieuwe executies van de pijpleiding werden voorkomen.

* Uitvoeringen van pijpleidingen zouden soms *geplakt* worden als gevolg van interne communicatieproblemen.

* De knopinfo op de programmakaarten was niet consistent correct.

* Er is een kleurfout opgetreden op de pagina **Overzicht**.

* Het Testen van de Prestaties van Plaatsen steunt nu het facultatieve gebruik van authentificatie.

* De caches van de verzender voor auteurinstanties worden automatisch leeggemaakt wanneer de berichtconfiguraties door de Manager van de Wolk worden opgesteld.

