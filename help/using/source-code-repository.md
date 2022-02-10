---
title: Broncodeopslagplaats
seo-title: Source Code Repository for Adobe AEM Cloud Manager
description: Volg deze pagina voor meer informatie over de git-opslagplaats die is ingericht voor elk programma dat u hebt in Cloud Manager.
seo-description: Follow this page to learn about the git repository that is provisioned for each program you have in Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: Provisioning
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# Broncodeopslagplaats {#source-code-repository}

## Opslagplaats voor wolkenbeheer {#cloud-manager-repository}

Uw [!UICONTROL AEM Managed Services] het abonnement zal een opslagplaats van de broncode omvatten provisioned en beheerd door Adobe. Aan elk programma van de klant wordt één en uniek toegewezen **Git Repository**, waar de gekoppelde code wordt opgeslagen en beveiligd.

Als beste praktijken, zou u altijd de Bewaarplaats van de Bewaarplaats van de Bezit van de Bediener van de Bediener van de Bediener van de Manager van de Wolk moeten gebruiken, die leeg zonder enige gevormde takken of steekproefprojecten komt. Als u de Git Repository van Cloud Manager wilt gebruiken, ontvangt u een **persoonlijke toegangstoken** Hiermee kunt u elke Git-compatibele client gebruiken om vertakkingen te maken, uw code op te slaan en op te halen, de geschiedenis van de commit weer te geven, enzovoort.

Voor meer informatie over hoe te om takken in Git te plaatsen, zie [De vertakkingen van uw Versie configureren](configure-your-release-branches.md).

Voor meer informatie over het gebruik van Cloud Manager **Git Repository** met de CI/CD pijpleiding, gelieve te verwijzen naar de documenten [Productiepijpleidingen configureren](configuring-production-pipelines.md) en [Niet-productiepijpleidingen configureren](configuring-non-production-pipelines.md) voor meer informatie.

## Bewaarplaats op locatie {#on-premise-repository}

In sommige gevallen hebt u een bestaande Git Repository en wilt u deze blijven gebruiken. In deze gevallen kunt u de ondersteunde functie van Git gebruiken voor meerdere externe opslagruimten. De ontwikkeling van dag tot dag zou in uw Git Repository blijven plaatsvinden. Wanneer een releasevertakking gereed is voor implementatie op productie, drukt u de nieuwste code naar de Git-opslagplaats van Cloud Manager en activeert u de CI/CD-pijplijn van Cloud Manager.

>[!NOTE]
>
>Als u de algemene opdrachten voor Git wilt weergeven, raadpleegt u de [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf).
