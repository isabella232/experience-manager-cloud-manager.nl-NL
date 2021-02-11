---
title: Uw omgevingen beheren
seo-title: Uw omgevingen beheren
description: Meer informatie over de omgeving van Cloud Manager
seo-description: Volg deze pagina om de lijst van productie en non-production milieu's te bekijken die voor vestiging en het in werking stellen van de pijpleiding CI/CD in de Manager van de Wolk worden gebruikt.
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
translation-type: tm+mt
source-git-commit: 2dda85baa5e7ed9bfd8933df3580ec6fc3c210fd
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Uw omgevingen beheren {#manage-your-environments}

De **Overview**-pagina van Cloud Manager bevat de **tile**-tegel die alle beheerde AEM weergeeft.

In elk van de vermelde omgevingen wordt de bijbehorende status weergegeven.

![](assets/Manage-Environ-Overview.png)

## Videozelfstudie {#video-tutorial}

### Overzicht van de omgevingstemperatuur in Cloud Manager {#environ-video}

De volgende video biedt een overzicht van de omgevingen van Cloud Manager die bestaan uit instanties van AEM-auteurs, AEM-publicaties en Dispatcher.

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## Toegang tot omgevingen in Cloud Manager {#accessing-environments-in-cloud-manager}

De **Omgevingen** tegel toont de Productie en de milieu&#39;s van het Stadium die in uw programma samen met de status worden voorzien.

De status is de toestand van het opgerold vermogen over de knooppunten in de omgeving. Het is groen als alle knopen lopen, rood als zelfs één knoop wordt tegengehouden, blauw als zelfs één knoop omhoog komt, en geel als zelfs één knoop een machtstoestand niet beschikbaar (in deze orde van prioriteit) heeft.

![](assets/Environments-card-new.png)

### Omgevingen {#environments}

Klik **Beheren** om het scherm **Omgevingen** weer te geven.

In het scherm **Omgevingen** wordt een kaart weergegeven voor elke *Productie*- en *Stage*-omgeving (indien van toepassing) in uw programma. De naam van de omgeving wordt boven elke kaart weergegeven. De kaart omvat een lijst van knopen in het milieu samen met de t-shirtgrootte van cpu, de opslag, het gebied, en de status.

>[!NOTE]
>
>De **STATUS** van het knooppunt vertegenwoordigt de energietoestand van de VM en geeft niet de status van AEM op de server weer. De status kan **Running** (groene cirkel), **Gestopt** (rode cirkel), **Komend omhoog** (blauwe cirkel) of **Niet beschikbaar** (gele cirkel) zijn.

![](assets/Environments-tab.png)
