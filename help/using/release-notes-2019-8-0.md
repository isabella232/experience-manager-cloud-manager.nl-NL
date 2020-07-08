---
title: Opmerkingen bij de release 2019.8.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2019.8.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.8.0.
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2019.8.0.
translation-type: tm+mt
source-git-commit: c07e88564dc1419bd0305c9d25173a8e0e1f47cf
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Opmerkingen bij de release 2019.8.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2019.8.0 voegt steun voor selectieve gebouwde inhoudspakketten toe, verbetert bouwstijlprestaties, en lost een verscheidenheid van minder belangrijke insecten op.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.8.0 is 19 augustus 2019.

## What&#39;s New {#whats-new}

* Nieuwe opdrachtregelinterface voor de Cloud Manager-API, aangedreven door de [Adobe I/O-CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager).
* De specifieke inhoudspakketten die door de bouwstijl worden geproduceerd kunnen als skippable worden verklaard en zullen niet worden opgesteld. Raadpleeg de sectie ***Inhoudspakketten*** overslaan in [Een AEM-toepassingsproject](/help/using/create-an-application-project.md) maken voor meer informatie.
* De reeks vooraf geladen gebiedsdelen in de bouwstijlcontainer is herwerkt om sommige onnodige netwerkverzoeken te vermijden.
* Het bericht op de overzichtspagina voor bepaalde verkeerd gevormde programma&#39;s is verbeterd.

## Bug Fixes {#bug-fixes}

* Bij de toegang tot SLA-rapporten was het standaardjaar 2018, niet 2019.
* Voor lange omgevingsnamen is de omgevingskiezer in het scherm Rapporten niet op de juiste wijze groter geworden.
* De ***ConfigAndInstallShouldOnlyContainOsgiNodes*** codekwaliteitsregel produceerde valse positieven toen de het Draaien component Rewriter werd gebruikt.
* De ***ConfigAndInstallShouldOnlyContainOsgiNodes*** codekwaliteitsregel produceerde valse positieven voor bepaalde ongewone wegstructuren.
* Klanten met alleen middelen hebben mogelijk niet consistent kunnen navigeren naar hun AEM-omgevingen.
* Het dialoogvenster Een vertakking maken en Project zijn in verschillende browsers anders weergegeven.
