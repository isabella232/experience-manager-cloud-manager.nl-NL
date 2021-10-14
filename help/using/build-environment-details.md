---
title: Inzicht in de omgeving van de build
description: Volg deze pagina voor meer informatie over omgevingen
feature: Environments
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 17f79fdc7278cae532485570a6e2b8700683ef0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Inzicht in de omgeving van de build {#build-environment-details}

Cloud Manager bouwt en test uw code gebruikend een gespecialiseerde bouwstijlmilieu. Deze omgeving heeft de volgende kenmerken:

* De ontwikkelomgeving is gebaseerd op Linux en is afgeleid van Ubuntu 18.04.
* Apache Maven 3.6.0 is geïnstalleerd.
* De geïnstalleerde Java-versies zijn Oracle JDK 8u202, Azul Zulu 8u292, Oracle JDK 11.0.2, en Azul Zulu 11.0.11.
* Standaard wordt de omgevingsvariabele JAVA_HOME ingesteld op `/usr/lib/jvm/jdk1.8.0_202` die Oracle JDK 8u202 bevat. Zie [JDK-versie](#alternate-maven) van Alternate Maven Execution voor meer informatie.
* Er zijn enkele extra systeempakketten geïnstalleerd die nodig zijn:

   * bzip2
   * unzip
   * libpng
   * imagemagick
   * grafiesmagick

* Andere pakketten kunnen worden geïnstalleerd tijdens het samenstellen zoals beschreven [hieronder](#installing-additional-system-packages).
* Elke bouw wordt gedaan op een ongerepte milieu; de bouwstijlcontainer houdt geen staat tussen uitvoeringen.
* Maven wordt altijd uitgevoerd met deze drie opdrachten:

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven wordt op systeemniveau geconfigureerd met een settings.xml-bestand dat automatisch de openbare Adobe **Artifact**-opslagplaats bevat met een profiel met de naam `adobe-public`.
Raadpleeg [Adobe Public Maven Repository](https://repo.adobe.com/) voor meer informatie.

>[!NOTE]
>Hoewel Cloud Manager geen specifieke versie van `jacoco-maven-plugin` definieert, moet de gebruikte versie ten minste `0.7.5.201505241946` zijn.


>[!NOTE]
>Raadpleeg de volgende aanvullende bronnen voor meer informatie over het gebruik van API&#39;s van Cloud Manager:
> * [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [API-integratie maken](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API-machtigingen](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## Een specifieke Java-versie gebruiken {#using-java-version}

Standaard worden projecten gemaakt door het buildproces van Cloud Manager met Oracle 8 JDK. Klanten die een alternatieve JDK willen gebruiken, hebben twee opties: Gemaakt met toolketens en het selecteren van een afwisselende versie JDK voor het volledige Geweven uitvoeringsproces.

### Maven Toolketins {#maven-toolchains}

Met de [Insteekmodule Gemaakt gereedschap](https://maven.apache.org/plugins/maven-toolchains-plugin/) kunnen projecten een specifieke JDK (of *toolchain*) selecteren die moet worden gebruikt in de context van Maven-ins met gereedschapsketens. Dit wordt gedaan in het `pom.xml` dossier van het project door een verkoper en versiewaarde te specificeren. Een voorbeeldsectie in het `pom.xml` dossier is:

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

Hierdoor wordt voor alle plug-ins met behoud van gereedschappen het Oracle JDK, versie 11, gebruikt.

Wanneer u deze methode gebruikt, wordt Maven zelf nog steeds uitgevoerd met de standaard-JDK (Oracle 8) en wordt de omgevingsvariabele `JAVA_HOME` niet gewijzigd. Daarom werkt het controleren of afdwingen van de Java-versie via plug-ins zoals de [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) niet en mogen dergelijke plug-ins niet worden gebruikt.

De momenteel beschikbare leverancier/versiecombinaties zijn:

* oracle 1.8
* oracle 1.11
* oracle 11
* zon 1.8
* zon 1.11
* zon 11
* azul 1,8
* azul 1,11
* azul 8

### JDK-versie van alternatieve uitvoering {#alternate-maven}

Het is ook mogelijk om Azul 8 of Azul 11 te selecteren als JDK voor de volledige executie Maven. In tegenstelling tot de opties van toolketins, verandert dit JDK die voor alle stop-ins wordt gebruikt tenzij de toolketenconfiguratie ook wordt geplaatst waarin de toolkettenconfiguratie nog voor toolketens-bewuste Maven plugins wordt toegepast. Hierdoor werkt het controleren en afdwingen van de Java-versie met de [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/).

Hiertoe maakt u een bestand met de naam `.cloudmanager/java-version` in de vertakking van de it-opslagruimte die door de pijplijn wordt gebruikt. Dit bestand kan de inhoud 11 of 8 hebben. Eventuele andere waarden worden genegeerd. Als 11 wordt gespecificeerd, wordt Azul 11 gebruikt en JAVA_HOME milieuvariabele wordt geplaatst aan `/usr/lib/jvm/jdk-11.0.11`. Als 8 wordt gespecificeerd, wordt Azul 8 gebruikt en JAVA_HOME milieuvariabele wordt geplaatst aan `/usr/lib/jvm/jdk-8.0.292`.

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

### Pipetvariabelen {#pipeline-variables}

In sommige gevallen, kan het bouwstijlproces van een klant van specifieke configuratievariabelen afhangen die om in de bewaarplaats van het Git ongepast zouden zijn te plaatsen of tussen pijpleidingsuitvoeringen moeten variëren gebruikend de zelfde tak.

Met Cloud Manager kunnen deze variabelen per pijpleiding worden geconfigureerd via de Cloud Manager API of Cloud Manager CLI. Variabelen kunnen worden opgeslagen als onbewerkte tekst of in rust worden versleuteld. In beide gevallen worden variabelen binnen de ontwikkelomgeving beschikbaar gemaakt als een omgevingsvariabele waarnaar vervolgens kan worden verwezen vanuit het `pom.xml`-bestand of andere constructiescripts.

Om een variabele te plaatsen die CLI gebruiken, stel een bevel als in werking:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

Huidige variabelen kunnen worden weergegeven:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

Namen van variabelen mogen alleen alfanumerieke tekens en onderstrepingstekens (_) bevatten. Volgens de conventie moeten de namen allemaal hoofdletters zijn. Er is een grens van 200 variabelen per pijpleiding, moet elke naam minder dan 100 karakters zijn en elke waarde moet minder dan 2048 karakters in het geval van koordtypevariabelen en 500 karakters in het geval van geheimString typevariabelen zijn.

Bij gebruik in een `Maven pom.xml`-bestand is het doorgaans handig om deze variabelen toe te wijzen aan Ge-maven-eigenschappen met behulp van een soortgelijke syntaxis:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```


## Extra systeempakketten installeren {#installing-additional-system-packages}

Voor sommige builds moeten extra systeempakketten worden geïnstalleerd om volledig te kunnen functioneren. Een build kan bijvoorbeeld een Python- of ruby-script aanroepen en moet daarom een geschikte taalinterpreter hebben geïnstalleerd. Dit kan worden gedaan door [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) te roepen om APT aan te halen. Deze uitvoering moet doorgaans worden opgenomen in een specifiek Maven-profiel voor Cloud Manager. Zo kunt u bijvoorbeeld python installeren:

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

Deze zelfde techniek kan worden gebruikt om taalspecifieke pakketten te installeren, d.w.z. gebruikend `gem` voor RubyGems of `pip` voor Python Pakketten.

>[!NOTE]
>Als u een systeempakket op deze manier installeert, wordt dit **niet** geïnstalleerd in de runtimeomgeving die voor het uitvoeren van Adobe Experience Manager wordt gebruikt. Als u een systeempakket nodig hebt dat op de AEM-omgeving is geïnstalleerd, neemt u contact op met uw Adobe-vertegenwoordiger.
