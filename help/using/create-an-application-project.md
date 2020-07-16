---
title: Een AEM-toepassingsproject maken
seo-title: Een AEM-toepassingsproject maken
description: 'null'
seo-description: Volg deze pagina voor meer informatie over het instellen van een AEM-project wanneer u aan de slag gaat met Cloud Manager.
uuid: 7b976ebf-5358-49d8-a58d-0bae026303fa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 76c1a8e4-d66f-4a3b-8c0c-b80c9e17700e
translation-type: tm+mt
source-git-commit: a4ea83c0b64515915871956c1cd3e53606f1c26b
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 6%

---


# Create an AEM Application Project {#create-an-aem-application-project}

## Wizard gebruiken om een AEM-toepassingsproject te maken {#using-wizard-to-create-an-aem-application-project}

Als klanten aan boord zijn van Cloud Manager, krijgen ze een lege git-opslagplaats. Huidige klanten van Adobe Managed Services (AMS) (of AEM-klanten op locatie die naar AMS migreren) hebben over het algemeen al hun projectcode in git (of een ander versiecontrolesysteem) en zullen hun project in de opslagplaats van de Manager van de Wolk invoeren. Nieuwe klanten hebben echter geen bestaande projecten.

Om nieuwe klanten aan de slag te helpen, kan Cloud Manager nu een minimaal AEM-project maken als startpunt. Dit proces is gebaseerd op het [**AEM Project Archetype **](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).


Voer de onderstaande stappen uit om een AEM-toepassingsproject te maken in Cloud Manager:

1. Nadat u zich hebt aangemeld bij Cloud Manager en de basisconfiguratie van het programma is voltooid, wordt een speciale aanroep naar een actiekaart weergegeven op het scherm **Overzicht** als de opslagplaats leeg is.

   ![](assets/image2018-10-3_14-29-44.png)

1. Klik op **** Maken om een dialoogvenster te openen waarin de gebruiker de parameters kan opgeven die vereist zijn voor het AEM-projectarchetype. In zijn standaardvorm, vraagt de dialoogdoos twee waarden:

   * **Titel** - deze is standaard ingesteld op *Programmanaam*

   * **Nieuwe Branch Name** - deze is standaard *master*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   Het dialoogvenster heeft een lade die kan worden geopend door op de handgreep naar de onderkant van het dialoogvenster te klikken. In zijn uitgebreide vorm, toont de dialoog alle configuratieparameters voor Archetype. Veel van deze parameters hebben standaardwaarden die op de **Titel** worden geproduceerd.

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >Als de **titel** bijvoorbeeld ***We.Finance*** is, wordt de parameter Basis Maven Artefact Id gegenereerd als ***com.wefinance***. Deze waarden kunnen desgewenst worden gewijzigd.
   >
   >
   >U kunt bijvoorbeeld de gegenereerde ***waarde com.wefinance*** wijzigen in ***net.wefinance***.

1. Klik in de voorafgaande stap **Maken** om het starterproject te maken met het archetype en vast te leggen aan de benoemde git-vertakking. Zodra dit wordt gedaan, kunt u opstelling de pijpleiding.

## Uw project instellen {#setting-up-your-project}

### Details projectinstelling wijzigen {#modifying-project-setup-details}

Voor een correcte bouw en implementatie met Cloud Manager moeten bestaande AEM-projecten zich aan een aantal basisregels houden:

* Projecten moeten worden gebouwd met Apache Maven.
* Er moet een *pom.xml* -bestand aanwezig zijn in de hoofdmap van de Git-opslagplaats. Dit *pom.xml* -bestand kan verwijzen naar zoveel submodules (die op hun beurt weer andere submodules kunnen hebben, enzovoort) indien nodig.

* U kunt verwijzingen naar extra bewaarplaatsen van het Artefact toevoegen Maven in uw *pom.xml* - dossiers. De toegang tot met een wachtwoord beveiligde of door het netwerk beveiligde gegevensopslagruimten voor artefacten wordt echter niet ondersteund.
* Implementeerbare inhoudspakketten worden ontdekt door te zoeken naar *ZIP* -bestanden van inhoudspakketten die zich in een map met de naam *target* bevinden. Elk aantal submodules kan inhoudspakketten produceren.

