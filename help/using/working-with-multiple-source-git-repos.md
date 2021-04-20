---
title: Werken met Meerdere bronopslaglocaties voor Git
description: Werken met Meerdere bronopslaglocaties voor Git - Cloud Manager
feature: Git Repositories
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# Werken met meerdere bronopslagplaatsen voor Git {#working-with-multiple-source-git-repos}


## Door de klant beheerde Git-opslagplaatsen synchroniseren {#syncing-customer-managed-git-repositories}

In plaats van rechtstreeks met de Git-opslagplaats van Cloud Manager te werken, kunnen klanten met hun eigen Git-opslagplaats of meerdere eigen Git-opslagruimten werken. In deze gevallen moet een geautomatiseerd synchronisatieproces worden ingesteld om ervoor te zorgen dat de Git-opslagplaats van Cloud Manager altijd wordt bijgewerkt. Afhankelijk van waar de gegevensopslagplaats van het Git van de klant wordt ontvangen, zou een actie GitHub of een ononderbroken integratieoplossing zoals Jenkins aan opstelling de automatisering kunnen worden gebruikt. Met een automatische installatie kan elke push naar een Git-opslagplaats in eigendom van een klant automatisch worden doorgestuurd naar de Git-opslagplaats van Cloud Manager.

Hoewel een dergelijke automatisering voor een Git-opslagplaats die eigendom is van één klant, meteen doorgaat, is een eerste installatie vereist om dit voor meerdere opslagplaatsen in te stellen. De inhoud van de meerdere Git-opslagplaatsen moet worden toegewezen aan verschillende mappen in de Git-opslagplaats van Cloud Manager.  De Git-opslagruimte van Cloud Manager moet worden ingericht met een pom met hoofdmap Maven, waarin de verschillende subprojecten worden vermeld in de sectie Modules

Hieronder ziet u een voorbeeldpom voor twee Git Repositories in eigendom van klanten: het eerste project zal in de folder genoemd `project-a` worden gezet, wordt het tweede project gezet in de folder genoemd `project-b`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
  
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
  
</project>
```

Een dergelijke hoofdpom wordt naar een vertakking verplaatst in de Git Repository van Cloud Manager. Vervolgens moeten de twee projecten worden ingesteld om wijzigingen automatisch door te sturen naar de Git Repository van Cloud Manager.

Bijvoorbeeld, kan een actie GitHub door een duw aan een tak in project A worden teweeggebracht. De actie evalueert project A en de gegevensopslagplaats van de Git van de Manager van de Wolk en kopieert alle inhoud van project A aan de folder `project-a` in de Opslagbewaarplaats van de Manager van de Wolk van de Wolk en dan verbind-duw de verandering. Een wijziging in de hoofdvertakking in project A wordt bijvoorbeeld automatisch doorgevoerd in de hoofdvertakking in de git-opslagplaats van Cloud Manager. Natuurlijk zou er een afbeelding tussen takken als een duw aan een tak kunnen zijn genoemd &quot;dev&quot;in project A wordt geduwd aan een tak genoemd &quot;ontwikkeling&quot;in de bewaarplaats van de it van de Manager van de Wolk. Vergelijkbare stappen zijn vereist voor project B.

Afhankelijk van de vertakkingsstrategie en workflows kan de synchronisatie worden geconfigureerd voor verschillende vertakkingen. Als de gebruikte gegevensopslagplaats van de Git geen concept gelijkend op acties GitHub verstrekt, is een integratie via (of gelijkaardig) Jenkins ook mogelijk. In dit geval activeert een webhaak een Jenkins-taak die het werk doet.

Voer de onderstaande stappen uit om een nieuwe (derde) bron of opslagplaats toe te voegen:

1. Voeg een nieuwe actie GitHub aan de nieuwe bewaarplaats toe die veranderingen van die Bewaarplaats in de Bewaarplaats van de Bewaarplaats van de Bewaarplaats van de Bediener van de Bewaarplaats van de Manager van de Wolk duwt.
1. Voer die actie ten minste één keer uit om ervoor te zorgen dat de projectcode zich in de Git Repository van de Manager van de Wolk bevindt.
1. Voeg een verwijzing naar de nieuwe map toe aan de pom Maven van de hoofdmap in de gegevensopslagruimte van Cloud Manager.


## Voorbeeld van GitHub-actie {#sample-github-action}

Dit is een voorbeeld van een GitHub-actie die wordt geactiveerd door een push naar de hoofdvertakking en die vervolgens wordt doorgedrukt in een submap van de Git Repository van Cloud Manager. De GitHub-acties moeten worden voorzien van twee geheimen, `MAIN_USER` en `MAIN_PASSWORD`, om verbinding te kunnen maken met en druk op de Git-opslagplaats van Cloud Manager.

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

Zoals hierboven getoond, is het gebruiken van een actie GitHub zeer flexibel. Elke toewijzing tussen vertakkingen van de Git-opslagplaatsen kan worden uitgevoerd en elke toewijzing van de afzonderlijke it-projecten aan de mappenlay-out van het hoofdproject.

>[!NOTE]
>In het bovenstaande script wordt `git add` gebruikt om de gegevensopslagruimte bij te werken, waarbij ervan wordt uitgegaan dat verwijderingen worden opgenomen. Afhankelijk van de standaardconfiguratie van Git moet dit worden vervangen door `git add --all`.

## Voorbeeld van Jenkins-taak {#sample-jenkins-job}

Dit is een voorbeeldscript dat kan worden gebruikt in een Jenkins-taak of vergelijkbaar. Het wordt geactiveerd door een wijziging in een Git Repository. De baan Jenkins controleert uit de recentste staat van dat project of tak en dan brengt dit manuscript in werking.

Met dit script wordt op zijn beurt de Git Repository van Cloud Manager uitgecheckt en wordt de projectcode toegewezen aan een submap.

De Jenkins-taak moet twee geheimen hebben, `MAIN_USER` en `MAIN_PASSWORD`, om verbinding te kunnen maken met en te kunnen drukken op de Git-opslagplaats van Cloud Manager.

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

Zoals hierboven is weergegeven, is het gebruik van een Jenkins-baan erg flexibel. Elke toewijzing tussen vertakkingen van de Git-opslagplaatsen kan worden uitgevoerd en elke toewijzing van de afzonderlijke Git-projecten aan de mappenlay-out van het hoofdproject.

>[!NOTE]
>In het bovenstaande script wordt `git add` gebruikt om de gegevensopslagruimte bij te werken, waarbij ervan wordt uitgegaan dat verwijderingen worden opgenomen. Afhankelijk van de standaardconfiguratie van Git moet dit worden vervangen door `git add --all`.