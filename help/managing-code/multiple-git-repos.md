---
title: Werken met Meerdere Git-opslagplaatsen
description: In plaats van rechtstreeks te werken met de git-opslagplaats van Cloud Manager, leert u hoe u kunt werken met uw eigen git-opslagplaats of met meerdere git-opslagplaatsen.
exl-id: 53bf78bb-489a-4a83-8459-c361f532d54a
source-git-commit: da9dff997a277c207e2c48207217cb30325f3c0d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Werken met Meerdere opslagplaatsen voor Git-bronnen {#working-with-multiple-source-git-repos}

In plaats van rechtstreeks te werken met de git-opslagplaats van Cloud Manager, leert u hoe u kunt werken met uw eigen git-opslagplaats of met meerdere git-opslagplaatsen.

## Door de klant beheerde Git-opslagruimten synchroniseren {#syncing-customer-managed-git-repositories}

Als u met uw eigen opslagplaats of opslagplaatsen wilt werken, moet een geautomatiseerd synchronisatieproces worden ingesteld om ervoor te zorgen dat de git-opslagplaats van Cloud Manager altijd up-to-date blijft.

Afhankelijk van waar uw git bewaarplaats wordt ontvangen, zou een actie GitHub of een ononderbroken integratieoplossing zoals Jenkins aan opstelling de automatisering kunnen worden gebruikt. Met een automatisering op zijn plaats, kan elke duw aan uw eigen bewaarplaats automatisch door:sturen aan de gokbewaarplaats van de Manager van de Wolk.

Hoewel een dergelijke automatisering voor één enkele klant-eigendom git bewaarplaats ongecompliceerd is, vereist het vormen van dit omhoog voor veelvoudige bewaarplaatsen een meer geïmpliceerde aanvankelijke opstelling. De inhoud van meerdere opslagruimten voor it moet worden toegewezen aan verschillende directory&#39;s binnen één opslagplaats voor it van Cloud Manager. De git-opslagruimte van Cloud Manager moet worden ingericht met een basisopslagruimte `pom.xml`, waarin de verschillende subprojecten worden vermeld in de sectie modules

Hieronder ziet u een monster `pom.xml` voor twee in eigendom van de klant zijnde it-opslagplaatsen. Het eerste project wordt in de genoemde directory geplaatst `project-a`, het tweede project in genoemde folder wordt gezet `project-b`.

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

Een dergelijke wortel `pom.xml` naar een vertakking in de git-opslagplaats van Cloud Manager. Vervolgens moeten de twee projecten worden ingesteld om wijzigingen automatisch door te sturen naar de git-opslagplaats van Cloud Manager.

Bijvoorbeeld, kan een actie GitHub door een duw aan een tak in project A worden teweeggebracht. Met deze actie worden project A en de gegevensopslagruimte van Cloud Manager uitgecheckt en wordt alle inhoud van project A naar de directory gekopieerd `project-a` in de git-opslagplaats van Cloud Manager en druk vervolgens op de wijziging.

Een wijziging van de `main` vertakking in project A wordt automatisch geduwd aan `main` vertakken in de git-opslagplaats van Cloud Manager. Natuurlijk zou er een afbeelding tussen takken als een duw aan een vertakking kunnen zijn genoemd `dev` in project A wordt geduwd aan een tak genoemd `development` in de git-opslagplaats van Cloud Manager. Vergelijkbare stappen zijn vereist voor project B.

Afhankelijk van de vertakkingsstrategie en workflows kan de synchronisatie worden geconfigureerd voor verschillende vertakkingen. Als de gebruikte gokbewaarplaats geen concept gelijkend op acties GitHub verstrekt, is een integratie via (of gelijkaardig) Jenkins ook mogelijk. In dit geval activeert een webhaak een Jenkins-taak die het werk doet.

Voer de onderstaande stappen uit om een nieuwe (derde) bron of opslagplaats toe te voegen:

1. Voeg een nieuwe actie GitHub aan de nieuwe bewaarplaats toe die veranderingen van die bewaarplaats aan de git bewaarplaats van de Manager van de Wolk duwt.
1. Voer die actie ten minste één keer uit om ervoor te zorgen dat de projectcode zich in de git-opslagplaats van Cloud Manager bevindt.
1. Een verwijzing naar de nieuwe map toevoegen in de hoofdmap Maven `pom.xml` in de git-opslagplaats van Cloud Manager.

## Voorbeeld van GitHub-actie {#sample-github-action}

Dit is een steekproefGitHub actie die door een duw aan wordt teweeggebracht `main` vertakken en vervolgens naar een submap van de it-opslagplaats van Cloud Manager gaan. De acties GitHub moeten van twee geheimen worden voorzien, `MAIN_USER` en `MAIN_PASSWORD`om verbinding te kunnen maken met en te kunnen drukken op de git-opslagplaats van Cloud Manager.

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

Zoals hierboven getoond, is het gebruiken van een actie GitHub zeer flexibel. Elke toewijzing tussen vertakkingen van de it-opslagplaatsen kan worden uitgevoerd en elke toewijzing van de afzonderlijke it-projecten aan de mappenindeling van het hoofdproject.

>[!NOTE]
>
>Het bovenstaande script gebruikt `git add` om de gegevensopslagruimte bij te werken, waarbij ervan wordt uitgegaan dat verwijderingen worden opgenomen. Afhankelijk van de standaardconfiguratie van de it moet deze mogelijk worden vervangen door `git add --all`.

## Sample Jenkins Job {#sample-jenkins-job}

Dit is een voorbeeldscript dat kan worden gebruikt in een Jenkins-taak of vergelijkbaar. Het wordt geactiveerd door een wijziging in een git-opslagplaats. De baan Jenkins controleert uit de recentste staat van dat project of tak en dan brengt dit manuscript in werking.

Met dit script wordt op zijn beurt de git-opslagplaats van Cloud Manager uitgecheckt en wordt de projectcode toegewezen aan een submap.

De baan van Jenkins moet van twee geheimen worden voorzien, `MAIN_USER` en `MAIN_PASSWORD`om verbinding te kunnen maken met en te kunnen drukken op de git-opslagplaats van Cloud Manager.

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

Zoals hierboven is weergegeven, is het gebruik van een Jenkins-baan erg flexibel. Elke toewijzing tussen vertakkingen van de it-opslagplaatsen kan worden uitgevoerd en elke toewijzing van de afzonderlijke it-projecten aan de mappenindeling van het hoofdproject.

>[!NOTE]
>
>Het bovenstaande script gebruikt `git add` om de opslagplaats bij te werken die ervan uitgaat dat verwijderingen worden opgenomen.Afhankelijk van de standaardconfiguratie van it moet deze mogelijk worden vervangen door `git add --all`.
