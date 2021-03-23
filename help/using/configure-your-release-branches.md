---
title: Configureer uw releasevertakkingen
seo-title: Configureer uw releasevertakkingen
description: Release-vertakkingen configureren in Git voor AEM Cloud Manager
seo-description: Volg deze pagina om te leren op hoe te om uw versietakken in git te vormen.
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
feature: Opslagplaatsen voor git
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Configureer uw releasetak {#configure-your-release-branches}

## Uw eerste vertakking instellen in Git {#setting-up-your-first-branch-in-git}

Eén **Git Repository** is in eerste instantie leeg en is bestemd voor elk programma dat in Cloud Manager wordt uitgevoerd. Deze opslagplaats kan zo vele (of slechts weinig) takken bevatten aangezien uw ontwikkelingsproces volgt, maar er moet minstens één tak zijn die door de pijpleiding CI/CD wordt gebruikt om toepassingscode aan stadium en productie op te stellen. De beste praktijken moeten `master` als naam van deze tak gebruiken. Dit is handig het standaardgedrag van Git-clients wanneer u nieuwe projecten instelt.

Als u bijvoorbeeld een nieuw project instelt, voert u een set opdrachten als deze uit:

```shell
$ git init
Initialized empty Git repository in /Users/myname/workspace/new-project/.git/
... steps which add Maven build files and source code ...
$ git add pom.xml core/pom.xml core/src ui.apps/pom.xml ui.apps/src
$ git commit -m "initial commit"
 19 files changed, 777 insertions(+)
 create mode 100644 core/pom.xml
 create mode 100644 pom.xml
 create mode 100644 ui.apps/pom.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/config.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/definition/.content.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/filter.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/nodetypes.cnd
 create mode 100644 ui.apps/src/main/content/META-INF/vault/properties.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/apps/my-aem-project/install/.vltignore
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/_rep_policy.xml
```

>[!NOTE]
>
>Het is geen vereiste om de bevel-lijn cliënt te gebruiken. Er zijn een verscheidenheid van grafische cliënten van Git beschikbaar of als standalone toepassingen of als deel van een Geïntegreerde Ontwikkelomgeving (winde) zoals Eclipse of IntelliJ. Zolang de clienttoepassing het gebruik van HTTPS ondersteunt, moet deze compatibel zijn met [!UICONTROL Cloud Manager].

## Het duwen van Uw Eerste Tak {#pushing-your-first-branch}

Nadat u ten minste één revisie hebt vastgelegd, kunt u de [!UICONTROL Cloud Manager]-opslagplaats toevoegen als een **extern** en vervolgens uw verbintenissen nakomen:

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      master -> master
```

>[!NOTE]
>
>De specifieke URL, samen met uw referenties, wordt tijdens [!UICONTROL Cloud Manager] on boarding door uw Success Engineering van de Klant verstrekt.

## Aanvullende vertakkingen {#additional-branches}

Een enkele `master` tak kan volstaan voor zeer eenvoudige projecten, maar in de meeste gevallen is een complexere vertakkingsstrategie vereist. Vele klanten volgen een proces waar de de ontwikkelingsactiviteiten van dag tot dag op een tak worden uitgevoerd genoemd `develop` en de ontwikkeltak wordt samengevoegd in `master` tak wanneer het tijd voor een plaatsing is.

>[!NOTE]
>
>Zie [Cheat Sheet plaatsen](https://github.github.com/training-kit/downloads/github-git-cheat-sheet) om de algemene git-opdrachten weer te geven.
