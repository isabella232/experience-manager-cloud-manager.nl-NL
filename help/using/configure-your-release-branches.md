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
translation-type: tm+mt
source-git-commit: 9c0df236c1e800802d62dea09996bb8e1e7033f7

---


# Configureer uw releasevertakkingen {#configure-your-release-branches}

## De eerste vertakking instellen in Git {#setting-up-your-first-branch-in-git}

Voor elk programma dat in Cloud Manager wordt gestart, wordt één, aanvankelijk lege **Git Repository** ingericht. Deze opslagplaats kan zo vele (of slechts weinig) takken bevatten aangezien uw ontwikkelingsproces volgt, maar er moet minstens één tak zijn die door de pijpleiding CI/CD wordt gebruikt om toepassingscode aan stadium en productie op te stellen. De beste manier is om als naam van deze vertakking te gebruiken `master` . Dit is handig het standaardgedrag van Git-clients wanneer u nieuwe projecten instelt.

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

## De eerste vertakking duwen {#pushing-your-first-branch}

Nadat u ten minste één revisie hebt vastgelegd, kunt u de [!UICONTROL Cloud Manager] opslagplaats toevoegen als een **externe** opslagruimte en vervolgens uw verplichtingen nakomen:

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
>De specifieke URL, samen met uw referenties, wordt tijdens het [!UICONTROL Cloud Manager] instappen aan uw klant geleverd door de Succesengineering van de klant.

## Aanvullende vertakkingen {#additional-branches}

Een enkele `master` tak kan voldoende zijn voor zeer eenvoudige projecten, maar in de meeste gevallen is een complexere vertakkingsstrategie vereist. Vele klanten volgen een proces waar de ontwikkelingsactiviteiten van dag tot dag op een geroepen tak worden uitgevoerd `develop` en de ontwikkeltak in de `master` tak wordt samengevoegd wanneer het tijd voor een plaatsing is.

>[!NOTE]
>
>Zie het [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)voor informatie over de algemene git-opdrachten.
