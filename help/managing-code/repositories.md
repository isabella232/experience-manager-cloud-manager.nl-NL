---
title: Opslagplaatsen voor Cloud Manager
description: Leer hoe u opslagruimten voor uw Cloud Manager-programma's kunt openen, maken en bewerken.
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Opslagplaatsen voor Cloud Manager {#cloud-manager-repos}

In opslagplaatsen kunt u uw code beheren met behulp van git. Leer hoe u opslagruimten voor uw Cloud Manager-programma&#39;s maakt.

## Toegang tot opslagplaatsen {#accessing-repos}

U kunt uw git-opslagruimten openen en beheren in een zelfservice van Cloud Manager.

Als u toegang wilt krijgen tot uw opslagplaats, gebruikt u de **Repo-info openen** beschikbaar in Cloud Manager, vooral op de pijplijnkaart.

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie en het juiste programma.

1. Navigeren naar **Pijpleidingen** kaart van **Programmaoverzicht** pagina en u ziet de **Repo-info openen** optie voor toegang tot en beheer van uw git-opslagplaats [gevormd met deze pijpleiding.](/help/using/production-pipelines.md)

   ![Knop Repo-info openen](/help/assets/access-repo1.png)

1. Als u overschakelt op **Niet-productie** pijplijntabblad, de **Repo-info openen** ook daar beschikbaar als [gevormd voor de pijpleiding.](/help/using/non-production-pipelines.md)

   ![Niet-productieleidingen](/help/assets/access-repo-nonprod.png)

1. Klik op de knop **Repo-info openen** om een dialoogvenster te openen dat het volgende bevat:

   * De URL naar de gegevensopslagruimte
   * Gebruikersnaam
   * Wachtwoord
   * De opdracht Git wordt uitgevoerd om de repository lokaal te klonen

   ![Dialoogvenster met informatie over opslagplaats](/help/assets/access-repo-create.png)

Gebruik de verschafte informatie om de opslagplaats lokaal te klonen, zodat u met lokale ontwikkeling kunt beginnen.

>[!NOTE]
>
>De **Repo-info openen** Deze optie is zichtbaar voor gebruikers in de **Ontwikkelaar** of **Implementatiebeheer** rol.

## Opslagplaatsen toevoegen {#add-repos}

Ga als volgt te werk om opslagruimten toe te voegen in Cloud Manager:

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie en het juiste programma.

1. Van de **Programmaoverzicht** pagina, klik op **Opslagplaatsen** en navigeer naar de **Opslagplaatsen** pagina.

1. Klikken op **Opslagplaats toevoegen** om de wizard te starten.

   >[!NOTE]
   >
   >U moet beschikken over de **Implementatiebeheer** of **Zakelijke eigenaar** rol om een gegevensopslagruimte toe te voegen.

   ![Opslagplaats toevoegen](/help/assets/create-repo2.png)

1. Voer de gewenste naam en beschrijving in en klik op **Opslaan**.

   ![Details van het antwoord](/help/assets/repo-1.png)

1. Selecteren **Opslaan**.

Het nieuwe bericht wordt weergegeven.

![Nieuwe reactie gemaakt](/help/assets/create-repo3.png)

In Cloud Manager gemaakte opslagruimten kunnen worden geselecteerd wanneer u [uw pijpleidingen aanmaken.](/help/overview/ci-cd-pipelines.md)

## Opslagplaatsen weergeven en bewerken {#edit-repos}

Voer de volgende stappen uit om opslagruimten te bewerken en weer te geven in Cloud Manager:

1. Aanmelden bij Cloud Manager [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie en het juiste programma.

1. Van de **Programmaoverzicht** pagina, klik op **Opslagplaatsen** en navigeer naar de **Opslagplaatsen** pagina. Hier kunt u de details van uw bestaande opslagplaatsen bekijken.

1. Selecteer de opslagplaats en klik op de ellipsknop helemaal rechts van de tabel om **Repository-URL kopiëren**, **Weergeven en bijwerken** of **Verwijderen** uw opslagplaats.

![Repo bewerken](/help/assets/create-repo3.png)

## Ondersteuning voor Git-submodule {#git-submodule-support}

Git-submodules kunnen worden gebruikt om de inhoud van meerdere vertakkingen tijdens het samenstellen samen te voegen tussen git-opslagruimten.

Wanneer het de bouwstijlproces van de Manager van de Wolk uitvoert, nadat de bewaarplaats die voor de pijpleiding wordt gevormd wordt gekloond en de gevormde tak wordt gecontroleerd, als de tak een bevat `.gitmodules` in de hoofdmap, wordt de opdracht uitgevoerd.

```
$ git submodule update --init
```

Dit zal elke submodule in de aangewezen folder uitchecken. Deze techniek is een mogelijk alternatief voor [werken met meerdere Git-opslagruimten](/help/managing-code/multiple-git-repos.md) voor organisaties die comfortabel zijn met het gebruik van git-submodules en geen extern samenvoegingsproces willen beheren.

Stel bijvoorbeeld dat er drie opslagruimten zijn die elk één vertakking met de naam `main`. In de &quot;primaire&quot; opslagplaats, d.w.z. de opslagplaats die in de pijpleidingen is geconfigureerd, `main` vertakking bevat een `pom.xml` dossier waarin de projecten in de andere twee gegevensbanken worden gedeclareerd:

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

Vervolgens voegt u submodules toe voor de andere twee opslagruimten:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Dit leidt tot een `.gitmodules` bestand dat er als volgt uitziet:

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Meer informatie over git-submodules vindt u in de [Handleiding Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### Beperkingen {#limitations}

Houd rekening met het volgende wanneer u it-submodules gebruikt:

* De URL van de it moet exact in de hierboven beschreven syntaxis staan.
* Sluit om beveiligingsredenen geen referenties in deze URL&#39;s in.
* Alleen submodules in de hoofdmap van de vertakking worden ondersteund.
* Git-submoduleverwijzingen worden opgeslagen naar specifieke it-opdrachten.
   * Dientengevolge, wanneer veranderingen in de submodule bewaarplaats worden aangebracht, moet het gecommitteerde referenced worden bijgewerkt, bijvoorbeeld door te gebruiken `git submodule update --remote`.
* Tenzij anders nodig, wordt het ten zeerste aanbevolen &quot;oppervlakkige&quot; submodules te gebruiken.
   * Voer `git config -f .gitmodules submodule.<submodule path>.shallow true` voor elke submodule.
