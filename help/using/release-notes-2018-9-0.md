---
title: Opmerkingen bij de release 2018.9.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2018.9.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2018.9.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2018.9.0.
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: ace032fbb26235d87d61552a11996ec2bb42abce
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Opmerkingen bij de release 2018.9.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2018.9.0 voegt steun voor een op Adobe I/O-Gebaseerde API, met inbegrip van Gebeurtenissen toe, voor het integreren [!UICONTROL Cloud Manager]van CI/CD pijpleiding van CI/CD met andere systemen. Het begint ook herschrijven van de laag UI in React.

## Releasedatum {#release-date}

De Releasedatum voor [!UICONTROL Cloud Manager] versie 2018.9.0 is 1 november 2018.

## What&#39;s New {#whats-new}

* **CI/CD Pipeline** - Nieuw API en Gebeurtenissysteem voor het integreren van [!UICONTROL Cloud Manager]de pijpleiding CI/CD met andere systemen. Raadpleeg de documentatie bij de [!UICONTROL Cloud Manager] API (https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) voor meer informatie.

* **UI** - Inleiding van nieuwe laag UI die ontvankelijker is.

## Bug Fixes {#bug-fixes}

* In [!UICONTROL Cloud Manager] 2018.8.0, werden de de paginaduur van de Activiteit vermeld in notulen en uren, maar die informatie werd niet weerspiegeld in de lijstkopbal.
* In zeldzame gevallen konden klanten de nieuwe wizard voor toepassingsprojecten niet starten.
* Het knoplabel in het dialoogvenster van de nieuwe wizard voor toepassingsprojecten was misleidend.
* In sommige omstandigheden, zou het klikken van de knoop van Details van de pagina van de Activiteit aan de pagina van het Overzicht opnieuw richten.
* In sommige zeldzame en onverwachte omstandigheden ontbrak een kaart op de overzichtspagina.
* Het pictogram Middelen werd weergegeven op de pagina Program List voor alle klanten.
* Wanneer er achtereind mislukkingen waren, soms zou een pijpleidingsuitvoering in de *Validate* stap lijken te blijven.
* In bepaalde omstandigheden is de duur van de programmabeschrijving onjuist berekend.

## Bekende problemen {#known-issues}

* De takken die gebruikend de Tovenaar van het Project van de Toepassing worden gecreeerd kunnen geen streepjes bevatten.
* Op de zijbalk met meldingen van Adobe kunnen meldingen mogelijk niet consistent worden geladen. [!UICONTROL Experience Cloud] Meldingen zijn echter wel zichtbaar in de Adobe [!UICONTROL Experience Cloud] en worden, indien geconfigureerd, nog steeds verzonden via e-mail.

