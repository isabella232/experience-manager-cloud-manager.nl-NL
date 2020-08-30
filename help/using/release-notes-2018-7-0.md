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
ht-degree: 0%

---


# Opmerkingen bij de release 2018.7.0 {#release-notes-for}

In de volgende sectie wordt de release [!UICONTROL Cloud Manager] 2018.7.0 beschreven die *functie voor automatisch schalen* biedt.

**Autoscaling** wordt toegelaten via horizontale schaal-uit van `Dispatcher/Publish` segmenten op het productiemilieu om een plotselinge verhoging van lading, volume, toegang, en andere bepaalde gecontroleerde metriek te steunen.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2018.7.0 is 10 september 2018.

## What&#39;s New {#what-s-new}

* **Levering** - [!UICONTROL Cloud Manager] zal nu de capaciteit hebben autoscale de productiemilieu op het klantenprogramma door horizontaal uit te schrapen met de segmenten van de Verzender/van de Publicatie. Nieuw in UI is de sectie van de Levering in de Opstelling van het Programma die zal tonen als autoscaling op het klantenprogramma wordt toegelaten. Gelieve te verwijzen naar [Opstelling uw Programma](setting-up-program.md) om meer te leren.

* **Omgevingen** - Het is nu mogelijk om een gedetailleerde weergave van Productie- en Stage-omgevingen te bekijken, samen met de grootte, opslag, regio en status van de knooppunten die aan elke omgeving zijn gekoppeld. Raadpleeg [Uw omgevingen](manage-your-environment.md) beheren voor meer informatie.

* **Codekwaliteitsanalyse** - Nieuwe regel om onjuist API-gebruik te identificeren. Raadpleeg de kwaliteitsregels voor [aangepaste code](custom-code-quality-rules.md) voor meer informatie.

* **Prestaties testen** - Tijdens het bekijken van de resultaten van prestatietests zijn grafieken voor CPU-gebruik, schijf-I/O-wachttijd, Paginafout snelheid, schijfbandbreedtegebruik, Netwerkbandbreedtegebruik, Piek-pagina responstijd en responstijd van 95e percentiele pagina beschikbaar. Raadpleeg de sectie *Prestaties testen* op de pagina [Testresultaten](understand-your-test-results.md) begrijpen.

* **Prestatietesten** - Tijdens het bekijken van de testresultaten voor de prestaties kan de lijst met paginafouten en trage aanvragen worden gedownload. Raadpleeg de sectie *Prestaties testen* op de pagina [Testresultaten](understand-your-test-results.md) begrijpen.

## Bug Fixes {#bug-fixes}

* In bepaalde omstandigheden is interne systeemsynchronisatie onjuist mislukt, wat leidt tot inconsistente weergaven van gegevens.
* In sommige gevallen is de handmatige trigger voor de pijplijn niet automatisch geselecteerd, wat leidt tot validatieproblemen.
* De specifieke klant bouwt manuscripten zou mislukkingen tijdens de bouwstijlstap kunnen veroorzaken die op plugin onverenigbaarheden wordt gebaseerd.

## Bekende problemen {#known-issues}

* Hoewel de klanten kunnen selecteren begaat trekker, kan de pijpleiding niet eigenlijk beginnen gebaseerd op nieuwe verbintenissen.
* Meldingen worden mogelijk niet consistent geladen op de [!UICONTROL Experience Cloud] berichtzijbalk. Meldingen zijn echter wel zichtbaar in de map [!UICONTROL Experience Cloud] en worden, indien geconfigureerd, nog steeds verzonden via e-mail.

