---
title: Inzicht in de testresultaten
seo-title: Inzicht in de testresultaten
description: Meer informatie over drie sneltoetsen tijdens het uitvoeren van een pijplijn in Cloud Manager
seo-description: Volg deze pagina voor meer informatie over drie sneltoetsen tijdens het uitvoeren van een pijplijn, het scannen van code, prestaties en beveiligingstests waarmee uw programma wordt gevalideerd in Cloud Manager.
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
feature: CI-CD Pipeline, testresultaten
translation-type: tm+mt
source-git-commit: 12a7d6199983e2d19ef401051f60e3f24bb6d4f8
workflow-type: tm+mt
source-wordcount: '2685'
ht-degree: 1%

---


# Inzicht in de testresultaten {#understand-your-test-results}

Tijdens de uitvoering van de pijpleiding, wordt een aantal metriek gevangen en vergeleken bij of de Belangrijkste Indicatoren van Prestaties (KPIs) die door de bedrijfseigenaar worden bepaald, of normen die door de Beheerde Diensten van Adobe worden geplaatst.

Deze worden gerapporteerd met behulp van het drielagige gatingsysteem zoals gedefinieerd in deze sectie.

## Drievoudige poorten bij het uitvoeren van een pijplijn {#three-tier-gates-while-running-a-pipeline}

Er liggen drie poorten in de pijplijn:

* Codekwaliteit
* Prestatietesten
* Beveiligingstests

Voor elk van deze poorten is er een structuur met drie niveaus voor emissies die door de poort worden geïdentificeerd.

* **Kritiek**  - Dit zijn kwesties die door de poort worden geïdentificeerd die een directe mislukking van de pijpleiding veroorzaken.
* **Belangrijk**  - Dit zijn kwesties die door de poort worden geïdentificeerd die de pijpleiding veroorzaken om een gepauzeerde staat in te gaan. Een plaatsingsmanager, projectmanager, of bedrijfseigenaar kunnen of de kwesties met voeten treden, waarin de pijpleiding te werk gaat, of zij kunnen de kwesties goedkeuren, in welk geval de pijpleiding met een mislukking stopt.
* **Info**  - Dit zijn kwesties die door de poort worden geïdentificeerd en die uitsluitend ter informatie worden verstrekt en geen invloed hebben op de uitvoering van de pijpleiding.

>[!NOTE]
>
>In een slechts pijpleiding van de Kwaliteit van de Code, kunnen de Belangrijke mislukkingen in de het Testen van de Kwaliteit van de Code de Testende stap van de Code niet worden met voeten getreden aangezien de het testen van de Kwaliteit van de Code de laatste stap in de pijpleiding is.

## Testen van de kwaliteit van de code {#code-quality-testing}

Deze stap evalueert de kwaliteit van uw toepassingscode. Het is de kerndoelstelling van een code-Kwaliteit enige pijpleiding en wordt uitgevoerd onmiddellijk na de bouwstap in alle niet-productie en productiepijpleidingen. Raadpleeg [Uw CI-CD Pipeline](/help/using/configuring-pipeline.md) configureren voor meer informatie over verschillende soorten pijpleidingen.

### Testen van codekwaliteit {#understanding-code-quality-testing}

Bij het testen van de kwaliteit van de code, wordt de broncode gescand om ervoor te zorgen dat het aan bepaalde kwaliteitscriteria voldoet. Momenteel wordt dit geïmplementeerd door een combinatie van SonarQube, inhoudspakketonderzoek met behulp van OakPAL en validatie van verzenders met behulp van het Dispatcher Optimization Tool. Er zijn meer dan 100 regels die generieke Java-regels en AEM-specifieke regels combineren. Enkele AEM-specifieke regels worden gecreeerd gebaseerd op beste praktijken van AEM Techniek en worden bedoeld als [Regels van de Kwaliteit van de Code van de Douane](/help/using/custom-code-quality-rules.md).

