---
title: Veelgestelde vragen over Cloud Manager
seo-title: Veelgestelde vragen over Cloud Manager
description: Raadpleeg de veelgestelde vragen over probleemoplossing in Cloud Manager
seo-description: Volg deze pagina om antwoorden te krijgen op veelgestelde vragen over Cloud Manager
translation-type: tm+mt
source-git-commit: cb63a8bbe30b28668313dc851f17aa34fc166474
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---


# Veelgestelde vragen over wolkenbeheer {#cloud-manager-faqs}

In het volgende gedeelte worden antwoorden gegeven op een aantal veelgestelde vragen over Cloud Manager.

## 1. Is het mogelijk om Java 11 te gebruiken met Cloud Manager builds? {#java-11-cloud-manager}

AEM de build van Cloud Manager mislukt wanneer wordt geprobeerd om van Java 8 over te schakelen op Java 11. Het probleem kan vele oorzaken hebben en de meest voorkomende zijn hieronder gedocumenteerd:

* Voeg de plug-in maven-toolketins toe met de juiste instellingen voor Java 11, zoals [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started) wordt beschreven.  Bijvoorbeeld, zie [wint steekproefprojectcode](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Als u de hieronder beschreven fout tegenkomt, moet u het gebruik van de maven-scr-plugin verwijderen en alle OSGi-annotaties omzetten in OSGi R6-annotaties. Zie [hier](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/) voor instructies.

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Voor Cloud Manager bouwt de toegewezen afdwingingsinsteekmodule mislukt met de fout `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Dit is een bekend probleem dat te wijten is aan het gebruik van Cloud Manager met een andere versie van Java voor het uitvoeren van de gemaven opdracht in plaats van het compileren van code. Laat op dit moment `requireJavaVersion` weg uit uw gefabriceerde-handhaving-stop- configuraties.

## 2. Onze implementatie is vastgelopen omdat de kwaliteitscontrole voor de code is mislukt. Is er een manier om deze controle te omzeilen? {#deployment-stuck}

Alle fouten van de Kwaliteit van de Code behalve *de Classificatie van de Veiligheid* zijn niet-kritieke metriek, zodat kunnen zij worden omzeild door de punten in resultatenUI uit te breiden.

Een gebruiker met [De Manager van de Plaatsing, de Manager van het Project, of de rol Bedrijfs van de Eigenaar ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements) kan de kwesties met voeten treden, in welk geval de pijpleiding te werk gaat, of zij kunnen de kwesties goedkeuren, in welk geval de pijpleiding met een mislukking ophoudt.  Zie [Drievoudige poorten tijdens het uitvoeren van een pijplijn](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) voor meer informatie.

## 3. Implementaties van Cloud Manager mislukken bij het testen van de prestaties in omgevingen met Adobe Managed Services. Hoe zuiveren wij dit om de kritieke metriek over te gaan? {#debug-critical-metrics}

Zie [Inzicht in uw testresultaten](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) om de resultaten te begrijpen.

Sommige opmerkingen over de teststap voor de prestaties:

* De *Performance Step* is een stap voor webprestaties. Dit houdt in dat het tijd is om de pagina te laden met een webbrowser.
* De URL&#39;s in het CSV-bestand met resultaten worden tijdens de test in een Chrome-browser in de Cloud Manager-infrastructuur geladen.
* Een gemeenschappelijke metrisch die ontbreekt is *foutentarief*. Een URL kan alleen worden doorgegeven als de hoofd-URL is geladen met de status 200 en binnen 20 seconden. Paginaladen die meer dan 20 seconden duren, worden gemarkeerd als 504 fouten.
* Als voor uw site gebruikersverificatie is vereist, raadpleegt u deze documentatie voor het configureren van de test voor verificatie op uw site.

## 4. Kunnen we SNAPSHOT gebruiken in de versie van het gemaakte project? Hoe werkt het versioning van de pakketten en bundeljar-bestanden voor werkgebied en productie? {#snapshot-version}

1. Voor dev-implementaties moeten de bestanden van de git-vertakking pom.xml -SNAPSHOT bevatten aan het einde van de waarde `<version>`. Dit staat verdere plaatsingen toe waar de versie niet verandert om nog geïnstalleerd te worden. In dev-implementaties wordt er geen automatische versie toegevoegd of gegenereerd voor de gemaskeerde build.

1. In werkgebied en productie wordt een automatische versie gegenereerd, zoals hier wordt beschreven.

1. Voor aangepaste versioning in werkgebied en productieimplementaties stelt u een correcte versie van drie onderdelen in, bijvoorbeeld `1.0.0`. Verhoog de versie telkens als u een andere moet doen opstelt aan productie.

1. Cloud Manager voegt automatisch zijn versie aan stadium toe en de productie bouwt en leidt zelfs tot een git tak. Er is geen speciale configuratie vereist. Als stap 3 hierboven wordt overgeslagen, zou de plaatsing nog goed werken en een versie automatisch worden geplaatst.

1. Als u de versie met `-SNAPSHOT` voor stadium en productie bouwt of opstelt dan is zelfs dat ok. Cloud Manager stelt automatisch een correct versienummer in en maakt een tag voor u in de it. Indien nodig kunt u later naar dit label verwijzen.

1. Als u één of andere experimentele code op dev wilt uitproberen kunt u een nieuwe git tak tot stand brengen en de pijpleiding plaatsen om die verschillende tak te gebruiken.  Dit is nuttig wanneer de plaatsingen beginnen te ontbreken en u met oudere versies van de code zou willen testen om te zien wanneer het brak.

   Met de git-opdracht hieronder maakt u een externe vertakking met de naam *testvertakking1* op basis van een specifieke, reeds bestaande koppeling `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Deze speciale vertakking kan worden gebruikt in Cloud Manager zonder andere vertakkingen te beïnvloeden:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Raadpleeg de [Git-documentatie](https://git-scm.com/book/en/v2/Git-Internals-Git-References) voor meer informatie.

   Als u later de testtak wilt schrappen dan gebruik het schrappingsbevel (duidelijk, ben zorgvuldig met dit bevel):

   `git push origin --delete testbranch1`

## 5. Maven-build mislukt in Cloud Manager, maar wordt lokaal zonder fouten gemaakt. Hoe kan ik fouten opsporen? {#maven-build-fail}

Zie [Git Resource](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) voor meer informatie.

## 6. Kan een variabele niet instellen via via een AIR-cloudmanager ingestelde pijpleidingvariabelen. Hoe te om deze kwesties te zuiveren? {#set-variable}

Als u een fout 403 krijgt wanneer het proberen om pijpleidingsvariabelen via bevelen te vermelden of te plaatsen gelijkend op hieronder, dan moet u als *Manager van de Plaatsing worden toegevoegd* het productrol van de Manager van de Wolk in de admin console.\
Zie [API-machtigingen](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) voor meer informatie.

Verwante opdrachten en fouten:

`$ aio cloudmanager:list-pipeline-variables 222`

Fout: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

Fout: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
