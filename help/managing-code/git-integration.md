---
title: Git Integration met Adobe Cloud Manager
description: Deze videoreeks doorloopt de opstelling en de integratie van een klant-beheerde (op-gebouw) gogegevensopslagplaats met de Manager van de Adobe Cloud.
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 91e909273bf2b21d7f6413731923011915079e45
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Git Integration met Adobe Cloud Manager

Adobe Cloud Manager wordt geleverd met één git-opslagplaats die wordt gebruikt om code te implementeren via de CI/CD-leidingen van Cloud Manager. U kunt de git-opslagruimte van Cloud Manager offline gebruiken of u hebt ook de mogelijkheid een git-opslagplaats op locatie of door de klant beheerd te integreren met Cloud Manager.

## Overzicht van GIT-integratie

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

In deze videoreeks worden verschillende gebruiksgevallen besproken met betrekking tot de integratie van een door de klant beheerde it-opslagplaats met Cloud Manager.

* [Beginsynchronisatie](#initial-sync)
* [Basisvertakkingsstrategie](#branching-strategy)
* [Ontwikkeling van de functiescherm](#feature-development)
* [Implementatie van productie](#production-deployment)
* [Releasetags synchroniseren](#sync-tags)

Deze videoreeks veronderstelt een basiskennis van git en broncontrolebeheer. Zie de [extra bronnen onder](#additional-resources) voor meer informatie over git .

De stappen en naamgevingsconventies die in deze videoreeks worden beschreven, zijn enkele aanbevolen werkwijzen voor het werken met een door de klant beheerde git-opslagplaats en Cloud Manager. Verwacht wordt dat de getoonde conventies en workflows zullen worden aangepast voor individuele ontwikkelingsteams.

Voor een volledig overzicht van Cloud Manager raadpleegt u het document [Inleiding tot Cloud Manager.](/help/introduction.md)

## Beginsynchronisatie {#initial-sync}

Eerste stappen voor het synchroniseren van een door de klant beheerde it-opslagplaats met de git-opslagplaats van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Basisvertakkingsstrategie {#branching-strategy}

Een basisvertakkingsstrategie instellen om te profiteren van de voordelen van Cloud Manager [productie](/help/using/production-pipelines.md) en [niet-productiepijpleidingen.](/help/using/non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Ontwikkeling van de functiescherm {#feature-development}

Gebruik een eigenschapvertakking om codeveranderingen in een klant-beheerde git bewaarplaats te isoleren en met de git bewaarplaats van de Manager van de Wolk te synchroniseren om een niet productiepijplijn voor codekwaliteit en bevestigingstests te gebruiken.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implementatie van productie {#production-deployment}

Code voorbereiden voor een productievrijgave in een door de klant beheerde it-opslagplaats en synchroniseren met de git-opslagplaats van Cloud Manager om te implementeren in testomgevingen en productieomgevingen.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Releasetags synchroniseren {#sync-tags}

Synchroniseer releasetags van een cloudbeheeropslagplaats naar een door de klant beheerde it-opslagplaats om te bepalen welke code is geïmplementeerd in testomgevingen en productieomgevingen.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Aanvullende bronnen {#additional-resources}

* [Introductie van Cloud Manager](/help/introduction.md)
* [GitHub-bronnen](https://try.github.io)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
