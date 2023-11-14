---
title: De Build-omgeving
description: Meer informatie over de gespecialiseerde ontwikkelomgeving die gebruikers van Cloud Manager gebruiken om uw code te maken en testen.
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 7f9866976667b485124cef60453ec3908ba41ec8
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# De Build-omgeving {#build-environment}

Meer informatie over de gespecialiseerde ontwikkelomgeving die gebruikers van Cloud Manager gebruiken om uw code te maken en testen.

## Omgevingsdetails {#details}

De buildomgevingen van Cloud Manager hebben de volgende kenmerken.

* De ontwikkelomgeving is gebaseerd op Linux en is afgeleid van Ubuntu 18.04.
* Apache Maven 3.8.8 is geïnstalleerd.
* De geïnstalleerde Java-versies zijn Oracle JDK 8u371 en Oracle JDK 11.0.20.
   * `/usr/lib/jvm/jdk1.8.0_371`
   * `/usr/lib/jvm/jdk-11.0.20`
* Standaard worden de `JAVA_HOME`  omgevingsvariabele is ingesteld op `/usr/lib/jvm/jdk1.8.0_371` die Oracle JDK 8u371 bevat. Zie de sectie [JDK-versie van alternatieve uitvoering](#alternate-maven) voor meer informatie.
* Er zijn enkele extra systeempakketten geïnstalleerd die nodig zijn.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Andere pakketten kunnen worden geïnstalleerd tijdens het samenstellen zoals beschreven in de sectie [Extra systeempakketten installeren.](#installing-additional-system-packages)
* Elke build wordt uitgevoerd in een ongerepte omgeving. De bouwstijlcontainer houdt geen staat tussen uitvoeringen.
* Maven wordt altijd uitgevoerd met deze drie opdrachten:
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven is geconfigureerd op systeemniveau met een `settings.xml` bestand dat automatisch de openbare gegevensopslagruimte voor Adoben bevat met een profiel met de naam `adobe-public`.
   * Zie de [Adobe openbare Maven-opslagplaats](https://repo1.maven.org/) voor meer informatie .

>[!NOTE]
>
>Hoewel in Cloud Manager geen specifieke versie van het dialoogvenster `jacoco-maven-plugin`moet de gebruikte versie ten minste `0.7.5.201505241946`.

>[!TIP]
>
>Raadpleeg de volgende aanvullende bronnen voor meer informatie over het gebruik van API&#39;s van Cloud Manager:
>* [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [API-integratie maken](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)
>* [API-machtigingen](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)

## Een specifieke Java-versie gebruiken {#using-java-version}

Standaard worden projecten gemaakt door het buildproces van Cloud Manager met Oracle 8 JDK. Klanten die een alternatieve JDK willen gebruiken, hebben twee opties.

* [Maven Toolketins](#maven-toolchains)
* [Een alternatieve JDK-versie selecteren voor het volledige uitgevoerde Maven-proces](#alternate-maven)

### Maven Toolketins {#maven-toolchains}

De [Maven Toolketins-plug-in](https://maven.apache.org/plugins/maven-toolchains-plugin/) Hiermee kunnen projecten een specifieke JDK (of toolchain) selecteren die moet worden gebruikt in de context van Maven-plug-ins die geschikt zijn voor toolketens. Dit wordt gedaan in het project `pom.xml` door een leverancier- en versiewaarde op te geven. Een voorbeeldsectie in de `pom.xml` bestand is:

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

Wanneer u deze methode gebruikt, wordt Maven zelf nog steeds uitgevoerd met de standaard-JDK (Oracle 8) en de `JAVA_HOME` omgevingsvariabele wordt niet gewijzigd. Daarom de Java-versie controleren of afdwingen via plug-ins zoals de [Insteekmodule Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) werkt niet en dergelijke plug-ins mogen niet worden gebruikt.

De momenteel beschikbare combinaties leverancier/versie zijn:

| Leverancier | Versie |
|---|---|
| oracle | 1.8 |
| oracle | 1.11 |
| oracle | 11 |
| zon | 1.8 |
| zon | 1.11 |
| zon | 11 |

>[!NOTE]
>
>Vanaf april 2022 is Oracle JDK de standaard-JDK voor de ontwikkeling en werking van AEM toepassingen. Het buildproces van Cloud Manager wordt automatisch overgeschakeld op het gebruik van Oracle JDK, zelfs als er expliciet een andere optie is geselecteerd in de Maven-toolchain. Zie [Opmerkingen bij de release van april](/help/release-notes/2022/2022-4-0.md) voor nadere bijzonderheden.

### JDK-versie van alternatieve uitvoering {#alternate-maven}

Het is ook mogelijk om Oracle 8 of Oracle 11 als JDK voor de volledige Geweven uitvoering te selecteren. In tegenstelling tot de opties van toolketins, verandert dit JDK die voor alle stop-ins wordt gebruikt tenzij de toolketenconfiguratie ook wordt geplaatst waarin de toolkettenconfiguratie nog voor toolketens-bewuste Maven plugins wordt toegepast. Hierdoor wordt de Java-versie gecontroleerd en afgedwongen met de [Insteekmodule Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) werkt.

Hiertoe maakt u een bestand met de naam `.cloudmanager/java-version` in de door de pijpleiding gebruikte vertakking van de git-opslagplaats. Dit bestand kan de inhoud hebben `11` of `8`. Eventuele andere waarden worden genegeerd. Indien `11` wordt gespecificeerd, wordt Oracle 11 gebruikt en `JAVA_HOME` omgevingsvariabele is ingesteld op `/usr/lib/jvm/jdk-11.0.2`. Indien `8` wordt gespecificeerd, wordt Oracle 8 gebruikt en `JAVA_HOME` omgevingsvariabele is ingesteld op `/usr/lib/jvm/jdk1.8.0_202`.

## Omgevingsvariabelen {#environment-variables}

### Standaardomgevingsvariabelen {#standard-environ-variables}

In sommige gevallen, kunt u het noodzakelijk vinden om het bouwstijlproces te variëren dat op informatie over het programma of de pijpleiding wordt gebaseerd.

Als JavaScript-miniaturen tijdens het bouwen bijvoorbeeld worden gemaakt met een tool als gulp, is het wellicht verstandig om een ander miniatuurniveau te gebruiken bij het bouwen voor een ontwikkelomgeving in plaats van voor het maken van ophaling en productie.

Ter ondersteuning hiervan voegt Cloud Manager voor elke uitvoering standaardomgevingsvariabelen toe aan de container voor de build.

| Naam variabele | Beschrijving |
|---|---|
| `CM_BUILD` | Altijd instellen op `true` |
| `BRANCH` | De gevormde tak voor de uitvoering |
| `CM_PIPELINE_ID` | De numerieke identificatie van de pijplijn |
| `CM_PIPELINE_NAME` | De pijpleidingsnaam |
| `CM_PROGRAM_ID` | De numerieke programma-id |
| `CM_PROGRAM_NAME` | De programmenaam |
| `ARTIFACTS_VERSION` | Voor een staging- of productiepijplijn wordt de synthetische versie gegenereerd door Cloud Manager |

### Beschikbaarheid van standaardomgevingsvariabele {#availability}

Standaardomgevingsvariabelen kunnen op een aantal plaatsen worden gebruikt.

#### Auteur, Voorvertoning en Publiceren {#author-preview-publish}

Zowel normale omgevingsvariabelen als geheimen kunnen worden gebruikt in de ontwerpomgeving, voorvertoningsomgeving en in de publicatieomgeving.

#### Dispatcher {#dispatcher}

Alleen normale omgevingsvariabelen kunnen worden gebruikt [de verzender.](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) Geheimen kunnen niet worden gebruikt.

Omgevingsvariabelen kunnen echter niet worden gebruikt in `IfDefine` richtlijnen.

>[!TIP]
>
>U moet het gebruik van omgevingsvariabelen valideren met de [lokale verzender](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) vóór implementatie.

#### OSGi-configuraties {#osgi}

Zowel normale omgevingsvariabelen als geheimen kunnen worden gebruikt in [OSGi-configuraties.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html)

### Pipetvariabelen {#pipeline-variables}

In sommige gevallen, kan uw bouwstijlproces van specifieke configuratievariabelen afhangen die om in de git bewaarplaats ongepast zouden zijn te plaatsen of tussen pijpleidinguitvoeringen moeten variëren gebruikend de zelfde tak.

Met Cloud Manager kunnen deze variabelen per pijpleiding worden geconfigureerd via de Cloud Manager API of Cloud Manager CLI. Variabelen kunnen worden opgeslagen als normale tekst of in rust worden versleuteld. In beide gevallen worden variabelen binnen de ontwikkelomgeving beschikbaar gemaakt als een omgevingsvariabele die vervolgens van binnen de `pom.xml` of andere build-scripts.

Om een variabele te plaatsen die CLI gebruiken, stel een bevel in werking gelijkend op het volgende.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Huidige variabelen kunnen worden vermeld gebruikend een bevel gelijkend op het volgende.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Variabelen moeten aan bepaalde beperkingen voldoen.

* Namen van variabelen mogen alleen alfanumerieke tekens en het onderstrepingsteken (`_`).
   * Volgens de conventie moeten de namen allemaal in hoofdletters staan.
* Er is een grens van 200 variabelen per pijpleiding.
* Elke naam moet uit minder dan 100 tekens bestaan.
* Elke tekenreekswaarde moet uit minder dan 2048 tekens bestaan.
* Elke geheimeString-waarde moet uit minder dan en 500 tekens bestaan.

Indien gebruikt in een Maven `pom.xml` , is het doorgaans handig om deze variabelen toe te wijzen aan Maven-eigenschappen met een syntaxis die lijkt op de volgende.

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

Om volledig te functioneren, vereisen sommige bouwstijlen extra systeempakketten worden geïnstalleerd. Een build kan bijvoorbeeld een Python- of Ruby-script aanroepen en moet daarom een geschikte taalinterpreter hebben geïnstalleerd. Dit kan door te roepen [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) om APT aan te roepen. Deze uitvoering moet doorgaans worden opgenomen in een specifiek Maven-profiel voor Cloud Manager. Als u bijvoorbeeld Python wilt installeren:

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
>Als u een systeempakket op deze manier installeert, wordt dit niet geïnstalleerd in de runtimeomgeving die voor het uitvoeren van Adobe Experience Manager wordt gebruikt. Als u een systeempakket nodig hebt dat op de AEM-omgeving is geïnstalleerd, neemt u contact op met uw Adobe-vertegenwoordiger.