* Inzetbare Dispatcher-artefacten worden ontdekt door te zoeken naar *ZIP* -bestanden (opnieuw opgenomen in een map met de naam *target*) met mappen met de naam *conf* en *conf.d*.

* Als er meer dan één inhoudspakket is, wordt de volgorde van pakketimplementaties niet gegarandeerd. Als een specifieke orde nodig is, kunnen de gebiedsdelen van het inhoudspakket worden gebruikt om de orde te bepalen. Pakketten kunnen van plaatsing worden [overgeslagen](#skipping-content-packages) .

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## Omgevingsdetails samenstellen {#build-environment-details}

Cloud Manager bouwt en test uw code gebruikend een gespecialiseerde bouwstijlmilieu. Deze omgeving heeft de volgende kenmerken:

* De ontwikkelomgeving is gebaseerd op Linux en is afgeleid van Ubuntu 18.04.
* Apache Maven 3.6.0 is geïnstalleerd.
* De geïnstalleerde Java-versies zijn Oracle JDK 8u202 en 11.0.2.
* Er zijn enkele extra systeempakketten geïnstalleerd die nodig zijn:

   * bzip2
   * unzip
   * libpng
   * imagemagick
   * grafiesmagick

* Andere pakketten kunnen worden geïnstalleerd tijdens het samenstellen zoals [hieronder](#installing-additional-system-packages)wordt beschreven.
* Elke bouw wordt gedaan op een ongerepte milieu; de bouwstijlcontainer houdt geen staat tussen uitvoeringen.
* Maven wordt altijd uitgevoerd met de opdracht: *mvn —batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent package*
* Maven wordt geconfigureerd op systeemniveau met een bestand settings.xml dat automatisch de openbare Adobe **Artefact** -opslagplaats omvat. (Raadpleeg de [Adobe Public Maven Repository](https://repo.adobe.com/) voor meer informatie.)

>[!NOTE]
>Hoewel in Cloud Manager geen specifieke versie van de versie wordt gedefinieerd, moet de gebruikte versie minstens `jacoco-maven-plugin``0.7.5.201505241946`zijn.

### Java 11 gebruiken {#using-java-11}

Cloud Manager ondersteunt nu het maken van klantprojecten met zowel Java 8 als Java 11. Standaard worden projecten gemaakt met behulp van Java 8. Klanten die van plan zijn Java 11 in hun projecten te gebruiken, kunnen dit doen gebruikend de Insteekmodule van Toolketens [Apache Maven](https://maven.apache.org/plugins/maven-toolchains-plugin/).

Hiervoor voegt u in het bestand pom.xml een `<plugin>` item toe dat er als volgt uitziet:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-toolchains-plugin</artifactId>
            <version>1.1</version>
            <executions>
                <execution>
                    <goals>
                        <goal>toolchain</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <toolchains>
                    <jdk>
                        <version>11</version>
                        <vendor>oracle</vendor>
                    </jdk>
                </toolchains>
            </configuration>
        </plugin>
```

>[!NOTE]
>De ondersteunde `vendor` waarden zijn `oracle` en `sun` en de ondersteunde `version` waarden zijn `1.8`, `1.11`en `11`.

## Omgevingsvariabelen {#environment-variables}

### Standaardomgevingsvariabelen {#standard-environ-variables}

In sommige gevallen, vinden de klanten het noodzakelijk om het bouwstijlproces te variëren dat op informatie over het programma of de pijpleiding wordt gebaseerd.

Als bijvoorbeeld JavaScript-miniaturen tijdens het bouwen worden gemaakt met een tool als gulp, is het mogelijk dat u een ander Minificatieniveau wilt gebruiken bij het bouwen voor een ontwikkelomgeving in plaats van voor het bouwen voor het werkgebied en de productie.

Ter ondersteuning hiervan voegt Cloud Manager deze standaardomgevingsvariabelen voor elke uitvoering toe aan de container voor de build.

| **Naam variabele** | **Definitie** |
|---|---|
| CM_BUILD | Altijd ingesteld op &quot;true&quot; |
| BRANCH | De gevormde tak voor de uitvoering |
| CM_PIPELINE_ID | De numerieke identificatie van de pijpleiding |
| CM_PIPELINE_NAME | De pijpleidingsnaam |
| CM_PROGRAM_ID | De numerieke programma-id |
| CM_PROGRAM_NAME | De naam van het programma |
| ARTIFACTS_VERSION | Voor een stadium of productiepijplijn, de synthetische versie die door Cloud Manager wordt geproduceerd |

### Aangepaste omgevingsvariabelen {#custom-variables}

In sommige gevallen kan het constructieproces van een klant afhangen van specifieke configuratievariabelen die niet geschikt zijn om in de opslagplaats voor it te plaatsen. Cloud Manager staat voor deze variabelen toe om door een Ingenieur van het Succes van de Klant (CSE) op klant-door-klant basis worden gevormd.

Deze variabelen worden opgeslagen in een veilige opslagplaats en zijn slechts zichtbaar in de bouwstijlcontainer voor de specifieke klant. Klanten die deze functie willen gebruiken, moeten contact opnemen met hun CSE om hun variabelen te configureren.
Zodra gevormd, zullen deze variabelen als omgevingsvariabelen beschikbaar zijn. Als u deze eigenschappen als Maven-eigenschappen wilt gebruiken, kunt u ernaar verwijzen in het bestand pom.xml, mogelijk binnen een profiel zoals hierboven beschreven:


```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <properties>
                  <my.custom.property>${env.MY_CUSTOM_PROPERTY}</my.custom.property>  
            </properties>
        </profile>
```

>[!NOTE]
>Namen van omgevingsvariabelen mogen alleen alfanumerieke tekens en onderstrepingstekens (_) bevatten. Volgens de conventie moeten de namen allemaal hoofdletters zijn.

## GeMaven profielen activeren in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In sommige beperkte gevallen moet u het constructieproces mogelijk enigszins variëren wanneer u het uitvoert in Cloud Manager, in tegenstelling tot wanneer het wordt uitgevoerd op ontwikkelaarswerkstations. In deze gevallen kunt u [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) gebruiken om te definiëren hoe de build in verschillende omgevingen moet verschillen, waaronder Cloud Manager.

De activering van een Geweven Profiel binnen de de bouwstijlmilieu van de Manager van de Wolk zou moeten worden gedaan door Cm_BUILD milieuvariabele te zoeken die hierboven wordt beschreven. Een profiel dat alleen buiten de buildomgeving van Cloud Manager mag worden gebruikt, moet daarentegen worden uitgevoerd door te zoeken naar de abnormaal werking van deze variabele.

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
>Om dit profiel op een ontwikkelaarwerkstation te testen, kunt u of het op de bevellijn (met `-PcmBuild`) of in uw Geïntegreerde Milieu van de Ontwikkeling (winde) toelaten.

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

## Extra systeempakketten installeren {#installing-additional-system-packages}

Voor sommige builds moeten extra systeempakketten worden geïnstalleerd om volledig te kunnen functioneren. Een build kan bijvoorbeeld een Python- of ruby-script aanroepen en moet daarom een geschikte taalinterpreter hebben geïnstalleerd. Dit kan worden gedaan door de [exec-maven-stop](https://www.mojohaus.org/exec-maven-plugin/) aan te roepen APT. Deze uitvoering moet doorgaans worden opgenomen in een specifiek Maven-profiel voor Cloud Manager. Zo kunt u bijvoorbeeld python installeren:

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Dezelfde techniek kan worden gebruikt om taalspecifieke pakketten te installeren, d.w.z. `gem` voor RubyGems of `pip` voor Python Packages.

>[!NOTE]
>
>Als u een systeempakket op deze manier installeert, wordt dit **niet** geïnstalleerd in de runtimeomgeving die wordt gebruikt voor het uitvoeren van Adobe Experience Manager. Als u een systeempakket nodig hebt dat op de AEM-omgeving is geïnstalleerd, neemt u contact op met uw Customer Success Engineers (CSE).

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

Adobe Engineering- en Consulting-teams hebben een [uitgebreide set met best practices ontwikkeld voor AEM-ontwikkelaars](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html).
