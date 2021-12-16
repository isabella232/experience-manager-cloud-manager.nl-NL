---
title: Git Integration met Adobe Cloud Manager
description: Een videoreeks die door de opstelling en de integratie van een klant-beheerde (op-gebouw) gogegevensopslagplaats met de Manager van de Adobe Cloud loopt.
seo-title: Git Integration with Adobe Cloud Manager
seo-description: A video series that walks through the set up and integration of a customer-managed (on-premise) git repository with Adobe Cloud Manager.
feature: Git Repositories
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 0bc3e775ef2432cdb8d3bd5470953c07c6628148
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# Git Integration met Adobe Cloud Manager

Adobe Cloud Manager wordt geleverd met één git-opslagplaats die wordt gebruikt om code te implementeren via de CI/CD-leidingen van Cloud Manager. Klanten kunnen de git-opslagruimte van Cloud Manager uit de doos gebruiken. Klanten hebben ook de mogelijkheid om een on-premise **door de klant beheerd** Opslagplaats maken met Cloud Manager.

## Overzicht van GIT-integratie

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

In deze videoreeks worden verschillende gebruiksgevallen besproken met betrekking tot de integratie van een door de klant beheerde git-opslagplaats met Cloud Manager, waaronder:

* [Beginsynchronisatie](#initial-sync)
* [Basisvertakkingsstrategie](#branching-strategy)
* [Ontwikkeling van de functiescherm](#feature-development)
* [Implementatie van productie](#production-deployment)
* [Releasetags synchroniseren](#sync-tags)

Voor een volledig overzicht raadpleegt u de [Gebruikershandleiding voor Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) De videoreeks veronderstelt een basiskennis van git en broncontrolebeheer. Zie de [extra bronnen onder](#additional-resources) voor meer informatie over git .

>[!NOTE]
>
> De stappen en naamgevingsconventies die in deze videoreeks worden beschreven, zijn enkele aanbevolen werkwijzen voor het werken met een door de klant beheerde git-opslagplaats en Cloud Manager. Verwacht wordt dat de getoonde conventies en workflows zullen worden aangepast voor individuele ontwikkelingsteams.

## Beginsynchronisatie {#initial-sync}

Eerste stappen voor het synchroniseren van een door de klant beheerde Git-opslagplaats met de Git-opslagplaats van Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Basisvertakkingsstrategie {#branching-strategy}

Een basisvertakkingsstrategie instellen om te profiteren van de voordelen van Cloud Manager [productie- en niet-productiepijpleidingen.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Ontwikkeling van de functiescherm {#feature-development}

Gebruik een eigenschapvertakking om codeveranderingen in een klant-beheerde git bewaarplaats te isoleren en met de git bewaarplaats van de Manager van de Wolk te synchroniseren om een niet productiepijplijn voor codekwaliteit en bevestigingstests te gebruiken.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implementatie van productie {#production-deployment}

Code voorbereiden voor een productievrijgave in een door de klant beheerde it-opslagplaats en synchroniseren met de git-opslagplaats van Cloud Manager om te implementeren in werkgebied- en productieomgevingen.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Releasetags synchroniseren {#sync-tags}

Synchroniseer releasetags van een cloudbeheeropslagplaats naar een door de klant beheerde it-opslagplaats om te bepalen welke code is geïmplementeerd in werkgebied- en productieomgevingen.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Aanvullende bronnen {#additional-resources}

* [Documentatie voor Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)
* [GitHub-bronnen](https://try.github.io)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