>[!NOTE]
>U kunt de volledige lijst met regels [hier](/help/using/assets/CodeQuality-rules-AMS.xlsx) downloaden.

De resultaten van deze stap worden geleverd als *Classificatie*. De onderstaande tabel geeft een overzicht van de scores voor verschillende testcriteria:

| Naam | Definitie | Categorie | Drempel voor fout |
|--- |--- |--- |--- |
| Beveiligingsbeoordeling | A = 0 Kwetsbaarheid <br/>B = ten minste 1 Kleinere kwetsbaarheid<br/> C = ten minste 1 Ernstige kwetsbaarheid <br/>D = ten minste 1 Kritieke kwetsbaarheid <br/>E = ten minste 1 Blokkeerkwetsbaarheid | Kritiek | &lt; B |
| Betrouwbaarheidsbeoordeling | A = 0 Bug <br/>B = ten minste 1 kleine bug <br/>C = ten minste 1 groot probleem <br/>D = ten minste 1 kritisch probleem<br/>E = ten minste 1 blokkeerprobleem | Belangrijk | &lt; C |
| Onderhoudsverklaring | Uitstaande herstelkosten voor codegeuren zijn: <br/><ul><li>&lt;> </li><li>tussen 6 en 10% is de rating een B </li><li>tussen 11 en 20% is de rating een C </li><li>tussen 21 en 50% is de rating een D</li><li>iets meer dan 50% is een E</li></ul> | Belangrijk | &lt; A |
| Dekking | Een combinatie van de dekking van de meetlijn en de toestand volgens deze formule: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>waarbij: CT = voorwaarden die ten minste eenmaal zijn geëvalueerd op &#39;true&#39; bij het uitvoeren van eenheidstests <br/>CF = voorwaarden die ten minste eenmaal zijn geëvalueerd op &#39;false&#39; bij het uitvoeren van eenheidstests <br/>LC = gedekte lijnen = lines_to_cover - uncoverlines <br/><br/> B = totaal aantal voorwaarden <br/>EL = totaal aantal uitvoerbare lijnen (lines_to_cover) | Belangrijk | &lt; 50=&quot;&quot;> |
| Overgeslagen eenheidstests | Aantal overgeslagen eenheidstests. | Info | > 1 |
| Problemen openen | Algemene uitgiftypen - Vulnerabilities, Bugs en Codefragmenten | Info | > 0 |
| Gedupliceerde lijnen | Aantal lijnen betrokken bij gedupliceerde blokken. <br/>Een codeblok dat als gedupliceerd moet worden beschouwd:  <br/><ul><li>**Niet-Java-projecten:**</li><li>Er moeten ten minste 100 opeenvolgende en gedupliceerde tokens zijn.</li><li>Deze tokens moeten ten minste op: </li><li>30 regels code voor COBOL </li><li>20 coderegels voor ABAP </li><li>10 coderegels voor andere talen</li><li>**Java-projecten:**</li><li> Er moeten minstens tien opeenvolgende en gedupliceerde verklaringen zijn, ongeacht het aantal tokens en lijnen.</li></ul> <br/>Verschillen in inspringing en in letterlijke tekenreeksen worden genegeerd bij het detecteren van duplicaten. | Info | > 1% |
| Compatibiliteit met Cloud Service | Aantal geïdentificeerde kwesties van de Verenigbaarheid van de Cloud Service. | Info | > 0 |


>[!NOTE]
>
>Raadpleeg [Metrische definities](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) voor gedetailleerdere definities.

>[!NOTE]
>
>Als u meer wilt weten over de regels voor de kwaliteit van aangepaste code die worden uitgevoerd door [!UICONTROL Cloud Manager], raadpleegt u [Aangepaste regels voor de kwaliteit van code](custom-code-quality-rules.md).

### Omgaan met valse positieven {#dealing-with-false-positives}

Het kwaliteitscontroleproces is niet perfect en zal soms ten onrechte problemen identificeren die eigenlijk niet problematisch zijn. Dit wordt een &quot;vals-positief&quot; genoemd.

