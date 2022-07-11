---
title: Dispatcher Configurations
description: Leer hoe u configuratiebestanden voor verzenders kunt implementeren met Cloud Manager.
exl-id: ffc2b60e-bde7-48ca-b268-dea0f8fd4e30
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Dispatcher Configurations {#manage-your-dispatcher-configurations}

Leer hoe u configuratiebestanden voor verzenders kunt implementeren met Cloud Manager

## Dispatcher-configuraties implementeren met Cloud Manager {#deploying-dispatcher-configurations}

Cloud Manager kan webserver- en Dispatcher-configuratiebestanden implementeren op basis van de veronderstelling dat deze samen met normale AEM-inhoudspakketten zijn opgeslagen in de git-opslagplaats.

Als u van deze mogelijkheid gebruik wilt maken, moet de Maven-build een ZIP-bestand maken dat ten minste twee mappen bevat: `conf` en `conf.d`. Dit ZIP-bestand kan worden gemaakt met het `maven-assembly-plugin`.

Projecten die zijn gegenereerd door Cloud Manager met de ingebouwde [wizard voor het maken van projecten](/help/getting-started/using-the-wizard.md) de juiste automatisch gemaakte Maven-projectstructuur hebben. Dit is het aanbevolen pad als u nog geen ervaring hebt met Adobe Managed Services (AMS).

Bij plaatsing aan een instantie van de verzender, wordt de inhoud van deze folders op de instantie van de Verzender overschreven door die in uw git bewaarplaats. Aangezien de de configuratiedossiers van de Webserver en van de Verzender regelmatig milieu-specifieke informatie vereisen om dit vermogen correct te gebruiken, zult u eerst met uw Ingenieurs van het Succes van de Klant (CSE) moeten werken om deze milieuvariabelen te plaatsen in `/etc/sysconfig/httpd`.

## Dispatcher Configuration for Existing Managed Service Customers {#steps-for-configuring-dispatcher}

Voer de volgende stappen uit om de eerste configuratie van Dispatcher te voltooien.

1. Verkrijg de huidige dossiers van de productieconfiguratie van uw CSE.
1. Verwijder hard-gecodeerde milieu-specifieke gegevens zoals publiceer renderer IP en vervang door variabelen.
1. Definieer vereiste variabelen in sleutel-waardeparen voor elk doelVerzender en verzoek uw CSE om hen toe te voegen aan `/etc/sysconfig/httpd` op elk exemplaar.
1. Test de bijgewerkte configuraties in uw testomgeving.
1. Zodra getest, verzoek uw CSE om aan productie op te stellen.
1. Leg de bestanden vast in uw it-opslagplaats.
1. Implementeer via Cloud Manager.

>[!NOTE]
>
>Het migreren van Dispatcher- en webserverconfiguraties naar uw it-opslagplaats kan plaatsvinden tijdens het instappen van Cloud Manager, maar kan ook op een later tijdstip worden uitgevoerd.

### Voorbeeld {#example}

De specifieke dossier en folderstructuur kunnen variëren gebaseerd op de details van uw project, maar dit voorbeeld zou een concrete gids voor hoe te om uw project te structureren om configuraties Apache en Dispatcher te omvatten.

1. Een submap maken met de naam `dispatcher`.

   U kunt hier elke naam gebruiken, maar de mapnaam die in deze stap wordt gemaakt, moet dezelfde zijn als de naam die in stap 6 wordt gebruikt.

1. Deze subdirectory bevat een module Maven die het ZIP-bestand van Dispatcher maakt met de plug-in Maven Assembly. Om dit te beginnen, in `dispatcher` map, een `pom.xml` bestand met deze inhoud, wijzigen `parent` referentie; `artifactId`, en `name` indien nodig.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
       <modelVersion>4.0.0</modelVersion>
       <parent>
           <!-- reference to your parent pom -->
       </parent>
   
       <artifactId>dispatcher</artifactId> <!-- feel free to change this -->
       <packaging>pom</packaging>
       <name>dispatcher</name> <!-- feel free to change this -->
   
       <build>
           <plugins>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-assembly-plugin</artifactId>
                   <version>3.1.0</version>
                   <executions>
                       <execution>
                           <phase>package</phase>
                           <goals><goal>single</goal></goals>
                           <configuration>
                               <descriptors>
                                   <descriptor>assembly.xml</descriptor>
                               </descriptors>
                               <appendAssemblyId>false</appendAssemblyId>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   </project>
   ```

   * Zoals in Stap 1, kunnen artefactId en de naam hier andere waarden zijn als u wilt. `dispatcher` wordt hier slechts een voorbeeld gebruikt.

1. Voor de plug-in Maven Assembly is een `descriptor` om te bepalen hoe het .zip dossier wordt gecreeerd. Als u deze descriptor wilt maken, maakt u een bestand in het dialoogvenster `dispatcher` submap genaamd `assembly.xml` met de volgende inhoud. Er wordt naar deze bestandsnaam verwezen op regel 26 in het dialoogvenster `pom.xml` bestand hierboven.

   ```xml
   <assembly xmlns="http://maven.apache.org/ASSEMBLY/2.0.0"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/ASSEMBLY/2.0.0 http://maven.apache.org/xsd/assembly-2.0.0.xsd">
     <id>distribution</id>
     <formats>
       <format>zip</format>
     </formats>
     <includeBaseDirectory>false</includeBaseDirectory>
     <fileSets>
       <fileSet>
         <directory>${basedir}/src</directory>
         <includes>
           <include>**/*</include>
         </includes>
         <outputDirectory></outputDirectory>
       </fileSet>
     </fileSets>
   </assembly>
   ```

1. Een submap maken met de naam `src` (zoals vermeld in de verzamelingsbeschrijving hierboven op regel 11) binnen de submap dispatcher om de werkelijke Apache- en Dispatcher-configuraties op te slaan. Binnen deze `src` map, mappen maken met de naam `conf`, `conf.d`, `conf.dispatcher.d`, en `conf.modules.d`.

1. Vul de `conf`, `conf.d`, `conf.dispatcher.d`, en `conf.modules.d` mappen met uw configuratiebestanden. De standaardconfiguratie bestaat bijvoorbeeld uit deze bestanden en symbolische koppelingen.

   ```
   dispatcher
   ├── assembly.xml
   ├── pom.xml
   └── src
       ├── conf
       │  ├── httpd.conf
       │  └── magic
       ├── conf.d
       │  ├── README
       │  ├── autoindex.conf
       │  ├── available_vhosts
       │  │  ├── aem_author.vhost
       │  │  ├── aem_flush.vhost
       │  │  ├── aem_health.vhost
       │  │  ├── aem_lc.vhost
       │  │  └── aem_publish.vhost
       │  ├── dispatcher_vhost.conf
       │  ├── enabled_vhosts
       │  │  ├── aem_author.vhost -> ../available_vhosts/aem_author.vhost
       │  │  ├── aem_flush.vhost -> ../available_vhosts/aem_flush.vhost
       │  │  └── aem_publish.vhost -> ../available_vhosts/aem_publish.vhost
       │  ├── rewrites
       │  │  ├── base_rewrite.rules
       │  │  └── xforwarded_forcessl_rewrite.rules
       │  ├── userdir.conf
       │  ├── variables
       │  │  └── ams_default.vars
       │  ├── welcome.conf
       │  └── whitelists
       │      └── 000_base_whitelist.rules
       ├── conf.dispatcher.d
       │  ├── available_farms
       │  │  ├── 000_ams_author_farm.any
       │  │  ├── 001_ams_lc_farm.any
       │  │  └── 999_ams_publish_farm.any
       │  ├── cache
       │  │  ├── ams_author_cache.any
       │  │  ├── ams_author_invalidate_allowed.any
       │  │  ├── ams_publish_cache.any
       │  │  └── ams_publish_invalidate_allowed.any
       │  ├── clientheaders
       │  │  ├── ams_author_clientheaders.any
       │  │  ├── ams_common_clientheaders.any
       │  │  ├── ams_lc_clientheaders.any
       │  │  └── ams_publish_clientheaders.any
       │  ├── dispatcher.any
       │  ├── enabled_farms
       │  │  ├── 000_ams_author_farm.any -> ../available_farms/000_ams_author_farm.any
       │  │  └── 999_ams_publish_farm.any -> ../available_farms/999_ams_publish_farm.any
       │  ├── filters
       │  │  ├── ams_author_filters.any
       │  │  ├── ams_lc_filters.any
       │  │  └── ams_publish_filters.any
       │  ├── renders
       │  │  ├── ams_author_renders.any
       │  │  ├── ams_lc_renders.any
       │  │  └── ams_publish_renders.any
       │  └── vhosts
       │      ├── ams_author_vhosts.any
       │      ├── ams_lc_vhosts.any
       │      └── ams_publish_vhosts.any
       └── conf.modules.d
           ├── 00-base.conf
           ├── 00-dav.conf
           ├── 00-lua.conf
           ├── 00-mpm.conf
           ├── 00-proxy.conf
           ├── 00-systemd.conf
           ├── 01-cgi.conf
           └── 02-dispatcher.conf
   ```

1. Tot slot, in het `pom.xml` dossier in de wortel van uw project, voeg een `<module>` -element dat de verzendermodule moet bevatten.

   Bijvoorbeeld als uw bestaande modulelijst is

   ```xml
       <modules>
           <module>core</module>
           <module>ui.apps</module>
           <module>ui.content</module>
       </modules>
   ```

   U moet het wijzigen in

   ```xml
       <modules>
           <module>core</module>
           <module>ui.apps</module>
           <module>ui.content</module>
           <module>dispatcher</module>
       </modules>
   ```

   * Zoals vermeld in stap 1, de waarde van de `<module>` -element moet overeenkomen met de gemaakte mapnaam.

1. Uitvoeren om te testen `mvn clean package` in de hoofdmap van het project. U zou lijnen als dit in de output moeten zien.

   ```
   [INFO] --- maven-assembly-plugin:3.1.0:single (default) @ dispatcher ---
   [INFO] Reading assembly descriptor: assembly.xml
   [INFO] Building zip: /Users/me/mycompany/dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
   ```

   U kunt dit bestand ook decomprimeren om de inhoud ervan weer te geven.

   ```shell
   $ unzip -l dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
   Archive:  dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
     Length      Date    Time    Name
   ---------  ---------- -----   ----
           0  09-12-2018 12:53   conf.modules.d/
           0  10-19-2018 10:38   conf.dispatcher.d/
           0  09-12-2018 12:53   conf.dispatcher.d/available_farms/
           0  09-12-2018 12:53   conf.dispatcher.d/filters/
           0  09-12-2018 12:53   conf.dispatcher.d/renders/
           0  09-12-2018 12:53   conf.dispatcher.d/cache/
           0  09-12-2018 12:53   conf.dispatcher.d/clientheaders/
           0  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/
           0  09-12-2018 12:53   conf.dispatcher.d/vhosts/
           0  09-12-2018 12:53   conf.d/
           0  09-12-2018 12:53   conf.d/rewrites/
           0  09-12-2018 12:53   conf.d/whitelists/
           0  09-12-2018 12:53   conf.d/variables/
           0  11-01-2018 13:53   conf.d/enabled_vhosts/
           0  09-12-2018 12:53   conf.d/available_vhosts/
           0  09-12-2018 12:53   conf/
          88  09-12-2018 12:53   conf.modules.d/00-systemd.conf
        4913  09-12-2018 12:53   conf.dispatcher.d/available_farms/999_ams_publish_farm.any
         152  09-12-2018 12:53   conf.dispatcher.d/renders/ams_lc_renders.any
         490  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_common_clientheaders.any
        1727  09-12-2018 12:53   conf.d/rewrites/base_rewrite.rules
          36  09-12-2018 12:53   conf.d/enabled_vhosts/aem_author.vhost
       11753  09-12-2018 12:53   conf/httpd.conf
         957  09-12-2018 12:53   conf.modules.d/00-proxy.conf
         944  09-12-2018 12:53   conf.dispatcher.d/available_farms/001_ams_lc_farm.any
         220  09-12-2018 12:53   conf.dispatcher.d/cache/ams_author_invalidate_allowed.any
          43  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any
         516  09-12-2018 12:53   conf.d/welcome.conf
          37  09-12-2018 12:53   conf.d/enabled_vhosts/aem_publish.vhost
       13077  09-12-2018 12:53   conf/magic
          96  09-12-2018 12:53   conf.modules.d/02-dispatcher.conf
        2601  09-12-2018 12:53   conf.dispatcher.d/available_farms/000_ams_author_farm.any
         837  09-12-2018 12:53   conf.dispatcher.d/cache/ams_author_cache.any
          42  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/000_ams_author_farm.any
        2926  09-12-2018 12:53   conf.d/autoindex.conf
        2555  09-12-2018 12:53   conf.d/available_vhosts/aem_lc.vhost
          41  09-12-2018 12:53   conf.modules.d/00-lua.conf
        2234  09-12-2018 12:53   conf.dispatcher.d/filters/ams_publish_filters.any
         220  09-12-2018 12:53   conf.dispatcher.d/cache/ams_publish_invalidate_allowed.any
         402  09-12-2018 12:53   conf.dispatcher.d/dispatcher.any
         573  09-12-2018 12:53   conf.d/whitelists/000_base_whitelist.rules
         871  09-12-2018 12:53   conf.d/available_vhosts/aem_flush.vhost
         139  09-12-2018 12:53   conf.modules.d/00-dav.conf
         742  09-12-2018 12:53   conf.dispatcher.d/filters/ams_author_filters.any
         557  09-12-2018 12:53   conf.dispatcher.d/cache/ams_publish_cache.any
         105  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_lc_vhosts.any
         101  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_publish_vhosts.any
        3582  09-12-2018 12:53   conf.d/dispatcher_vhost.conf
        2529  09-12-2018 12:53   conf.d/available_vhosts/aem_publish.vhost
         742  09-12-2018 12:53   conf.modules.d/00-mpm.conf
          88  09-12-2018 12:53   conf.dispatcher.d/filters/ams_lc_filters.any
         177  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_lc_clientheaders.any
         366  09-12-2018 12:53   conf.d/README
        2723  09-12-2018 12:53   conf.d/available_vhosts/aem_author.vhost
        3739  09-12-2018 12:53   conf.modules.d/00-base.conf
         138  09-12-2018 12:53   conf.dispatcher.d/renders/ams_author_renders.any
          44  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any
         112  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_author_vhosts.any
         580  09-12-2018 12:53   conf.d/variables/ams_default.vars
          35  09-12-2018 12:53   conf.d/enabled_vhosts/aem_flush.vhost
        1252  09-12-2018 12:53   conf.d/userdir.conf
         451  09-12-2018 12:53   conf.modules.d/01-cgi.conf
         321  09-12-2018 12:53   conf.dispatcher.d/renders/ams_publish_renders.any
         170  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_author_clientheaders.any
         220  09-12-2018 12:53   conf.d/rewrites/xforwarded_forcessl_rewrite.rules
        1753  09-12-2018 12:53   conf.d/available_vhosts/aem_health.vhost
   ---------                     -------
       69017                     66 files
   ```
