---
title: Opmerkingen bij de release 2021.2.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2021.2.0
description: Volg deze pagina om informatie op te halen voor Cloud Manager Release 2021.2.0
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2021.2.0
translation-type: tm+mt
source-git-commit: d956c7a2d3833e357920a9602e4f5a5b37f2c98a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2021.2.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2021.2.0 beschreven.

## Releasedatum {#release-date}

De datum van de Versie voor [!UICONTROL Cloud Manager] Versie 2021.2.0 is 11 Februari, 2021.

## Wat is er nieuw?{#whats-new}

* Het AEM Project Archetype dat in Project en Sandbox creatie wordt gebruikt is bijgewerkt aan versie 25.

* De lijst met afgekeurde API&#39;s die tijdens het scannen van code zijn geïdentificeerd, is verfijnd en bevat nu extra klassen en methoden die zijn afgekeurd in de meest recente Cloud Service SDK-releases.

* Productie-implementaties worden nu parallel geïmplementeerd in de gepaarde publicatie- en verzendingsinstanties.

* SonarQube-profiel voor Cloud Manager bijgewerkt om Sonar-regel `squid:S2142` te verwijderen. Dit zal niet meer met de controles van de draadonderbreking in conflict brengen.

* Eigenschappen die zijn ingesteld in `pom.xml`-bestanden van de klant die vooraf zijn voorzien van sonar, worden nu dynamisch verwijderd om fouten met het scannen van build en kwaliteit te voorkomen.

* Er zijn aanvullende regels voor de kwaliteit van code toegevoegd om compatibiliteitsproblemen met Cloud Servicen te verhelpen.

## Opgeloste problemen {#bug-fixes}

* De CI/CD (plaatsing) pijpleiding mislukte tijdens een prestatieteststap toe te schrijven aan een container die de ladingstest in werking stelt die een fout ontmoette.

* Soms kan de laadtestcontainer de run als mislukt rapporteren, zelfs als er slechts één uitzondering optreedt. De fout wordt alleen gemeld als het testproces niet kan worden hersteld.

* Bepaalde problemen met trapsgewijze gegevens tussen de manier waarop de omgevingsnamen werden opgeslagen, zouden leiden tot fouten bij het testen van de prestaties.

* Sommige pijpleidingsmislukkingen werden verkeerd gemeld als pijpleidingsfouten.