In deze gevallen kan de broncode worden geannoteerd met de standaard-Java `@SuppressWarnings`-annotatie die de regel-id opgeeft als het annotatiekenmerk. Een veelvoorkomend probleem is bijvoorbeeld dat de SonarQube-regel voor het detecteren van gecodeerde wachtwoorden agressief kan zijn ten aanzien van de manier waarop een gecodeerd wachtwoord wordt geïdentificeerd.

Om naar een specifiek voorbeeld te kijken, zou deze code vrij gemeenschappelijk in een AEM project zijn dat code heeft om met één of andere externe dienst te verbinden:

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
>Hoewel het aan te raden is om de `@SuppressWarnings`-annotatie zo specifiek mogelijk te maken, dat wil zeggen alleen de specifieke instructie of het specifieke blok dat de uitgave veroorzaakt, van annotatie te voorzien op klasseniveau.

## Beveiligingstests {#security-testing}

[!UICONTROL Cloud Manager] stelt het bestaande  ***AEM het stadium van de Controle van de*** Gezondheid van de Veiligheid na de plaatsing in werking en rapporteert de status door UI. De resultaten worden samengevoegd van alle AEM in de omgeving.

Deze zelfde Controles van de Gezondheid kunnen op elk ogenblik door de Console van het Web of het Dashboard van Verrichtingen worden uitgevoerd.

Als om het even welk **Instanties** een mislukking voor een bepaalde gezondheidscontrole melden, ontbreekt het volledige **Milieu** die gezondheidscontrole. Net als bij het testen van de kwaliteit en prestaties van de code, worden deze gezondheidscontroles in categorieën ingedeeld en gerapporteerd met behulp van het drielagige gatingsysteem. Het enige verschil is dat er geen drempelwaarde is voor het testen van de veiligheid. Alle gezondheidscontroles worden gewoon goedgekeurd of gefaald.

In de volgende tabel worden de huidige controles weergegeven:

