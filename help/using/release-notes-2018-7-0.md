---
title: Opmerkingen bij de release 2018.7.0
seo-title: Opmerkingen bij de release 2018.7.0
description: 'null'
seo-description: Volg deze pagina voor informatie over Cloud Manager Release 2018.7.0.
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
translation-type: tm+mt
source-git-commit: ace032fbb26235d87d61552a11996ec2bb42abce
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---


# Opmerkingen bij de release voor 2018.7.0 {#release-notes-for}

In de volgende sectie wordt de [!UICONTROL Cloud Manager] 2018.7.0-release beschreven die *autoscaling*-functie biedt.

**** Autoscalingis toegelaten via horizontale schaal-uit van  `Dispatcher/Publish` segmenten op het productiemilieu om een plotselinge verhoging van lading, volume, toegang, en andere bepaalde gecontroleerde metriek te steunen.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2018.7.0 is 10 september 2018.

## Wat is er nieuw?{#what-s-new}

* **Levering**  -  [!UICONTROL Cloud Manager] zal nu de capaciteit hebben autoscale de productieomgeving op het klantenprogramma door horizontaal uit te schrapen met de segmenten van de Verzender/van de Publicatie. Nieuw in UI is de sectie van de Levering in de Opstelling van het Programma die zal tonen als autoscaling op het klantenprogramma wordt toegelaten. Gelieve te verwijzen naar [Opstelling uw Programma](setting-up-program.md) om meer te leren.

* **Milieu**  - Het is nu mogelijk om een gedetailleerde mening van Productie en de milieu&#39;s van het Stadium samen met de grootte, de opslag, het gebied, en de status van de knopen te zien verbonden aan elke milieu. Raadpleeg [Uw omgevingen beheren](manage-your-environment.md) voor meer informatie.

* **Analyse**  van de Kwaliteit van de code - Nieuwe regel om onjuist API gebruik te identificeren. Raadpleeg [Aangepaste regels voor codekwaliteit](custom-code-quality-rules.md) voor meer informatie.

* **Prestaties testen**  - Tijdens het bekijken van de resultaten van prestatietests zijn grafieken voor CPU-gebruik, schijf-I/O-wachttijd, Paginafout, schijfbreedtegebruik, Netwerkbandbreedtegebruik, Piek-pagina responstijd en responstijd van 95e percentiele pagina beschikbaar. Raadpleeg de sectie *Prestaties testen* op [De pagina Testresultaten begrijpen](understand-your-test-results.md).

* **Prestatietesten**  - Tijdens het bekijken van de testresultaten voor de prestaties kan de lijst met paginafouten en trage aanvragen worden gedownload. Raadpleeg de sectie *Prestaties testen* op [De pagina Testresultaten begrijpen](understand-your-test-results.md).

## Opgeloste problemen {#bug-fixes}

* In bepaalde omstandigheden is interne systeemsynchronisatie onjuist mislukt, wat leidt tot inconsistente weergaven van gegevens.
* In sommige gevallen is de handmatige trigger voor de pijplijn niet automatisch geselecteerd, wat leidt tot validatieproblemen.
* De specifieke klant bouwt manuscripten zou mislukkingen tijdens de bouwstijlstap kunnen veroorzaken die op plugin onverenigbaarheden wordt gebaseerd.

## Bekende problemen {#known-issues}

* Hoewel de klanten kunnen selecteren begaat trekker, kan de pijpleiding niet eigenlijk beginnen gebaseerd op nieuwe verbintenissen.
* De meldingszijbalk [!UICONTROL Experience Cloud] laadt meldingen mogelijk niet consistent. Meldingen zijn echter zichtbaar in [!UICONTROL Experience Cloud] en worden, indien geconfigureerd, nog steeds verzonden via e-mail.

