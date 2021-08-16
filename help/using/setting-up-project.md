---
title: Het project instellen
description: Volg deze pagina om te leren hoe u een project instelt
feature: Aan de slag, Productieprogramma's
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 2a253abb98fa096f9f1c07bac94804849fad2ebb
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 7%

---

# Uw project instellen {#setting-up-your-project}

## Details projectinstelling wijzigen {#modifying-project-setup-details}

Om te kunnen worden gebouwd en geïmplementeerd met Cloud Manager, moeten bestaande AEM projecten zich aan een aantal basisregels houden:

* Projecten moeten worden gebouwd met Apache Maven.
* Er moet een *pom.xml*-bestand aanwezig zijn in de hoofdmap van de Git-opslagplaats. Dit *pom.xml*-bestand kan verwijzen naar zoveel submodules (die op hun beurt weer andere submodules kunnen hebben, enz.) indien nodig.

* U kunt verwijzingen naar extra bewaarplaatsen van het Artefact toevoegen Maven in uw *pom.xml* dossiers. De toegang tot [met wachtwoord beveiligde artefactrepositories](#password-protected-maven-repositories) wordt gesteund wanneer gevormd. Toegang tot door het netwerk beveiligde gegevensbestanden voor artefacten wordt echter niet ondersteund.
* Implementeerbare inhoudspakketten worden gedetecteerd door te scannen op inhoud *zip* bestanden die zich in een map met de naam *target* bevinden. Elk aantal submodules kan inhoudspakketten produceren.

* Implementeerbare Dispatcher-artefacten worden gedetecteerd door te scannen op *zip*-bestanden (opnieuw opgenomen in een map met de naam *target*) met mappen met de namen *conf* en *conf.d*.

* Als er meer dan één inhoudspakket is, wordt de volgorde van pakketimplementaties niet gegarandeerd. Als een specifieke orde nodig is, kunnen de gebiedsdelen van het inhoudspakket worden gebruikt om de orde te bepalen. Pakketten kunnen [van implementatie worden overgeslagen](#skipping-content-packages).


## GeMaven profielen activeren in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In sommige beperkte gevallen moet u het constructieproces mogelijk enigszins variëren wanneer u het uitvoert in Cloud Manager, in tegenstelling tot wanneer het wordt uitgevoerd op ontwikkelaarswerkstations. In deze gevallen kan [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) worden gebruikt om te definiëren hoe de build in verschillende omgevingen moet verschillen, waaronder Cloud Manager.

De activering van een Geweven Profiel binnen de de bouwstijlmilieu van de Manager van de Wolk zou moeten worden gedaan door Cm_BUILD milieuvariabele te zoeken die hierboven wordt beschreven. Omgekeerd moet een profiel dat alleen buiten de buildomgeving van Cloud Manager moet worden gebruikt, worden uitgevoerd door te zoeken naar de afwezigheid van deze variabele.

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
>Om dit profiel op een ontwikkelaarwerkstation te testen, kunt u of het op de bevellijn (met `-PcmBuild`) of in uw Geïntegreerde Ontwikkelomgeving (winde) toelaten.

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

>[!NOTE]
>Artefacten van een met wachtwoord beveiligde Maven-opslagplaats mogen alleen zeer voorzichtig worden gebruikt, aangezien code die via dit mechanisme wordt geïmplementeerd, momenteel niet door alle kwaliteitsregels wordt uitgevoerd die in de Quality Gates van Cloud Manager zijn geïmplementeerd. Daarom mag het alleen worden gebruikt in zeldzame gevallen en voor code die niet aan AEM is gekoppeld. Het wordt geadviseerd om de bronnen van Java evenals de volledige code van de projectbron samen met het binaire getal op te stellen.

Als u een met een wachtwoord beveiligde gegevensopslagruimte vanuit Cloud Manager wilt gebruiken, geeft u het wachtwoord (en eventueel de gebruikersnaam) op als geheim [Pipeline Variable](/help/using/build-environment-details.md#pipeline-variables) en verwijst u naar dat geheim in een bestand met de naam `.cloudmanager/maven/settings.xml` in de gegevensopslagruimte. Dit bestand volgt het schema [Maven Settings File](https://maven.apache.org/settings.html). Wanneer het buildproces van Cloud Manager wordt gestart, wordt het `<servers>`-element in dit bestand samengevoegd met het standaardbestand `settings.xml` van Cloud Manager. Server-id&#39;s die beginnen met `adobe` en `cloud-manager` worden beschouwd als gereserveerd en mogen niet worden gebruikt door aangepaste servers. Server-id&#39;s **niet** die overeenkomen met een van deze voorvoegsels of de standaard-id `central` worden nooit weerspiegeld door Cloud Manager. Als dit bestand is geïnstalleerd, wordt naar de server-id verwezen vanuit een `<repository>`- en/of `<pluginRepository>`-element in het `pom.xml`-bestand. In het algemeen worden deze `<repository>` en/of `<pluginRepository>` elementen opgenomen in een [Cloud Manager-specifiek profiel](#activating-maven-profiles-in-cloud-manager), hoewel dat niet strikt noodzakelijk is.

Stel bijvoorbeeld dat de gegevensopslagruimte zich op https://repository.myco.com/maven2 bevindt. De naam van de gebruiker is `cloudmanager` en het wachtwoord is `secretword`.

Plaats eerst het wachtwoord als geheim op de pijpleiding:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Verwijs dan dit van het `.cloudmanager/maven/settings.xml` dossier:

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

En ten slotte verwijs naar de server-id in het `pom.xml`-bestand:

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

Vorm maven-bron-stop in uw project:

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

Het is een goede praktijk om de volledige projectbron samen met binair aan een Geweven bewaarplaats op te stellen - dit staat toe om het nauwkeurige artefact te herbouwen.

Vorm maven-assemblage-stop in uw project:

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

In Cloud Manager kunnen builds een willekeurig aantal inhoudspakketten produceren.
Om diverse redenen kan het wenselijk zijn een inhoudspakket te maken, maar het niet te implementeren. Dit kan bijvoorbeeld handig zijn wanneer u inhoudspakketten maakt die alleen voor testen worden gebruikt of die door een andere stap in het constructieproces opnieuw worden verpakt, dat wil zeggen als een subpakket van een ander pakket.

Voor deze scenario&#39;s zoekt Cloud Manager naar een eigenschap met de naam ***cloudManagerTarget*** in de eigenschappen van samengestelde contentpakketten. Als deze eigenschap is ingesteld op Geen, zal het pakket worden overgeslagen en niet geïmplementeerd. Het mechanisme om deze eigenschap in te stellen hangt af van de manier waarop de build het contentpakket produceert. Met de invoegtoepassing filevault-maven-plugin kunt u de invoegtoepassing bijvoorbeeld als volgt configureren:

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

Met de insteekmodule voor het verpakken van inhoud is deze vergelijkbaar:

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

## Ontwikkel uw Code die op Beste praktijken wordt gebaseerd {#develop-your-code-based-on-best-practices}

Adobe Engineering- en Consultingteams hebben een [uitgebreide set met best practices ontwikkeld voor AEM ontwikkelaars](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html).
