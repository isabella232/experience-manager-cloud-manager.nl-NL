---
title: Inzicht in de testresultaten
seo-title: Inzicht in de testresultaten
description: 'null'
seo-description: Volg deze pagina voor meer informatie over drie sneltoetsen tijdens het uitvoeren van een pijplijn, het scannen van code, prestaties en beveiligingstests waarmee uw programma wordt gevalideerd in Cloud Manager.
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
translation-type: tm+mt
source-git-commit: 4edbbff4e519a1403c3140cc742def35f9516eff
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 2%

---


# Inzicht in de testresultaten {#understand-your-test-results}

Tijdens het proces van de **Pijpleiding** , wordt een aantal metriek gevangen en vergeleken bij of de Belangrijkste Indicatoren van Prestaties (KPIs) die door de bedrijfseigenaar worden bepaald, of normen die door de Beheerde Diensten van Adobe worden geplaatst.

Deze worden gerapporteerd met behulp van het drielagige gatingsysteem zoals gedefinieerd in deze sectie.

## Drievoudige Gates terwijl het runnen van een Pijpleiding  {#three-tier-gates-while-running-a-pipeline}

Er liggen drie poorten in de pijplijn:

* Codekwaliteit
* Prestatietesten
* Beveiligingstests

Voor elk van deze poorten is er een structuur met drie niveaus voor emissies die door de poort worden geïdentificeerd.

* **Kritiek** - Dit zijn kwesties die door de poort worden geïdentificeerd die een directe mislukking van de pijpleiding veroorzaken.
* **Belangrijk** - Dit zijn kwesties die door de poort worden geïdentificeerd die de pijpleiding ertoe brengen om een gepauzeerde staat in te gaan. Een plaatsingsmanager, projectmanager, of bedrijfseigenaar kunnen of de kwesties met voeten treden, waarin de pijpleiding te werk gaat, of zij kunnen de kwesties goedkeuren, in welk geval de pijpleiding met een mislukking stopt.
* **Info** - Dit zijn kwesties die door de poort worden geïdentificeerd en die uitsluitend ter informatie worden verstrekt en geen invloed hebben op de uitvoering van de pijpleiding.

>[!NOTE]
>
>In een slechts pijpleiding van de Kwaliteit van de Code, kunnen de Belangrijke mislukkingen in de het Testen van de Kwaliteit van de Code de Testende stap van de Code niet worden met voeten getreden aangezien de het testen van de Kwaliteit van de Code de laatste stap in de pijpleiding is.

## Testen van de codekwaliteit {#code-quality-testing}

Als deel van de pijpleiding wordt de broncode gescand om ervoor te zorgen dat de plaatsingen aan bepaalde kwaliteitscriteria voldoen. Momenteel wordt dit geïmplementeerd door een combinatie van SonarQube en inhoudspakketonderzoek met gebruik van OakPAL. Er zijn meer dan 100 regels die generieke Java-regels en AEM-specifieke regels combineren. In de volgende tabel wordt de classificatie voor testcriteria samengevat:

| Naam | Definitie | Categorie | Drempel voor fout |
|--- |--- |--- |--- |
| Beveiligingsbeoordeling | A = 0 Kwetsbaarheid <br/>B = ten minste 1 Kleine Kwetsbaarheid<br/> C = ten minste 1 Ernstige Kwetsbaarheid <br/>D = ten minste 1 Kritieke Kwetsbaarheid <br/>E = ten minste 1 Kwetsbaarheid | Kritiek | &lt; B |
| Betrouwbaarheidsbeoordeling | A = 0 Bug <br/>B = ten minste 1 kleine bug <br/>C = ten minste 1 groot probleem <br/>D = ten minste 1 kritisch probleem E = ten minste 1 blokkeerprobleem | Belangrijk | &lt; C |
| Onderhoudsverklaring | Uitstaande herstelkosten voor codegeuren zijn: <br/><ul><li>&lt;=5% van de tijd die al in de toepassing is ingegaan, is de rating A </li><li>tussen 6 en 10% is de rating een B </li><li>tussen 11 en 20% is de rating een C </li><li>tussen 21 en 50% is de rating een D</li><li>iets meer dan 50% is een E</li></ul> | Belangrijk | &lt; A |
| Dekking | Een combinatie van de dekking van de meetlijn en de toestand volgens deze formule: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>waarbij: CT = voorwaarden die ten minste één keer zijn geëvalueerd op &#39;true&#39; tijdens het uitvoeren van eenheidstests <br/>CF = voorwaarden die ten minste één keer zijn geëvalueerd op &#39;false&#39; tijdens het uitvoeren van eenheidstests <br/>LC = gedekte lijnen = lines_to_cover - uncoverlines <br/><br/> B = totaal aantal voorwaarden <br/>EL = totaal aantal uitvoerbare lijnen (lines_to_cover) | Belangrijk | &lt; 50% |
| Overgeslagen eenheidstests | Aantal overgeslagen eenheidstests. | Info | > 1 |
| Problemen openen | Algemene uitgiftypen - Vulnerabilities, Bugs en Codefragmenten | Info | > 1 |
| Gedupliceerde lijnen | Aantal lijnen betrokken bij gedupliceerde blokken. <br/>Een codeblok dat als gedupliceerd moet worden beschouwd: <br/><ul><li>**Niet-Java-projecten:**</li><li>Er moeten ten minste 100 opeenvolgende en gedupliceerde tokens zijn.</li><li>Deze tokens moeten ten minste op: </li><li>30 regels code voor COBOL </li><li>20 coderegels voor ABAP </li><li>10 coderegels voor andere talen</li><li>**Java-projecten:**</li><li> Er moeten minstens tien opeenvolgende en gedupliceerde verklaringen zijn, ongeacht het aantal tokens en lijnen.</li></ul> <br/>Verschillen in inspringing en in letterlijke tekenreeksen worden genegeerd bij het detecteren van duplicaten. | Info | > 1% |
| Compatibiliteit met cloudservice | Aantal geïdentificeerde compatibiliteitsproblemen met de cloudservice. | Info | > 0 |


