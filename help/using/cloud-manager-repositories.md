---
title: Opslagplaatsen voor Cloud Manager
description: Opslagplaatsen voor Cloud Manager
source-git-commit: 7bda34be143d2d7587e61c09dab642f3419dfad9
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Opslagplaatsen voor Cloud Manager {#cloud-manager-repos}

Opslagplaatsen die zijn gemaakt en beschikbaar zijn in Cloud Manager, kunnen worden weergegeven en beheerd via de pagina Opslagplaatsen.

## Opslagplaatsen toevoegen en beheren {#add-manage-repos}

Voer de onderstaande stappen uit om opslagruimten in Cloud Manager weer te geven en te beheren:

1. Van **Overzicht van het Programma** pagina, klik op **Bewaarplaatsen** lusje en navigeer aan **Bewaarplaatsen** pagina.

1. Klik op **Opslagplaats toevoegen** om de wizard te starten.

   >[!NOTE]
   >Een gebruiker in de Manager van de Plaatsing of de rol van BedrijfsEigenaar moet worden het programma geopend om een bewaarplaats kunnen toevoegen.

   ![](assets/create-repo2.png)


1. Voer de gewenste naam en beschrijving in en klik op **Opslaan**.

   ![](assets/repo-1.png)

1. Selecteer **Opslaan**. De nieuwe reactie wordt weergegeven in de tabel, zoals hieronder wordt weergegeven.

   ![](assets/create-repo3.png)

   >[!NOTE]
   >In Cloud Manager gemaakte opslagplaatsen kunnen u ook selecteren tijdens het toevoegen of bewerken van pijpleidingstappen.

1. U kunt de opslagplaats selecteren en op de menuopties van uiterst rechts van de lijst klikken aan **Repository URL kopiëren**, **View &amp; Update** of **Delete** uw bewaarplaats, zoals aangetoond in de hieronder figuur.

   ![](assets/create-repo3.png)



## Ondersteuning voor Git-submodule {#git-submodule-support}

Git-submodules kunnen worden gebruikt om de inhoud van meerdere vertakkingen tijdens het samenstellen samen te voegen tussen git-opslagruimten. Wanneer het de bouwstijlproces van de Manager van de Wolk uitvoert, nadat de bewaarplaats die voor de pijpleiding wordt gevormd wordt gekloond en de gevormde tak wordt gecontroleerd, als de tak een `.gitmodules` dossier in de wortelfolder bevat, wordt het bevel uitgevoerd.

```
$ git submodule update --init
```

Dit zal elke submodule in de aangewezen folder uitchecken. Deze techniek is een mogelijk alternatief voor https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html voor organisaties die vertrouwd zijn met het gebruik van git-submodules en geen extern samenvoegingsproces willen beheren.

Stel dat er drie opslagplaatsen zijn, die elk een enkele vertakking met de naam main bevatten. In de &quot;primaire&quot; opslagplaats, d.w.z. de opslagplaats die in de pijpleidingen is geconfigureerd, heeft de hoofdtak een bestand pom.xml waarin de projecten in de andere twee opslagplaatsen worden aangegeven:

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

Dit resulteert in een `.gitmodules` dossier dat als dit kijkt:

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

Meer informatie over git-submodules vindt u in de [Git-referentiehandleiding](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Houd rekening met het volgende wanneer u git-submodules gebruikt:

* De URL van de it moet exact in de hierboven beschreven syntaxis staan. Sluit om beveiligingsredenen geen referenties in deze URL&#39;s in.
* Alleen submodules in de hoofdmap van de vertakking worden ondersteund.
* Git-submoduleverwijzingen worden opgeslagen naar specifieke it-opdrachten. Dientengevolge, wanneer veranderingen in de submodule bewaarplaats worden aangebracht, moet het gecommitteerde referenced worden bijgewerkt, bijvoorbeeld door `git submodule update --remote` te gebruiken.

