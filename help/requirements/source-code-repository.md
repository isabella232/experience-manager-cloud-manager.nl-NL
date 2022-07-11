---
title: Broncodeopslagplaats
description: Meer informatie over de git-opslagruimte die is ingericht voor elk programma dat u hebt in Cloud Manager.
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# Broncodeopslagplaats {#source-code-repository}

Meer informatie over de git-opslagruimte die is ingericht voor elk programma dat u hebt in Cloud Manager.

## Opslagplaats voor wolkenbeheer {#cloud-manager-repository}

Uw [!UICONTROL AEM Managed Services] het abonnement omvat een opslagplaats van de broncode provisioned en beheerd door Adobe. Aan elk programma wordt één enkele en unieke it-opslagplaats toegewezen, waar uw bijbehorende code wordt opgeslagen en beveiligd.

Als beste praktijken, zou u altijd de git bewaarplaats van de Manager van de Wolk moeten gebruiken, die leeg zonder om het even welke gevormde takken of steekproefprojecten komt. Als u de git-opslagplaats van Cloud Manager wilt gebruiken, ontvangt u een token voor persoonlijke toegang waarmee u elke willekeurige git-client kunt gebruiken voor het maken van vertakkingen, het opslaan en ophalen van uw code, het vastleggen van de geschiedenis, enzovoort.

Voor meer informatie over hoe te om takken in git te plaatsen, zie [Release-vertakkingen configureren.](/help/getting-started/configuring-branches.md)

Raadpleeg de documenten voor meer informatie over het gebruik van de git-opslagplaats van Cloud Manager met de CI/CD-pijplijn [Productiepijpleidingen configureren](/help/using/production-pipelines.md) en [Niet-productiepijpleidingen configureren](/help/using/non-production-pipelines.md) voor meer informatie.

## Bewaarplaats op locatie {#on-premise-repository}

U hebt mogelijk een bestaande git-opslagplaats en wilt deze blijven gebruiken. In dat geval kunt u de git-functie gebruiken voor meerdere externe opslagruimten. De ontwikkeling van dag tot dag zou in uw git-opslagplaats blijven plaatsvinden. Wanneer een releasevertakking gereed is voor implementatie op productie, kunt u de nieuwste code naar de git-opslagplaats van Cloud Manager drukken en de Cloud Manager CI/CD-pijplijn activeren.

Als u de algemene opdrachten voor de it wilt weergeven, raadpleegt u de [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf) op de GitHub-website.
