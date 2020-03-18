---
title: CI/CD Pipet
seo-title: CI/CD Pipet
description: 'null'
seo-description: Volg deze sectie om over de pijpleiding te leren CI/CD, die plaatsingen aan stadium en productie in de Manager van de Wolk behandelt.
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
translation-type: tm+mt
source-git-commit: 8580cec50ac5dafb4e2525371a39d58c82f1cbc9

---


# CI/CD Pipet {#ci-cd-pipeline}

## Overzicht van pijplijn {#pipeline-overview}

[!UICONTROL Cloud Manager] Dit omvat een raamwerk voor continue integratie (CI) en continue levering (CD), waarmee implementatieteams snel nieuwe of bijgewerkte code kunnen testen en leveren. Implementatieteams kunnen bijvoorbeeld een geautomatiseerde CI/CD-pijplijn instellen, configureren en starten die de best practices voor Adobe-codering gebruikt om een grondige codescan uit te voeren en de hoogste codekwaliteit te garanderen.

De CI/CD pijpleiding automatiseert ook eenheid en prestaties testende processen om plaatsingsefficiency te verhogen en pro-actief kritieke kwesties te identificeren die duur zijn om na plaatsing te bevestigen. Implementatieteams hebben toegang tot een uitgebreid rapport met codeprestaties om inzicht te krijgen in mogelijke gevolgen voor KPI&#39;s en kritieke beveiligingsvalidaties als de code wordt geïmplementeerd in de productie.

## Pipetproces {#pipeline-process}

In het volgende diagram ziet u wat er gebeurt wanneer een release wordt geactiveerd [!UICONTROL Cloud Manager]. In de bijgevoegde tabel wordt elke stap in de workflow uitgelegd.

![](assets/screen_shot_2018-05-30at82457pm.png)

In de volgende tabel wordt aangegeven wat er in elke stap van het proces gebeurt:

| Stap in pijplijnproces | Wat is er aan de hand? |
|---|---|
| 1. Een release starten | Een plaatsingsmanager brengt of manueel een versie teweeg, met een Git begaan of gebaseerd op een terugkerend programma. |
| 2. Release-tag maken | [!UICONTROL Cloud Manager] Hiermee maakt u een Git-tag om de release te markeren met een automatisch gegenereerd versienummer. Bijvoorbeeld: 2018 531 245527 000000122 |
| 3. Gebouwd als Versie met auto-geproduceerde versie | [!UICONTROL Cloud Manager] bouwt de toepassing met het onlangs-toegewezen versieaantal. |
| 4. Codekwaliteit evalueren | [!UICONTROL Cloud Manager] scant de broncode en verstrekt een samenvatting alvorens de code aan het werkgebiedmilieu kan worden opgesteld |
| 5. Opgeslagen artefact(en) | De versieartefacten worden opgeslagen voor later gebruik in de plaatsingsstappen. |
| 6. Automatische implementatie van Artefact(en) in AMS AEM Stage | Het releaseartefact wordt geïmplementeerd in de werkgebiedomgeving. |
| 7. Automatische tests activeren | [!UICONTROL Cloud Manager] stelt de tests van Prestaties en van de Veiligheid op het artefact in werking. |
| 8. Implementatie van productieactivering | Nadat de geautomatiseerde tests volledig zijn [!UICONTROL Cloud Manager] begint de plaatsing aan productie. |
| 9. Te implementeren artefacten [!UICONTROL Cloud Manager] ophalen | [!UICONTROL Cloud Manager] trekt de opgeslagen versieartefacten. |
| 10 Artefacten aan productie verstrekken | De releaseartefacten worden opgesteld aan het milieu van de Productie. |

### Hoe te opstelling een CI/CD Pijpleiding {#how-to-setup-a-ci-cd-pipeline}

Meer over pijpleidingsconfiguratie leren, zie [het vormen pijpleiding](configuring-pipeline.md).

## Kwaliteitsgates {#quality-gates}

De pijpleiding CI/CD verstrekt kwaliteitsspoorten, of aanvaardingscriteria, die moeten worden voldaan alvorens de code van het werkgebiedmilieu aan het plaatsingsmilieu kan worden verplaatst. Er liggen drie poorten in de pijplijn:

* Codekwaliteit
* Prestatietesten
* Beveiligingstests

Voor elk van deze poorten zijn drie niveaus van problemen vastgesteld:

* **Kritiek** - door de poort geïdentificeerde problemen die een onmiddellijk uitvallen van de pijpleiding veroorzaken.
* **Belangrijk** - kwesties die door de poort worden geïdentificeerd die de pijpleiding veroorzaken om een gepauzeerde staat in te gaan. Een plaatsingsmanager, projectmanager, of bedrijfseigenaar kunnen of de kwesties met voeten treden, waarin de pijpleiding te werk gaat, of zij kunnen de kwesties goedkeuren, in welk geval de pijpleiding met een mislukking stopt.
* **Informatie** - door de poort geïdentificeerde kwesties die uitsluitend ter informatie worden verstrekt en geen invloed hebben op de uitvoering van de pijpleiding.

Hieronder ziet u een voorbeeld van een codescannen met problemen die zijn geïdentificeerd voor de code:

![](assets/quality-gate-failed.png)

### Gates instellen {#how-to-setup-gates}

Zie Gates **[](configuring-pipeline.md)**configureren voor meer informatie over het instellen van code, kwaliteit en prestatiegraad.
