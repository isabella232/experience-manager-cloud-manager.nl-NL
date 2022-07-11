---
title: Veelgestelde vragen over Cloud Manager
description: Dit document bevat antwoorden op de meest gestelde vragen over Cloud Manager voor AMS-klanten.
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6be659e02df0657ec7d3dbce8c18c44a327a36f4
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Veelgestelde vragen over Cloud Manager {#cloud-manager-faqs}

Dit document bevat antwoorden op de meest gestelde vragen over Cloud Manager voor AMS-klanten.

## Is het mogelijk om Java 11 te gebruiken met Cloud Manager builds? {#java-11}

Ja. U moet de opdracht `maven-toolchains-plugin` met de juiste instellingen voor Java 11.

* Dit proces wordt gedocumenteerd [hier.](/help/getting-started/using-the-wizard.md)
* Zie voor een voorbeeld de [wknd-voorbeeldprojectcode.](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)

## Mijn build mislukt met een fout over maven-scr-plugin na het schakelen van Java 8 naar Java 11. Wat kan ik doen? {#maven-src-plugin}

Het is mogelijk dat de build van uw AEM Cloud Manager mislukt wanneer u probeert de build over te schakelen van Java 8 naar 11. Als de volgende fout optreedt, moet u `maven-scr-plugin` en zet alle OSGi-annotaties om in OSGi R6-annotaties.

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

Voor instructies over het verwijderen van deze plug-in: [zie hier.](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## Mijn build mislukt met een fout met betrekking tot RequireJavaVersion na het schakelen van Java 8 naar Java 11. Wat kan ik doen? {#requirejavaversion}

Voor builds van Cloud Manager worden de `maven-enforcer-plugin` kan mislukken met deze fout

```text
[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion
```

Dit is een bekend probleem vanwege het gebruik van een andere Java-versie voor het uitvoeren van de gedeelde opdracht in plaats van het compileren van code. Eenvoudig weglaten `requireJavaVersion` van uw `maven-enforcer-plugin` configuraties.

## De kwaliteitscontrole van de code is mislukt en onze implementatie is vastgelopen. Is er een manier om deze controle te omzeilen? {#deployment-stuck}

Ja. Alle mislukkingen van de codekwaliteit behalve veiligheidsclassificaties zijn niet-kritieke metriek, zodat kunnen zij als deel van een plaatsingspijpleiding worden overgeslagen door de punten in resultatenUI uit te breiden.

Een gebruiker met [Implementatiebeheer, projectmanager of bedrijfseigenaar](/help/requirements/users-and-roles.md#role-definitions) de rol kan de kwesties met voeten treden, waarin de pijpleiding te werk gaat of zij de kwesties kunnen goedkeuren, waarbij de pijpleiding met een mislukking stopt.

Zie de documenten [Drievoudige Gates terwijl het runnen van een Pijpleiding](/help/using/code-quality-testing.md#three-tier-gates-while-running-a-pipeline) en [Niet-productiepijpleidingen configureren](/help/using/non-production-pipelines.md#understanding-the-flow) voor meer informatie .

## Implementaties van Cloud Manager mislukken bij het testen van de prestaties in omgevingen met Adobe Managed Services. Hoe zuiveren wij dit om de kritieke metriek over te gaan? {#debug-critical-metrics}

Er is geen enkel antwoord op deze vraag. Maar dit zijn enkele belangrijke punten met betrekking tot de teststap voor de prestaties die u in gedachten moet houden:

* Deze stap is een stap in de webprestaties, d.w.z. de tijd om de pagina met een webbrowser te laden.
* De URL&#39;s die in het CSV-bestand met resultaten worden vermeld, worden tijdens de test in een Chrome-browser in de Cloud Manager-infrastructuur geladen.
* Een gemeenschappelijke metrisch die ontbreekt is het foutentarief.
   * Een URL kan alleen worden doorgegeven als de hoofd-URL is geladen met `200` status en in minder dan `20` seconden.
   * Pagina wordt geladen die groter is dan `20` seconden worden gemarkeerd als `504` fouten.
* Raadpleeg het document als gebruikersverificatie vereist is voor uw site [De testresultaten begrijpen](/help/using/code-quality-testing.md#authenticated-performance-testing) voor het configureren van de test voor verificatie op uw site.

Zie het document [Testresultaten begrijpen](/help/using/code-quality-testing.md) voor meer informatie over kwaliteitscontroles.

## Kan ik SNAPSHOT voor de versie van het Maven project gebruiken? {#snapshot}

Ja. Voor ontwikkelaarsplaatsingen, de git tak `pom.xml` bestanden moeten bevatten `-SNAPSHOT` aan het einde van de `<version>` waarde.

Dit laat verdere plaatsing toe om nog worden geïnstalleerd wanneer de versie niet veranderde. In ontwikkelaarsplaatsingen, wordt geen automatische versie toegevoegd of geproduceerd voor de beproefde bouwstijl.

U kunt de versie ook instellen op `-SNAPSHOT` voor stadium- en productiegebouwen of -implementaties. Cloud Manager stelt automatisch een correct versienummer in en maakt een tag voor u in de it. Indien nodig kunt u later naar dit label verwijzen.

Meer informatie over versiebeheer vindt u op [Hier gedocumenteerd.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/project-version-handling.html)

## Hoe werkt het pakket en de bundelversioning voor het opvoeren en productieplaatsingen? {#staging-production}

In het opvoeren en productieplaatsingen, wordt een automatische versie geproduceerd [zoals hier beschreven.](/help/managing-code/maven-project-version.md)

Voor aangepaste versioning in werkgebied- en productieimplementaties stelt u een correcte versie met drie delen in, zoals `1.0.0`. Verhoog de versie telkens wanneer u aan productie opstelt.

Cloud Manager voegt automatisch zijn versie aan stadium toe en de productie bouwt en leidt tot een git tak. Er is geen speciale configuratie vereist. Als u een bepaalde versie niet zoals eerder beschreven plaatst, zal de plaatsing nog slagen en een versie zal automatisch worden geplaatst.

## Mijn gefabriceerde build mislukt voor implementaties van Cloud Manager, maar het wordt lokaal zonder fouten gemaakt. Wat is er mis? {#maven-build-fail}

Zie dit [git-resource](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) voor meer informatie .

## Ik kan geen variabele plaatsen gebruikend een bevel van de lucht. Wat kan ik doen? {#set-variable}

U kunt een fout van 403 zoals het volgende ontvangen wanneer het proberen om pijpleidingsvariabelen te maken of te plaatsen via `aio` opdrachten.

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

In dit geval moet de gebruiker die deze opdrachten uitvoert, worden toegevoegd aan de opdracht **Implementatiebeheer** rol in de Admin Console.

Zie [API-machtigingen](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/) voor meer informatie .
