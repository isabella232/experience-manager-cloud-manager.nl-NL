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
feature: Geen informatie
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---


# Opmerkingen bij de release voor 2018.9.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie 2018.9.0 voegt steun voor een op Adobe I/O-Gebaseerde API, met inbegrip van Gebeurtenissen toe, voor het integreren van [!UICONTROL Cloud Manager]&#39;s CI/CD pijpleiding met andere systemen. Het begint ook herschrijven van de laag UI in React.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2018.9.0 is November 01, 2018.

## Wat is er nieuw?{#whats-new}

* **CI/CD Pipeline**  - Nieuw API en Gebeurtenissysteem voor het integreren van  [!UICONTROL Cloud Manager]de pijpleiding CI/CD met andere systemen. Raadpleeg de [!UICONTROL Cloud Manager] API-documentatie (https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) voor meer informatie.

* **UI**  - Inleiding van nieuwe laag UI die ontvankelijker is.

## Opgeloste problemen {#bug-fixes}

* In [!UICONTROL Cloud Manager] 2018.8.0, werden de de paginaduur van de Activiteit vermeld in notulen en uren, maar die informatie werd niet weerspiegeld in de lijstkopbal.
* In zeldzame gevallen konden klanten de nieuwe wizard voor toepassingsprojecten niet starten.
* Het knoplabel in het dialoogvenster van de nieuwe wizard voor toepassingsprojecten was misleidend.
* In sommige omstandigheden, zou het klikken van de knoop van Details van de pagina van de Activiteit aan de pagina van het Overzicht opnieuw richten.
* In sommige zeldzame en onverwachte omstandigheden ontbrak een kaart op de overzichtspagina.
* Het pictogram Middelen werd weergegeven op de pagina Program List voor alle klanten.
* Wanneer er achterste eindmislukkingen waren, soms zou een pijpleidingsuitvoering in *Validate* stap lijken te blijven.
* In bepaalde omstandigheden is de duur van de programmabeschrijving onjuist berekend.

## Bekende problemen {#known-issues}

* De takken die gebruikend de Tovenaar van het Project van de Toepassing worden gecreeerd kunnen geen streepjes bevatten.
* De Adobe [!UICONTROL Experience Cloud]-berichtenzijbalk laadt meldingen mogelijk niet consistent. Meldingen zijn echter wel zichtbaar in de Adobe [!UICONTROL Experience Cloud] en worden, indien geconfigureerd, nog steeds verzonden via e-mail.

