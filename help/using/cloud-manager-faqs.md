---
title: Veelgestelde vragen over Cloud Manager
seo-title: Cloud Manager FAQs
description: Raadpleeg de veelgestelde vragen over probleemoplossing in Cloud Manager
seo-description: Follow this page to get answers on Cloud Manager FAQs
feature: Getting Started
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6dce1f48b66c6970c3ba025031f0adcbd01195dd
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# Veelgestelde vragen over Cloud Manager {#cloud-manager-faqs}

In het volgende gedeelte worden antwoorden gegeven op veelgestelde vragen over Cloud Manager.

## Is het mogelijk om Java 11 te gebruiken met Cloud Manager builds? {#java-11-cloud-manager}

AEM de build van Cloud Manager mislukt tijdens een poging om te schakelen van Java 8 naar 11. Het probleem kan vele oorzaken hebben en de meest voorkomende zijn hieronder gedocumenteerd:

* Voeg de plug-in Gemaakt-toolketens toe met de juiste instellingen voor Java 11, zoals wordt beschreven [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started).  Zie bijvoorbeeld de [code van wknwdb-voorbeeldproject](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* Als u hieronder de fout tegenkomt, moet u het gebruik van `maven-scr-plugin` en zet alle OSGi-annotaties om in OSGi R6-annotaties. Zie voor instructies [hier](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Voor het samenstellen van Cloud Manager mislukt de gemaakte insteekmodule voor afdwingbare bestanden met een fout `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. Dit is een bekend probleem vanwege het gebruik van een andere Java-versie voor het uitvoeren van de gedeelde opdracht in plaats van het compileren van code. Op dit moment weglaten `requireJavaVersion` van uw gefabriceerde afdwingbare plug-inconfiguraties.

## Onze implementatie is vastgelopen omdat de kwaliteitscontrole van de code is mislukt. Is er een manier om deze controle te omzeilen? {#deployment-stuck}

Ja. Alle fouten in de codekwaliteit, behalve *Beveiligingsbeoordeling* zijn niet-kritieke metriek, zodat kunnen zij als deel van een plaatsingspijpleiding worden overgeslagen door de punten in resultatenUI uit te breiden.

Een gebruiker met [Implementatiebeheer, projectmanager of bedrijfseigenaar](/help/using/setting-up-users-and-roles.md#role-definitions) de rol kan de kwesties met voeten treden, waarin de pijpleiding te werk gaat of zij de kwesties kunnen goedkeuren, waarbij de pijpleiding met een mislukking stopt.

Zie de documenten [Drievoudige Gates terwijl het runnen van een Pijpleiding](/help/using/understand-your-test-results.md#three-tier-gates-while-running-a-pipeline) en [Niet-productiepijpleidingen configureren](/help/using/configuring-non-production-pipelines.md#understanding-the-flow) voor meer informatie .

## Implementaties van Cloud Manager mislukken bij het testen van de prestaties in omgevingen met Adobe Managed Services. Hoe zuiveren wij dit om de kritieke metriek over te gaan? {#debug-critical-metrics}

Zie [De testresultaten begrijpen](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use) de resultaten te begrijpen.

Sommige notities over de stap Prestatietest:

* De *Prestatiestap* is een stap in de webprestaties, dat wil zeggen de tijd om de pagina te laden met een webbrowser.
* De URL&#39;s in het resultaat *CSV* worden tijdens de test in een Chrome-browser geladen in de Cloud Manager-infrastructuur.
* Een gemeenschappelijke metrisch die ontbreekt is *foutenfrequentie*. Een URL kan alleen worden doorgegeven als de hoofd-URL is geladen met `200` status en in minder dan `20` seconden. Pagina wordt geladen die groter is dan `20` seconden worden gemarkeerd als `504` fouten.
* Raadpleeg het document als gebruikersverificatie vereist is voor uw site [De testresultaten begrijpen](understand-your-test-results.md#authenticated-performance-testing) voor het configureren van de test voor verificatie voor uw site.

## Kunnen wij SNAPSHOT in de versie van het Maven project gebruiken? Hoe werkt het versioning van pakketten en bundeljar-bestanden voor werkgebied- en productieimplementaties? {#snapshot-version}

Raadpleeg de volgende scenario&#39;s voor meer informatie over het versieren van pakketten en bundeljar-bestanden voor werkgebied- en productieimplementaties:

1. Voor ontwikkelaarsplaatsingen, de tak van de it `pom.xml` bestanden moeten bevatten `-SNAPSHOT` aan het einde van de `<version>` waarde. Dit staat verdere plaatsing toe waar de versie niet verandert om nog geïnstalleerd te worden. In ontwikkelaarsplaatsingen, wordt geen automatische versie toegevoegd of geproduceerd voor de beproefde bouwstijl.

1. In de implementatie van werkgebied en productie wordt een automatische versie gegenereerd zoals wordt gedocumenteerd [hier](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code).

1. Stel voor aangepaste versies in werkgebied- en productieimplementaties een correcte versie van drie onderdelen in, zoals `1.0.0`. Verhoog de versie telkens als u een andere moet doen opstelt aan productie.

1. Cloud Manager voegt automatisch zijn versie toe aan Stage en Production builds en maakt zelfs een Git-vertakking. Er is geen speciale configuratie vereist. Als stap 3 hierboven wordt overgeslagen, zou de plaatsing nog goed werken en een versie automatisch worden geplaatst.

1. Er zijn geen problemen als u de versie bij laat `-SNAPSHOT` voor Stage en Production builds of implementaties. Cloud Manager stelt automatisch een correct versienummer in en maakt een tag voor u in Git. Indien nodig kunt u later naar dit label verwijzen.

1. Als u één of andere experimentele code op het milieu van de Ontwikkeling wilt uitproberen, kunt u een nieuwe tak van de Git tot stand brengen en de pijpleiding plaatsen om die verschillende tak te gebruiken. Dit is nuttig wanneer de plaatsingen beginnen te ontbreken en u met oudere versies van de code zou willen testen om te zien wanneer het brak.

   Met de opdracht Git hieronder maakt u een externe vertakking met de naam *testbank1* tegen een specifieke, reeds bestaande verbintenis `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  Deze speciale vertakking kan worden gebruikt in Cloud Manager zonder andere vertakkingen te beïnvloeden:

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   Zie de [Git-documentatie](https://git-scm.com/book/en/v2/Git-Internals-Git-References) voor meer informatie .

   Als u de testtak later wilt schrappen, dan gebruik het schrappingsbevel:

   `git push origin --delete testbranch1`

## Maven-build mislukt in Cloud Manager, maar wordt lokaal zonder fouten gemaakt. Hoe kan ik fouten opsporen? {#maven-build-fail}

Zie [Git Resource](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) voor meer informatie .

## Kan een variabele niet instellen via via een AIR-cloudmanager ingestelde pijpleidingvariabelen. Hoe te om deze kwesties te zuiveren? {#set-variable}

Als u een `403` fout wanneer het proberen om pijpleidingsvariabelen via bevelen te maken of te plaatsen gelijkend op hieronder, dan moet u als a worden toegevoegd *Implementatiebeheer* De productrol van Cloud Manager in de Admin Console.\
Zie [API-machtigingen](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) voor meer informatie .

Verwante opdrachten en fouten:

`$ aio cloudmanager:list-pipeline-variables 222`

*Fout*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*Fout*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
