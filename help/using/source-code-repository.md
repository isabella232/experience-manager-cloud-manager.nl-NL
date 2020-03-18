---
title: Broncodeopslagplaats
seo-title: Inschrijving als broncode voor Adobe AEM Cloud Manager
description: Volg deze pagina voor meer informatie over de git-opslagplaats die is ingericht voor elk programma dat u hebt in Cloud Manager.
seo-description: Volg deze pagina voor meer informatie over de git-opslagplaats die is ingericht voor elk programma dat u hebt in Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
translation-type: tm+mt
source-git-commit: 697311cd00ef96568f6befd2fe76febafc27961e

---


# Broncodeopslagplaats {#source-code-repository}

## Opslagplaats voor wolkenbeheer {#cloud-manager-repository}

Uw [!UICONTROL AEM Managed Services] abonnement bevat een opslagplaats voor broncode die is ingericht en beheerd door Adobe. Aan het programma van elke klant wordt één en unieke **Git Repository** toegewezen, waar uw bijbehorende code wordt opgeslagen en beveiligd.

Als beste praktijken, zou u altijd de Bewaarplaats van de Bewaarplaats van de Bezit van de Bediener van de Bediener van de Bediener van de Manager van de Wolk moeten gebruiken, die leeg zonder enige gevormde takken of steekproefprojecten komt. Als u de Git Repository van Cloud Manager wilt gebruiken, ontvangt u een **privétoegangstoken** waarmee u elke met Git compatibele client kunt gebruiken om vertakkingen te maken, uw code op te slaan en op te halen, de geschiedenis van de commit weer te geven, enz.

Voor meer informatie over hoe te opstellingstakken in Git, zie het [Vormen van uw Tanden](configure-your-release-branches.md)van de Versie.

Voor meer informatie over hoe te om de Bewaarplaats van de Bewaarplaats **van de Bezit van de Bediener van de Bediener van de Bediener van de** Bediener [van de Bediener van de Bediener van de Bediener van de Wolk met CI/CD te gebruiken, zie het](configuring-pipeline.md)Vormen van uw pijpleidingCI/CD.

## Bewaarplaats op locatie {#on-premise-repository}

In sommige gevallen hebt u een bestaande Git Repository en wilt u deze blijven gebruiken. In deze gevallen kunt u de ondersteunde functie van Git gebruiken voor meerdere externe opslagruimten. De ontwikkeling van dag tot dag zou in uw Git Repository blijven plaatsvinden. Wanneer een releasevertakking gereed is voor implementatie op productie, drukt u de nieuwste code naar de Git-opslagplaats van Cloud Manager en activeert u de CI/CD-pijplijn van Cloud Manager.

>[!NOTE]
>
>Zie het [stramienblad](https://education.github.com/git-cheat-sheet-education.pdf)voor informatie over de algemene opdrachten voor Git.