>[!NOTE]
>
>Zie [Metrische definities](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) voor meer gedetailleerde definities.

U kunt de lijst met regels hier downloaden [code-quality-rules.xlsx](/help/using/assets/CodeQuality-rules-latest.xlsx)

>[!NOTE]
>
>Voor meer informatie over de regels voor de kwaliteit van aangepaste code die worden uitgevoerd door [!UICONTROL Cloud Manager], raadpleegt u [Aangepaste regels](custom-code-quality-rules.md)voor codekwaliteit.

### Werken met valse positieven {#dealing-with-false-positives}

Het kwaliteitscontroleproces is niet perfect en zal soms ten onrechte problemen identificeren die eigenlijk niet problematisch zijn. Dit wordt een &quot;vals-positief&quot; genoemd.

In deze gevallen kan de broncode worden geannoteerd met de standaard-Java- `@SuppressWarnings` annotatie die de regel-id opgeeft als het annotatiekenmerk. Een veelvoorkomend probleem is bijvoorbeeld dat de SonarQube-regel voor het detecteren van gecodeerde wachtwoorden agressief kan zijn ten aanzien van de manier waarop een gecodeerd wachtwoord wordt geïdentificeerd.

Om naar een specifiek voorbeeld te kijken, zou deze code vrij gemeenschappelijk in een project zijn AEM dat code heeft om met één of andere externe dienst te verbinden:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube verhoogt vervolgens de kwetsbaarheid van de blokker. Na het herzien van de code, identificeert u dat dit geen kwetsbaarheid is en kan dit met aangewezen regel identiteitskaart annoteren

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Maar als de code eigenlijk dit was:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Dan is de correcte oplossing het hardcoded wachtwoord te verwijderen.

>[!NOTE]
>
>Het is weliswaar aan te raden de `@SuppressWarnings` annotatie zo specifiek mogelijk te maken, d.w.z. alleen de specifieke instructie of het specifieke blok dat de uitgave veroorzaakt, aan te brengen, maar het is wel mogelijk om een annotatie op klasseniveau te maken.

## Beveiligingstests {#security-testing}

[!UICONTROL Cloud Manager] stelt de bestaande Controle ****** van de Gezondheid van de Veiligheid AEM op stadium na de plaatsing in werking en rapporteert de status door UI. De resultaten worden samengevoegd van alle AEM-instanties in de omgeving.

Als een van de **Instanties** meldt dat een bepaalde gezondheidscontrole is mislukt, mislukt het hele **milieu** die gezondheidscontrole. Net als bij het testen van de kwaliteit en prestaties van de code, worden deze gezondheidscontroles in categorieën ingedeeld en gerapporteerd met behulp van het drielagige gatingsysteem. Het enige verschil is dat er geen drempelwaarde is voor het testen van de veiligheid. Alle gezondheidscontroles worden gewoon goedgekeurd of gefaald.

In de volgende tabel worden de huidige controles weergegeven:

