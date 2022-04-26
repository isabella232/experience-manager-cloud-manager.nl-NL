---
title: Uw omgevingen beheren
seo-title: Manage your Environments
description: Meer informatie over de omgeving van Cloud Manager
seo-description: Follow this page to view the list of production and non-production environments that are used for setting up and running the CI/CD pipeline in Cloud Manager.
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: Environments
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 6ff704ec11dd4a5f73d5b5df5721c4fee649527b
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Uw omgevingen beheren {#manage-your-environments}

>[!NOTE]
>Ga voor meer informatie over het beheren van omgevingen voor Cloud Manager in AEM as a Cloud Service naar [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#using-cloud-manager).

De **Overzicht** bevat de pagina met Cloud Manager de **Omgevingen** tegel die van alle beheerde AEM milieu&#39;s een lijst maakt.

In elk van de vermelde omgevingen wordt de bijbehorende status weergegeven.

![](assets/Manage-Environ-Overview.png)

## Videozelfstudie {#video-tutorial}

### Overzicht van Cloud Manager-omgeving {#environ-video}

De volgende video biedt een overzicht van de omgevingen van Cloud Manager die bestaan uit instanties van AEM-auteurs, AEM-publicaties en Dispatcher.

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## Toegang tot omgevingen in Cloud Manager {#accessing-environments-in-cloud-manager}

De **Omgevingen** De tegel geeft de productie- en werkgebiedomgevingen weer die samen met de status in uw programma zijn opgenomen.

De status is de toestand van het opgerold vermogen over de knooppunten in de omgeving. Het is groen als alle knopen lopen, rood als zelfs één knoop wordt tegengehouden, blauw als zelfs één knoop omhoog komt, en geel als zelfs één knoop een machtstoestand niet beschikbaar (in deze orde van prioriteit) heeft.

![](assets/Environments-card-new.png)

### Omgevingen {#environments}

Klikken **Beheren** om de **Omgevingen** scherm.

De **Omgevingen** scherm geeft een kaart weer voor *Productie* en *Werkgebied* omgevingen (zoals van toepassing) in uw programma. De naam van de omgeving wordt boven elke kaart weergegeven. De kaart omvat een lijst van knopen in het milieu samen met de t-shirtgrootte van cpu, de opslag, het gebied, en de status.

>[!NOTE]
>
>De **STATUS** van het knooppunt staat voor de energiestatus van de VM en geeft niet de status van AEM op de server weer. De status kan **Wordt uitgevoerd** (groene cirkel), **Gestopt** (rode cirkel), **Opstaan** (blauwe cirkel) of **Niet beschikbaar** (gele cirkel).

![](assets/Environments-tab.png)

>[!NOTE]
>
>Als u uw omgevingslogboeken nodig hebt, kunnen deze worden aangevraagd via uw Customer Success Engineer.