| **Naam** | **Implementatie van gezondheidscontrole** | **Categorie** |
|---|---|---|
| Gereedheid van API voor aansluiting op een virtualisatiefirewall is acceptabel | [Gereedheid van de firewall voor deserialisatie bevestigen-API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | Kritiek |
| De firewall voor deserialization werkt goed | [Functionele firewall voor deserialization](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | Kritiek |
| De firewall voor deserialization wordt geladen | [Firewall voor deserialisatie geladen](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | Kritiek |
| AuthorizableNodeName de implementatie stelt toegelaten identiteitskaart in de knoopnaam/de weg niet bloot. | [Authorizable Node Name Generation](https://experienceleague.adobe.com/docs/experience-manager-64/administering/security/security-checklist.html?lang=en#security) | Kritiek |
| Standaardwachtwoorden zijn gewijzigd | [Standaardaanmeldingsaccounts](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=en#users-and-groups-in-aem) | Kritiek |
| Standaard GET-servlet wordt beveiligd tegen DOS-aanvallen. | Sling Get Servlet | Kritiek |
| De Sling Java Script Handler is op de juiste wijze geconfigureerd | JavaScript-handler afspelen | Kritiek |
| De Sling JSP Scripthandler is op de juiste wijze geconfigureerd | JSP-scripthandler afspelen | Kritiek |
| SSL is correct geconfigureerd | SSL-configuratie | Kritiek |
| Geen duidelijk onveilig beleid voor gebruikersprofielen gevonden | Standaardtoegang gebruikersprofiel | Kritiek |
| Het filter van de Verschuiver wordt gevormd om aanvallen te verhinderen CSRF | [Filter Verschuivingsverwijzing](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#security) | Belangrijk |
| De Adobe Granite HTML Library Manager is op de juiste wijze geconfigureerd | Config. HTML Library Manager | Belangrijk |
| CRXDE-ondersteuningsbundel is uitgeschakeld | CRXDE-ondersteuning | Belangrijk |
| Sling DavEx-bundel en -servlet zijn uitgeschakeld | DavEx Health Check | Belangrijk |
| Voorbeeldinhoud is niet geïnstalleerd | Voorbeelden van inhoudspakketten | Belangrijk |
| Zowel het WCM-aanvraagfilter als het WCM-foutopsporingsfilter zijn uitgeschakeld | [Configuratie WCM-filters](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=en#configuring) | Belangrijk |
| De verkoop WebDAV bundel en servlet worden gevormd geschikt | WebDAV Health Check | Belangrijk |
| De webserver is geconfigureerd om te voorkomen dat er wordt geklikt | Webserverconfiguratie | Belangrijk |
| Replicatie maakt geen gebruik van de gebruiker &#39;admin&#39; | Replicatie- en transportgebruikers | Info |

## Prestaties testen {#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager voert prestatietests voor AEM Sites-programma&#39;s uit. De prestatietest wordt uitgevoerd voor ongeveer 30 minuten door virtuele gebruikers (containers) te draaien die daadwerkelijke gebruikers simuleren om tot pagina&#39;s op het milieu van het Stadium toegang te hebben en verkeer te simuleren. Deze pagina&#39;s worden gevonden gebruikend een kruipper.

1. **Virtuele gebruikers**

   Het aantal virtuele gebruikers of containers dat door de Manager van de Wolk wordt gesponnen wordt gedreven door KPI (reactietijd en pagina&#39;s/min) die door de gebruiker in de rol Bedrijfs van de Eigenaar wordt bepaald terwijl [creërend of het uitgeven van het programma](setting-up-program.md). Op basis van gedefinieerde KPI&#39;s worden maximaal 10 containers gesponnen die werkelijke gebruikers simuleren. De pagina&#39;s die voor het testen zijn geselecteerd, worden gesplitst en toegewezen aan elke virtuele pagina.

1. **Crawler**

   Vóór het begin van de testperiode van 30 minuten, zal de Manager van de Wolk de milieu van het Stadium kruipen gebruikend een reeks van één of meerdere zaadURLs die door de Ingenieur van het Succes van de Klant wordt gevormd. Vanaf deze URL&#39;s wordt de HTML van elke pagina gecontroleerd en worden koppelingen doorlopen op een wijze die begint met het doorlopen van de breedte. Dit schuifproces is beperkt tot maximaal 5000 pagina&#39;s. De verzoeken van de kruipper hebben een vaste onderbreking van 10 seconden.

1. **Paginasets voor testen**

   Pagina&#39;s worden geselecteerd door drie paginasets. Cloud Manager gebruikt de toegangslogboeken van de AEM instanties over Productie en Stadium om de volgende drie emmers te bepalen:

   * *Populaire actieve pagina&#39;s*: Deze optie is geselecteerd om ervoor te zorgen dat de populairste pagina&#39;s die door live klanten worden benaderd, worden getest. Cloud Manager leest het toegangslogboek en bepaalt de 25 meest benaderde pagina&#39;s van live klanten om een lijst met top `Popular Live Pages` te genereren. Het snijpunt hiervan dat ook aanwezig is in het werkgebied wordt vervolgens gekropen in de Stage-omgeving.

   * *Andere actieve pagina&#39;s*: Deze optie is geselecteerd om te controleren of de pagina&#39;s die buiten de bovenste 25 populaire live pagina&#39;s vallen die misschien niet populair zijn, maar die wel belangrijk zijn om te testen, worden getest. Net als bij populaire live pagina&#39;s worden deze opgehaald uit het toegangslogboek en moeten deze ook aanwezig zijn in het werkgebied.

   * *Nieuwe pagina&#39;s*: Deze optie is geselecteerd om nieuwe pagina&#39;s te testen die mogelijk alleen in het werkgebied zijn geïmplementeerd en nog niet in productie zijn, maar die moeten worden getest.

      **Verdeling van verkeer over geselecteerde paginasets**

      U kunt overal van één tot alle drie reeksen in het &quot;Testen&quot;lusje van uw pijpleidingsconfiguratie (de verbinding van het Tussenvoegsel) kiezen. De verdeling van verkeer is gebaseerd op het aantal geselecteerde reeksen, dat wil zeggen, als alle drie worden geselecteerd, 33% van de totale paginameningen in de richting van elke reeks wordt gezet; als er twee zijn geselecteerd, gaat 50% naar elke set; als er één wordt geselecteerd , gaat 100 % van het verkeer naar die set .

      Stel bijvoorbeeld dat er een splitsing is van 50% tot 50% tussen de set Actieve pagina&#39;s populair en Nieuwe pagina&#39;s (in dit voorbeeld wordt Andere actieve pagina&#39;s niet gebruikt) en dat de set Nieuwe pagina&#39;s 3000 pagina&#39;s bevat. De paginaweergaven per minuut KPI is ingesteld op 200. Gedurende de testperiode van 30 minuten:

      * Elk van de 25 pagina&#39;s in de Populaire live paginaset wordt 120 keer - (200 * 0,5) / 25) * 30 = 120

      * Elk van de 3000 pagina&#39;s in de set Nieuwe pagina&#39;s wordt één keer geraakt - (200 * 0,5) / 3000) * 30 = 1

#### {#testing-reporting} testen en rapporteren

Cloud Manager voert de prestatie-tests voor AEM Sites-programma&#39;s uit door pagina&#39;s (als een niet-geverifieerde gebruiker standaard) op de publicatieserver van het werkgebied aan te vragen voor een testperiode van 30 minuten en de (virtuele) door de gebruiker gegenereerde meetgegevens te meten (responstijd, foutfrequentie, weergaven per minuut, enz.) voor elke pagina en voor alle instanties op systeemniveau (CPU, geheugen, netwerkgegevens).\
De volgende tabel geeft een overzicht van de meetgegevens van de prestatietest ten opzichte van het gebruik van het drielagige gatingsysteem:

In de volgende tabel wordt een overzicht gegeven van de prestatietestmatrix met behulp van het drielagige gatingsysteem:

| **Metrisch** | **Categorie** | **Drempel voor fout** |
|---|---|---|
| Foutpercentage voor paginaverzoek % | Kritiek | >= 2% |
| CPU-gebruikssnelheid | Kritiek | >= 80% |
| Wachttijd schijf-IO | Kritiek | >= 50% |
| 95 Percentage van de responstijd | Belangrijk | >= KPI op programmaniveau |
| Piekresponstijd | Belangrijk | >= 18 seconden |
| Paginaweergaven per minuut | Belangrijk | &lt; Program-level=&quot;&quot; KPI=&quot;&quot;> |
| Gebruik van schijfbandbreedte | Belangrijk | >= 90% |
| Netwerkbandbreedtegebruik | Belangrijk | >= 90% |
| Aanvragen per minuut | Info | >= 6000 |

Raadpleeg de onderstaande sectie **Authenticated Performance Testing** voor meer informatie over het gebruik van basisverificatie voor het testen van prestaties voor sites en middelen.

>[!NOTE]
>Elk exemplaar wordt gecontroleerd tijdens de periode van de test, voor zowel Publish als Auteur. Als om het even welke metrisch voor zelfs één instantie niet wordt verkregen, wordt die metrisch gemeld als onbekend en de overeenkomstige stap zal ontbreken.

#### Voor authentiek verklaarde Prestaties het Testen {#authenticated-performance-testing}

Deze functie is Sites optioneel.
AMS-klanten met geverifieerde sites kunnen een gebruikersnaam en wachtwoord opgeven die door Cloud Manager worden gebruikt voor toegang tot de website tijdens het testen van de Sites-prestaties.
De gebruikersnaam en het wachtwoord worden gespecificeerd als Variabelen van de Pijpleiding met de namen `CM_PERF_TEST_BASIC_USERNAME` en `CM_PERF_TEST_BASIC_PASSWORD`.
Hoewel niet strikt vereist, wordt het geadviseerd om het type van koordvariabele voor de gebruikersbenaming en het geheimString veranderlijke type voor het wachtwoord te gebruiken. Als beide van deze worden gespecificeerd, zal elk verzoek van de kruipper van de prestatietest en de test virtuele gebruikers deze geloofsbrieven als Basisauthentificatie van HTTP bevatten.

Voer de volgende handelingen uit om deze variabelen in te stellen met de CLI van Cloud Manager:

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

Raadpleeg [Variabelen](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchPipelineVariables) voor meer informatie over het gebruik van de API.

### AEM Assets {#aem-assets}

Cloud Manager voert de prestatietests voor AEM Assets-programma&#39;s uit door elementen gedurende een testperiode van 30 minuten herhaaldelijk te uploaden.

1. **Voorschrift aan boord**

   Voor het testen van de prestaties van middelen zal uw Klantsuccesingenieur `cloudmanager` gebruiker (en wachtwoord) tijdens het instappen van de Auteur aan het milieu van het Stadium creëren. Voor het testen van de prestaties is de gebruiker `cloudmanager` nodig en het bijbehorende wachtwoord dat door de CSE is ingesteld. Deze mag niet uit de Auteur worden verwijderd en mag niet worden gewijzigd in machtigingen. Dit zal waarschijnlijk mislukken bij het testen van de middelenprestaties.

1. **Afbeeldingen en middelen voor tests**

   Klanten kunnen hun eigen middelen uploaden om te testen. Dit kan van de Opstelling van de Pijpleiding of het Edit scherm worden gedaan. Algemene afbeeldingsindelingen, zoals JPEG, PNG, GIF en BMP, worden ondersteund in combinatie met Photoshop-, Illustrator- en Postscript-bestanden. Als er echter geen afbeeldingen worden geüpload, gebruikt Cloud Manager een standaardafbeelding en PDF-document voor het testen.

1. **Distributie van activa voor tests**

   De verdeling van hoeveel activa van elk type per minuut worden geupload wordt geplaatst in de Opstelling of geeft het scherm van de Pijpleiding uit.
Als bijvoorbeeld een splitsing van 70/30 wordt gebruikt, zoals in de onderstaande afbeelding wordt getoond. Er worden 10 elementen per minuut geüpload, 7 afbeeldingen worden per minuut geüpload en 3 documenten.

1. **Testen en rapporteren**

   Cloud Manager maakt een map op de instantie Auteur met behulp van de gebruikersnaam en het wachtwoord die door de CSE zijn ingesteld in stap #1 (Vereisten voor instapweigering), zoals hierboven vermeld, en uploadt elementen in de map met behulp van een bibliotheek die open source is. De tests die door de het testen van Activa worden in werking gesteld worden geschreven gebruikend deze [open bronbibliotheek](https://github.com/adobe/toughday2). Zowel de verwerkingstijd voor elk element als de verschillende metingen op systeemniveau worden over de testduur van 30 minuten gemeten. Met deze functie kunt u zowel afbeeldingen als PDF-documenten uploaden.

   >[!NOTE]
   >U kunt meer leren over het vormen van prestaties het testen, van [vorm uw CI/CD Pijpleiding](configuring-pipeline.md). Verwijs naar [Opstelling uw Programma](setting-up-program.md) om te leren hoe te om uw programma te installeren en uw KPIs te bepalen.

### Resultaten van het testen van prestaties Grafieken {#performance-testing-results-graphs}

Er zijn nieuwe grafieken en downloadopties toegevoegd aan het dialoogvenster Prestatietestresultaten.

Wanneer u het dialoogvenster Prestatietest opent, kunnen de metrische deelvensters worden uitgevouwen om een grafiek weer te geven, een koppeling naar een download of beide weer te geven.

Voor [!UICONTROL Cloud Manager] Release 2018.7.0 is deze functionaliteit beschikbaar voor de volgende metriek:

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

