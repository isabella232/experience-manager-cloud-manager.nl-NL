---
title: Opslagplaatsen voor Cloud Manager
description: Opslagplaatsen voor Cloud Manager
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 280d760766cf445e609b865f827c01b4ab1db69c
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Opslagplaatsen voor Cloud Manager {#cloud-manager-repos}

Opslagplaatsen die zijn gemaakt en beschikbaar zijn in Cloud Manager, kunnen worden weergegeven en beheerd via de pagina Opslagplaatsen.

## Opslagplaatsen toevoegen en beheren {#add-manage-repos}

Voer de onderstaande stappen uit om opslagruimten in Cloud Manager weer te geven en te beheren:

1. Van de **Programmaoverzicht** pagina, klik op **Opslagplaatsen** en navigeer naar de **Opslagplaatsen** pagina.

1. Klikken op **Opslagplaats toevoegen** om de wizard te starten.

   >[!NOTE]
   >Een gebruiker in de Manager van de Plaatsing of de rol van BedrijfsEigenaar moet worden het programma geopend om een bewaarplaats kunnen toevoegen.

   ![](assets/create-repo2.png)


1. Voer de gewenste naam en beschrijving in en klik op **Opslaan**.

   ![](assets/repo-1.png)

1. Selecteren **Opslaan**. De nieuwe reactie wordt weergegeven in de tabel, zoals hieronder wordt weergegeven.

   ![](assets/create-repo3.png)

   >[!NOTE]
   >In Cloud Manager gemaakte opslagplaatsen kunnen u ook selecteren tijdens het toevoegen of bewerken van pijpleidingstappen.

1. U kunt de opslagplaats selecteren en op de menuopties van uiterst rechts in de tabel tot **Repository-URL kopiëren**, **Weergeven en bijwerken** of **Verwijderen** de opslagplaats, zoals weergegeven in de onderstaande afbeelding.

   ![](assets/create-repo3.png)



## Ondersteuning voor Git-submodule {#git-submodule-support}

Git-submodules kunnen worden gebruikt om de inhoud van meerdere vertakkingen tijdens het samenstellen samen te voegen tussen git-opslagruimten. Wanneer het de bouwstijlproces van de Manager van de Wolk uitvoert, nadat de bewaarplaats die voor de pijpleiding wordt gevormd wordt gekloond en de gevormde tak wordt gecontroleerd, als de tak een bevat `.gitmodules` in de hoofdmap, wordt de opdracht uitgevoerd.

```
$ git submodule update --init
```

Dit zal elke submodule in de aangewezen folder uitchecken. Deze techniek is een mogelijk alternatief voor [werken met meerdere Git-opslagruimten](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html) voor organisaties die comfortabel zijn met het gebruik van git-submodules en geen extern samenvoegingsproces willen beheren.

Stel dat er drie opslagruimten zijn, die elk één vertakking met de naam main bevatten. In de &quot;primaire&quot; opslagplaats, d.w.z. de opslagplaats die in de pijpleidingen is geconfigureerd, heeft de hoofdtak een bestand pom.xml waarin de projecten in de andere twee opslagplaatsen worden aangegeven:

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

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Dit leidt tot een `.gitmodules` bestand dat er als volgt uitziet:

```
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

Houd rekening met het volgende wanneer u git-submodules gebruikt:

* De URL van de it moet exact in de hierboven beschreven syntaxis staan. Sluit om beveiligingsredenen geen referenties in deze URL&#39;s in.
* Alleen submodules in de hoofdmap van de vertakking worden ondersteund.
* Git-submoduleverwijzingen worden opgeslagen naar specifieke it-opdrachten. Dientengevolge, wanneer veranderingen in de submodule bewaarplaats worden aangebracht, moet het gecommitteerde referenced worden bijgewerkt, bijvoorbeeld door te gebruiken `git submodule update --remote`.
* Tenzij anders nodig, wordt het ten zeerste aanbevolen &quot;oppervlakkige&quot; submodules te gebruiken. Voer `git config -f .gitmodules submodule.<submodule path>.shallow true` voor elke submodule.
