---
title: Het project instellen
description: Leer hoe u uw project instelt zodat u het kunt beheren en implementeren met Cloud Manager.
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 2%

---


# Projectinstelling {#setting-up-your-project}

Leer hoe u uw project instelt zodat u het kunt beheren en implementeren met Cloud Manager.

## Bestaande projecten wijzigen {#modifying-project-setup-details}

Bestaande AEM projecten moeten zich aan enkele basisregels houden om te kunnen worden gebouwd en met succes te kunnen worden geïmplementeerd met Cloud Manager.

* Projecten moeten worden gebouwd met Apache Maven.
* Er moet een `pom.xml` in de hoofdmap van de it-opslagplaats.
   * Dit `pom.xml` bestand kan verwijzen naar zoveel submodules (die op hun beurt weer andere submodules kunnen hebben) als nodig.
   * U kunt verwijzingen toevoegen naar extra gegevensopslagruimten voor vervormingen in uw `pom.xml` bestanden.
   * Toegang tot [met wachtwoord beveiligde gegevensbanken voor artefacten](#password-protected-maven-repositories) wordt gesteund wanneer gevormd. Toegang tot door het netwerk beveiligde gegevensbestanden voor artefacten wordt echter niet ondersteund.
* Implementeerbare inhoudspakketten worden gedetecteerd door te zoeken naar .zip-bestanden van een inhoudspakket in een map met de naam `target`.
   * Elk aantal submodules kan inhoudspakketten produceren.
* Implementeerbare Dispatcher-artefacten worden gedetecteerd door te scannen op `zip` bestanden bevatten submappen van `target` benoemd `conf` en `conf.d`.
* Als er meer dan één inhoudspakket is, wordt de volgorde van pakketimplementaties niet gegarandeerd.
* Als een specifieke orde nodig is, kunnen de gebiedsdelen van het inhoudspakket worden gebruikt om de orde te bepalen.
* Verpakkingen kunnen [overgeslagen](#skipping-content-packages) vanaf de implementatie.

## GeMaven profielen activeren in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In sommige beperkte gevallen moet u het constructieproces mogelijk enigszins variëren wanneer u het uitvoert in Cloud Manager, in tegenstelling tot wanneer het wordt uitgevoerd op ontwikkelaarswerkstations. In deze gevallen [Geweven profielen](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) kan worden gebruikt om te definiëren hoe de build in verschillende omgevingen moet verschillen, waaronder Cloud Manager.

Activering van een Maven Profiel in de Cloud Manager-ontwikkelomgeving moet worden uitgevoerd door te zoeken naar `CM_BUILD` [omgevingsvariabele](/help/getting-started/build-environment.md#environment-variables) omgevingsvariabele. Omgekeerd moet een profiel dat alleen buiten de buildomgeving van Cloud Manager moet worden gebruikt, worden uitgevoerd door te zoeken naar de afwezigheid van deze variabele.

Als u bijvoorbeeld alleen een eenvoudig bericht wilt uitvoeren wanneer de build wordt uitgevoerd in Cloud Manager, doet u het volgende:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Als u dit profiel op een werkstation voor ontwikkelaars wilt testen, kunt u het op de opdrachtregel inschakelen (met `-PcmBuild`) of in uw Integrated Development Environment (IDE).

En als u een eenvoudig bericht wilt uitvoeren slechts wanneer de bouwstijl buiten de Manager van de Wolk in werking wordt gesteld, zou u dit doen:

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## Ondersteuning voor met wachtwoord beveiligde gegevensopslagruimte {#password-protected-maven-repositories}

Artefacten van een met een wachtwoord beveiligde Maven-opslagplaats mogen alleen zeer voorzichtig worden gebruikt, aangezien code die via dit mechanisme wordt geïmplementeerd, niet door alle kwaliteitsregels wordt uitgevoerd die in de kwaliteitspoorten van Cloud Manager zijn geïmplementeerd. Het wordt geadviseerd om de bronnen van Java evenals de volledige code van de projectbron samen met het binaire getal op te stellen.

>[!TIP]
>
>Artefacten van met een wachtwoord beveiligde Maven-repositories mogen alleen in zeldzame gevallen worden gebruikt en voor code die niet aan AEM is gekoppeld.

Als u een met een wachtwoord beveiligde gegevensopslagruimte vanuit Cloud Manager wilt gebruiken, geeft u het wachtwoord (en eventueel de gebruikersnaam) op als geheim [Pipetvariabele](/help/getting-started/build-environment.md#pipeline-variables) en verwijst u naar dat geheim in een bestand met de naam `.cloudmanager/maven/settings.xml` in de it-opslagplaats. Dit bestand volgt op [Maven Settings-bestand](https://maven.apache.org/settings.html) schema.

Wanneer het buildproces van Cloud Manager wordt gestart, wordt `<servers>` element in dit bestand wordt samengevoegd met de standaardwaarde `settings.xml` bestand geleverd door Cloud Manager. Server-id&#39;s die beginnen met `adobe` en `cloud-manager` worden beschouwd als gereserveerd en mogen niet worden gebruikt door aangepaste servers. Server-id&#39;s die niet overeenkomen met een van deze voorvoegsels of de standaard-id `central` wordt nooit weerspiegeld door Cloud Manager.

Als dit bestand is geïnstalleerd, wordt vanuit een `<repository>` en/of `<pluginRepository>` element binnen de `pom.xml` bestand. Over het algemeen: `<repository>` en/of `<pluginRepository>` elementen zouden in een [Specifiek profiel voor Cloud Manager](#activating-maven-profiles-in-cloud-manager), hoewel dat niet strikt noodzakelijk is.

Als voorbeeld, laten we zeggen dat de bewaarplaats is bij `https://repository.myco.com/maven2`is de gebruikersnaam die Cloud Manager moet gebruiken: `cloudmanager` en het wachtwoord `secretword`.

Plaats eerst het wachtwoord als geheim op de pijpleiding:

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword
```

Verwijs dit vervolgens vanuit de `.cloudmanager/maven/settings.xml` bestand:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

En ten slotte verwijst u naar de server-id in de `pom.xml` bestand:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

### Bronnen implementeren {#deploying-sources}

Het is een goede praktijk om de bronnen van Java samen met binair aan een Geweven bewaarplaats op te stellen.

Configureer de `maven-source-plugin` in uw project:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### Projectbronnen implementeren {#deploying-project-sources}

Het is een goede praktijk om de volledige projectbron samen met binair aan een Geweven bewaarplaats op te stellen. Hierdoor kan het exacte artefact opnieuw worden opgebouwd.

Configureer de `maven-assembly-plugin` in uw project:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## Inhoudspakketten worden overgeslagen {#skipping-content-packages}

In Cloud Manager kunnen builds een willekeurig aantal inhoudspakketten produceren. Om diverse redenen kan het wenselijk zijn een inhoudspakket te maken, maar het niet te implementeren. Dit kan bijvoorbeeld handig zijn wanneer u inhoudspakketten maakt die alleen voor testen worden gebruikt of die door een andere stap in het constructieproces opnieuw worden verpakt, dat wil zeggen als een subpakket van een ander pakket.

Voor deze scenario&#39;s zoekt Cloud Manager naar een eigenschap met de naam `cloudManagerTarget` in de eigenschappen van samengestelde contentpakketten. Als deze eigenschap is ingesteld op `none`, wordt het pakket overgeslagen en niet geïmplementeerd. Het mechanisme om deze eigenschap in te stellen hangt af van de manier waarop de build het contentpakket produceert. Met de `filevault-maven-plugin` u zou de stop als volgt vormen:

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

Met de `content-package-maven-plugin` het is vergelijkbaar :

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## Artefacthergebruik maken {#build-artifact-reuse}

In veel gevallen, wordt de zelfde code opgesteld aan veelvoudige AEM milieu&#39;s. Waar mogelijk, zal de Manager van de Wolk vermijden herbouwend de codebasis wanneer het ontdekt dat het zelfde gat begaan wordt gebruikt in veelvoudige full-stack pijpleidinguitvoeringen.

Wanneer een uitvoering is begonnen, begaat de huidige HEAD voor de takpijpleiding wordt gehaald. De commit hash is zichtbaar in UI en via API. Wanneer de bouwstijlstap met succes voltooit, worden de resulterende artefacten opgeslagen gebaseerd op die knoeiboel begaan en kunnen in verdere pijpleidingsuitvoeringen opnieuw worden gebruikt.

Pakketten worden opnieuw gebruikt via pijpleidingen als ze zich in hetzelfde programma bevinden. Wanneer u pakketten zoekt die opnieuw kunnen worden gebruikt, negeert AEM vertakkingen en hergebruikt artefacten tussen vertakkingen.

Wanneer een hergebruik voorkomt, worden de bouw en de stappen van de codekwaliteit effectief vervangen met de resultaten van de originele uitvoering. Het logboekdossier voor de bouwstijlstap zal van de artefacten en de uitvoeringsinformatie een lijst maken die werd gebruikt om hen oorspronkelijk te bouwen.

Hieronder ziet u een voorbeeld van een dergelijke loguitvoer.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Het logboek van de stap van de codekwaliteit zal gelijkaardige informatie bevatten.

### Voorbeelden {#example-reuse}

#### Voorbeeld 1 {#example-1}

Houd er rekening mee dat uw programma twee ontwikkelingspijplijnen heeft:

* Pijpleiding 1 op tak `foo`
* Pijpleiding 2 op vertakking `bar`

Beide vertakkingen zijn op zelfde verbind identiteitskaart

1. De lopende pijpleiding 1 zal eerst de pakketten normaal bouwen.
1. Dan die pijpleiding 2 loopt zal pakketten hergebruiken die door pijpleiding 1 worden gecreeerd.

#### Voorbeeld 2 {#example-2}

Houd er rekening mee dat uw programma twee vertakkingen heeft:

* Branch `foo`
* Branch `bar`

Beide vertakkingen hebben zelfde verbind identiteitskaart

1. Een ontwikkelingspijplijn bouwt en voert uit `foo`.
1. Daarna bouwt en voert een productiepijpleiding uit `bar`.

In dit geval is het artefact van `foo` zal opnieuw worden gebruikt voor de productiepijplijn aangezien dezelfde &quot;commit hash&quot; is geïdentificeerd.

### Afmelden {#opting-out}

Indien gewenst, kan het hergebruikgedrag voor specifieke pijpleidingen door de pijpleidingsvariabele te plaatsen worden onbruikbaar gemaakt `CM_DISABLE_BUILD_REUSE` tot `true`. Als deze variabele wordt geplaatst, begaan hash nog wordt gehaald en de resulterende artefacten voor later gebruik zullen worden opgeslagen, maar om het even welke eerder opgeslagen artefacten zullen niet opnieuw worden gebruikt. Overweeg het volgende scenario om dit gedrag te begrijpen.

1. Er wordt een nieuwe pijpleiding gemaakt.
1. De pijpleiding wordt uitgevoerd (uitvoering #1) en de huidige HEAD begaan is `becdddb`. De uitvoering is geslaagd en de resulterende artefacten worden opgeslagen.
1. De `CM_DISABLE_BUILD_REUSE` variable is set.
1. De pijpleiding wordt opnieuw uitgevoerd zonder code te veranderen. Hoewel er opgeslagen artefacten verbonden aan zijn `becdddb`, worden zij niet opnieuw gebruikt vanwege de `CM_DISABLE_BUILD_REUSE` variabele.
1. De code wordt veranderd en de pijpleiding wordt uitgevoerd. De HEAD commit is nu `f6ac5e6`. De uitvoering is geslaagd en de resulterende artefacten worden opgeslagen.
1. De `CM_DISABLE_BUILD_REUSE` variabele wordt verwijderd.
1. De pijpleiding wordt re-uitgevoerd zonder de code te veranderen. Aangezien er opgeslagen artefacten verbonden aan zijn `f6ac5e6`, worden deze artefacten opnieuw gebruikt.

### Caveats {#caveats}

* Artefacten van de bouwstijl worden niet opnieuw gebruikt over verschillende programma&#39;s, ongeacht als de commit knoeiboel identiek is.
* De kunstmatigheden van de bouwstijl worden opnieuw gebruikt binnen het zelfde programma zelfs als de tak en/of de pijpleiding verschillend is.
* [Beproefde versieafhandeling](/help/managing-code/maven-project-version.md) de projectversie alleen in productiepijpleidingen vervangen. Daarom als het zelfde begaat op zowel ontwikkelt uitvoering als een uitvoering van de productiepijplijn en de ontwikkelings opstellen pijpleiding eerst wordt uitgevoerd, zullen de versies aan stadium en productie zonder worden veranderd worden opgesteld. In dit geval wordt echter nog steeds een tag gemaakt.
* Als de terugwinning van de opgeslagen artefacten niet succesvol is, zal de bouwstijlstap worden uitgevoerd alsof geen artefacten waren opgeslagen.
* Andere pijpleidingvariabelen dan `CM_DISABLE_BUILD_REUSE` worden niet in overweging genomen wanneer Cloud Manager besluit eerder gemaakte constructieartefacten opnieuw te gebruiken.

## Ontwikkel uw Code die op Beste praktijken wordt gebaseerd {#develop-your-code-based-on-best-practices}

Adobe Engineering- en Consultingteams hebben een [uitgebreide reeks beste praktijken voor AEM ontwikkelaars.](https://experienceleague.adobe.com/docs/experience-manager-65/developing/bestpractices/best-practices.html)