| **Naam** | **Implementatie van gezondheidscontrole** | **Categorie** |
|---|---|---|
| Gereedheid van API voor aansluiting op een virtualisatiefirewall is acceptabel | Gereedheid van de firewall voor deserialisatie bevestigen-API | Kritiek |
| De firewall voor deserialization werkt goed | Functionele firewall voor deserialization | Kritiek |
| De firewall voor deserialization wordt geladen | Firewall voor deserialisatie geladen | Kritiek |
| AuthorizableNodeName de implementatie stelt toegelaten identiteitskaart in de knoopnaam/de weg niet bloot. | Authorizable Node Name Generation | Kritiek |
| Standaardwachtwoorden zijn gewijzigd | Standaardaanmeldingsaccounts | Kritiek |
| De verkoop standaard krijgt servlet wordt beschermd tegen DOS aanvallen. | Sling Get Servlet | Kritiek |
| De Sling Java Script Handler is op de juiste wijze geconfigureerd | JavaScript-handler afspelen | Kritiek |
| De Sling JSP Scripthandler is op de juiste wijze geconfigureerd | JSP-scripthandler afspelen | Kritiek |
| SSL is correct geconfigureerd | SSL-configuratie | Kritiek |
| Geen duidelijk onveilig beleid voor gebruikersprofielen gevonden | Standaardtoegang gebruikersprofiel | Kritiek |
| Het filter van de Verschuiver wordt gevormd om aanvallen te verhinderen CSRF | Filter Verschuivingsverwijzing | Belangrijk |
| Adobe Granite HTML Library Manager is op de juiste wijze geconfigureerd | Config. HTML-bibliotheekbeheer CQ | Belangrijk |
| CRXDE-ondersteuningsbundel is uitgeschakeld | CRXDE-ondersteuning | Belangrijk |
| Sling DavEx-bundel en -servlet zijn uitgeschakeld | DavEx Health Check | Belangrijk |
| Voorbeeldinhoud is niet geïnstalleerd | Voorbeelden van inhoudspakketten | Belangrijk |
| Zowel het WCM-aanvraagfilter als het WCM-foutopsporingsfilter zijn uitgeschakeld | Configuratie WCM-filters | Belangrijk |
| De verkoop WebDAV bundel en servlet worden gevormd geschikt | WebDAV Health Check | Belangrijk |
| De webserver is geconfigureerd om te voorkomen dat er wordt geklikt | Webserverconfiguratie | Belangrijk |
| Replicatie maakt geen gebruik van de gebruiker &#39;admin&#39; | Replicatie- en transportgebruikers | Info |

## Prestatietesten {#performance-testing}

*De prestatietests* in [!UICONTROL Cloud Manager] worden uitgevoerd met een test van 30 minuten.

Tijdens pijpleidingsopstelling, kan de plaatsingsmanager beslissen hoeveel verkeer aan elk emmertje te leiden.

U kunt meer over bandcontroles leren, van [Vorm uw CI/CD Pijpleiding](configuring-pipeline.md).

>[!NOTE]
>
>Om uw programma te opstelling en uw KPIs te bepalen, zie [Opstelling uw Programma](setting-up-program.md).

In de volgende tabel wordt een overzicht gegeven van de prestatietestmatrix met behulp van het drielagige gatingsysteem:

| **Metrisch** | **Categorie** | **Drempel voor fout** |
|---|---|---|
| Foutpercentage voor paginaverzoek % | Kritiek | >= 2% |
| CPU-gebruikssnelheid | Kritiek | >= 80% |
| Wachttijd schijf-IO | Kritiek | >= 50% |
| 95 Percentage van de responstijd | Belangrijk | >= KPI op programmaniveau |
| Piekresponstijd | Belangrijk | >= 18 seconden |
| Paginaweergaven per minuut | Belangrijk | &lt; KPI op programmaniveau |
| Gebruik van schijfbandbreedte | Belangrijk | >= 90% |
| Netwerkbandbreedtegebruik | Belangrijk | >= 90% |
| Aanvragen per minuut | Info | &lt; 6000 |

### Resultaten van het testen van prestaties Grafieken {#performance-testing-results-graphs}

Er zijn nieuwe grafieken en downloadopties toegevoegd aan het dialoogvenster Prestatietestresultaten.

Wanneer u het dialoogvenster Prestatietest opent, kunnen de metrische deelvensters worden uitgevouwen om een grafiek weer te geven, een koppeling naar een download of beide weer te geven.

Voor [!UICONTROL Cloud Manager] versie 2018.7.0 is deze functionaliteit beschikbaar voor de volgende metriek:

* **CPU-gebruik**
   * Een grafiek van het gebruik van cpu tijdens de testperiode.

* **I/O-wachttijd schijf**
   * Een grafiek van schijf I/O wacht Tijd tijdens de testperiode.

* **Paginafoutenfrequentie**
   * Een grafiek van paginafouten per minuut tijdens de testperiode.
   * Een CSV-bestandenlijst met pagina&#39;s die tijdens de test een fout hebben veroorzaakt.

* **Gebruik van schijfbandbreedte**
   * Een grafiek van het gebruik van de Bandbreedte van de Schijf tijdens de testperiode.

* **Netwerkbandbreedtegebruik**
   * Een grafiek van het Gebruik van de Bandbreedte van het Netwerk tijdens de testperiode.

* **Piekresponstijd**
   * Een grafiek van de piekresponstijd per minuut tijdens de testperiode.

* **95e responstijd met percentage**
   * Een grafiek van de responstijd van 95e percentiel per minuut tijdens de testperiode.
   * Een CSV-bestand met pagina&#39;s met een responstijd van 95% die de gedefinieerde KPI overschrijdt.

In de volgende afbeeldingen worden de prestatietestgrafieken weergegeven:

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

