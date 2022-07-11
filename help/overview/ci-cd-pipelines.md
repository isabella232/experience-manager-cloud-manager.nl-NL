---
title: CI/CD-pijpleidingen
description: Leer meer over CI/CD-pijpleidingen en hoe ze implementaties in testomgevingen en productieomgevingen in Cloud Manager verwerken.
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# CI/CD-pijpleidingen {#ci-cd-pipeline}

Leer meer over CI/CD-pijpleidingen en hoe ze implementaties in testomgevingen en productieomgevingen in Cloud Manager verwerken.

## Overzicht {#overview}

[!UICONTROL Cloud Manager] omvat een ononderbroken integratie/ononderbroken levering (CI/CD) kader, dat implementatieteams toestaat om nieuwe of bijgewerkte code snel te testen en te leveren. Bijvoorbeeld, kunnen de implementatieteams opstelling, vormen, en beginnen een geautomatiseerde pijpleiding CI/CD die Adobe coderend beste praktijken gebruikt om een grondig codescans uit te voeren en de hoogste codekwaliteit te verzekeren.

De CI/CD pijpleiding automatiseert ook eenheid en prestaties testende processen om plaatsingsefficiency te verhogen en proactief kritieke kwesties identificeren die na plaatsing duur zijn om te bevestigen. Implementatieteams hebben toegang tot een uitgebreid rapport met codeprestaties om inzicht te krijgen in mogelijke gevolgen voor KPI&#39;s en kritieke beveiligingsvalidaties als de code wordt geïmplementeerd in de productie.

## Het pijpleidingproces {#pipeline-process}

In dit diagram wordt getoond wat er gebeurt wanneer een release wordt geactiveerd. [!UICONTROL Cloud Manager] via een pijpleiding.

![Het pijpleidingproces](/help/assets/screen_shot_2018-05-30at82457pm.png)

| Pipetstap | Beschrijving |
|---|---|
| 1. Een release starten | Een plaatsingsmanager brengt of manueel een versie teweeg, met een it begaat, of gebaseerd op een terugkomende planning. |
| 2. Release-tag maken | [!UICONTROL Cloud Manager] maakt een tag git om de release te markeren met een automatisch gegenereerd versienummer, bijvoorbeeld `2018.531.245527.0000001222`. |
| 3. Gebouwd als release met automatisch gegenereerde versie | [!UICONTROL Cloud Manager] bouwt de toepassing met het onlangs-toegewezen versieaantal. |
| 4. Codekwaliteit evalueren | [!UICONTROL Cloud Manager] scant de broncode en verstrekt een samenvatting alvorens de code aan het opvoeren milieu kan worden opgesteld. |
| 5. Versioned artefact(s) opgeslagen | De versieartefacten worden opgeslagen voor later gebruik in de plaatsingsstappen. |
| 6. Automatische implementatie van artefact(en) op AMS-AEM | Het releaseartefact wordt geïmplementeerd in de testomgeving. |
| 7. Automatische tests activeren | [!UICONTROL Cloud Manager] voert prestaties en veiligheidstests op het artefact uit. |
| 8. Implementatie van productitrigger | Nadat de geautomatiseerde tests zijn voltooid, [!UICONTROL Cloud Manager] start de inzet voor productie. |
| 9. [!UICONTROL Cloud Manager] haalt artefacten op die moeten worden geïmplementeerd | [!UICONTROL Cloud Manager] trekt de opgeslagen versieartefacten. |
| 10 Artefacten implementeren voor productie | De releaseartefacten worden ingezet in de productieomgeving. |

### Hoe te Opstelling een CI/CD pijpleiding {#how-to-setup-a-ci-cd-pipeline}

Meer over pijpleidingsconfiguratie leren, zie de documenten [Productiepijpleidingen configureren](/help/using/production-pipelines.md) en [Niet-productiepijpleidingen configureren.](/help/using/non-production-pipelines.md)

## Kwaliteitsgates {#quality-gates}

De pijpleiding CI/CD verstrekt kwaliteitsspoorten, of goedkeuringscriteria, die moeten worden voldaan alvorens de code van het opvoerende milieu aan het plaatsingsmilieu kan worden verplaatst. Er liggen drie poorten in de pijplijn:

* Codekwaliteit
* Prestatietesten
* Beveiligingstests

Voor elk van deze poorten kunnen drie niveaus worden vastgesteld:

* **Kritiek** - Kritieke kwesties die door de poort worden geïdentificeerd, veroorzaken een onmiddellijke mislukking van de pijpleiding.
* **Belangrijk** - Belangrijke kwesties die door de poort worden geïdentificeerd zorgen ervoor dat de pijpleiding een gepauzeerde staat ingaat. Een plaatsingsmanager, projectmanager, of bedrijfseigenaar kunnen of de kwesties met voeten treden, waarin de pijpleiding te werk gaat, of zij kunnen de kwesties goedkeuren, in welk geval de pijpleiding met een mislukking stopt.
* **Informatie** - De door de poort geïdentificeerde informatie wordt uitsluitend ter informatie verstrekt en heeft geen invloed op de uitvoering van de pijpleiding.

Dit is een voorbeeld van een codescan met geïdentificeerde problemen.

![Voorbeeld van codescan](/help/assets/quality-gate-failed.png)

### Gates instellen {#how-to-setup-gates}

Zie het document [Productiepijpleidingen configureren](/help/using/production-pipelines.md) voor meer informatie over het instellen van uw code, kwaliteit en prestatiegraad.
