---
title: Aangepaste regels voor codekwaliteit
seo-title: Aangepaste regels voor codekwaliteit
description: Volg deze pagina voor meer informatie over de regels voor de kwaliteit van aangepaste code die worden uitgevoerd door Cloud Manager.
seo-description: Volg deze pagina om meer te weten te komen over de aangepaste regels voor codekwaliteit die worden uitgevoerd door Adobe Experience Manager Cloud Manager.
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
translation-type: tm+mt
source-git-commit: cd6272bfd1ffdbf1802c30217e0c615392076109
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 5%

---


# Custom Code Quality Rules {#custom-code-quality-rules}

Op deze pagina worden de kwaliteitsregels voor aangepaste code beschreven die worden uitgevoerd door Cloud Manager en die zijn gemaakt op basis van de beste werkwijzen van AEM Engineering.

>[!NOTE]
>
>De hier opgegeven codevoorbeelden dienen slechts ter illustratie.

## SonarQube-regels {#sonarqube-rules}

In de volgende sectie worden de SonarQube-regels gemarkeerd:

### Gebruik geen potentieel gevaarlijke functies {#do-not-use-potentially-dangerous-functions}

**Sleutel**: CQRules:CWE-676

**Type**: Kwetsbaarheid

**Ernst**: Majoor

**Sinds**: Versie 2018.4.0

De methoden ***Thread.stop()*** en ***Thread.interrupt()*** kunnen problemen veroorzaken die moeilijk te reproduceren zijn en in sommige gevallen beveiligingsproblemen veroorzaken. Het gebruik ervan moet zorgvuldig worden gecontroleerd en gevalideerd. Over het algemeen is het doorgeven van berichten een veiligere manier om vergelijkbare doelen te bereiken.

#### Niet-compatibele code {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Compatibele code {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### Gebruik geen opmaaktekenreeksen die extern kunnen worden beheerd {#do-not-use-format-strings-which-may-be-externally-controlled}

**Sleutel**: CQRules:CWE-134

**Type**: Kwetsbaarheid

**Ernst**: Majoor

**Sinds**: Versie 2018.4.0

Het gebruiken van een formaatkoord van een externe bron (zoals een verzoekparameter of user-generated inhoud) kan een toepassing aan ontkenning van de dienstaanvallen blootstellen. Er zijn omstandigheden waarin een indelingstekenreeks extern kan worden beheerd, maar alleen is toegestaan vanuit vertrouwde bronnen.

#### Niet-compatibele code {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP-aanvragen moeten altijd socket- en verbindingstime-outs hebben {#http-requests-should-always-have-socket-and-connect-timeouts}

**Sleutel**: CQRules:ConnectionTimeoutMechanism

**Type**: Bug

**Ernst**: Kritiek

**Sinds**: Versie 2018.6.0

Wanneer het uitvoeren van HTTP- verzoeken van binnen een toepassing AEM, is het kritiek om ervoor te zorgen dat juiste onderbrekingen worden gevormd om onnodige draadconsumptie te vermijden. Jammer genoeg, is het standaardgedrag van zowel de standaardHTTP Cliënt van Java (java.net.HttpUrlConnection) als de algemeen gebruikte cliënt van de Componenten van Apache HTTP aan nooit onderbreking, zodat moeten de onderbrekingen uitdrukkelijk worden geplaatst. Bovendien zouden deze onderbrekingen, als beste praktijken, niet meer dan 60 seconden moeten zijn.

#### Niet-compatibele code {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Compatibele code {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Product-API&#39;s die met @ProviderType zijn geannoteerd, mogen niet door klanten worden geïmplementeerd of uitgebreid {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**Sleutel**: CQBP-84, afhankelijkheden van CQBP-84

**Type**: Bug

**Ernst**: Kritiek

**Sinds**: Versie 2018.7.0

De AEM-API bevat Java-interfaces en -klassen die alleen door aangepaste code mogen worden gebruikt, maar niet geïmplementeerd. De interface *com.day.cq.wcm.api.Page* is bijvoorbeeld ontworpen om ***alleen door AEM*** te worden geïmplementeerd.

Wanneer nieuwe methoden aan deze interfaces worden toegevoegd, beïnvloeden deze aanvullende methoden geen bestaande code die deze interfaces gebruikt en daardoor wordt de toevoeging van nieuwe methoden aan deze interfaces beschouwd als compatibel met eerdere versies. Als echter door aangepaste code één van deze interfaces ***wordt geïmplementeerd***, heeft deze aangepaste code een risico voor compatibiliteit met eerdere versies voor de klant geïntroduceerd.

Interfaces (en klassen) die alleen bedoeld zijn om door AEM te worden geïmplementeerd, zijn voorzien van een annotatie met *org.osgi.annotation.versioning.ProviderType* (of, in sommige gevallen, een vergelijkbare oudere annotatie *Qute.bnd.annotation.ProviderType*). Deze regel identificeert de gevallen waarin een dergelijke interface wordt uitgevoerd (of een klasse wordt uitgebreid) door douanecode.

#### Niet-compatibele code {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver-objecten moeten altijd worden gesloten {#resourceresolver-objects-should-always-be-closed}

**Sleutel**: CQRules:CQBP-72

**Type**: Code Smell

**Ernst**: Majoor

**Sinds**: Versie 2018.4.0

ResourceResolver-objecten die zijn verkregen van de ResourceResolverFactory gebruiken systeembronnen. Hoewel er maatregelen op zijn plaats zijn om deze middelen terug te winnen wanneer een ResourceResolver niet meer in gebruik is, is het efficiënter om om het even welke geopende voorwerpen uitdrukkelijk te sluiten ResourceResolver door de close () methode te roepen.

Eén relatief gebruikelijke misvatting is dat ResourceResolver-objecten die zijn gemaakt met een bestaande JCR-sessie, niet expliciet moeten worden gesloten of dat de onderliggende JCR-sessie hierdoor wordt gesloten. Dit is niet het geval - ongeacht hoe een ResourceResolver wordt geopend, zou het moeten worden gesloten wanneer niet meer gebruikt. Aangezien ResourceResolver de Closeable interface uitvoert, is het ook mogelijk om de poging-met-middelen syntaxis te gebruiken in plaats van uitdrukkelijk het aanhalen van close().

#### Niet-compatibele code {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Compatibele code {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Gebruik geen Serlet-serverpaden naar elkaar om servlets te registreren {#do-not-use-sling-servlet-paths-to-register-servlets}

**Sleutel**: CQRules:CQBP-75

**Type**: Code Smell

**Ernst**: Majoor

**Sinds**: Versie 2018.4.0

Zoals beschreven in de [verkoopdocumentatie](http://sling.apache.org/documentation/the-sling-engine/servlets.html), worden bindingen servlets door wegen ontmoedigd. Padgebonden servers kunnen geen standaard JCR-toegangsbesturingselementen gebruiken en vereisen daarom extra beveiligingsstrengheid. In plaats van het gebruiken van weg-gebonden servlets, wordt het geadviseerd om knopen in de bewaarplaats tot stand te brengen en servlets te registreren door middeltype.

#### Niet-compatibele code {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### De gevangen Uitzonderingen zouden moeten worden geregistreerd of worden geworpen, maar niet allebei {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Sleutel**: CQRules:CQBP-44—CatchAndOrLogOrThrow

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

In het algemeen, zou een uitzondering precies één keer moeten worden geregistreerd. Het registreren van uitzonderingen kan veelvoudige tijden verwarring veroorzaken aangezien het onduidelijk is hoe vaak een uitzondering voorkwam. Het meest gangbare patroon dat tot dit leidt is het registreren en het werpen van een gevangen uitzondering.

#### Niet-compatibele code {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Compatibele code {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Vermijd het hebben van een logboekverklaring onmiddellijk gevolgd door een throw verklaring {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Sleutel**: CQRules:CQBP-44—ConsecutivelyLogAndThrow

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

Een ander gemeenschappelijk patroon te vermijden is een bericht te registreren en dan onmiddellijk een uitzondering te werpen. Dit geeft doorgaans aan dat het uitzonderingsbericht uiteindelijk wordt gedupliceerd in logbestanden.

#### Niet-compatibele code {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Compatibele code {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Meld u niet aan bij INFO bij het verwerken van GET- of HEAD-verzoeken {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Sleutel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Type**: Code Smell

**Ernst**: Klein

In het algemeen, zou het INFO logboekniveau moeten worden gebruikt om belangrijke acties te afbakenen en, door gebrek, wordt AEM gevormd om bij het INFO niveau of boven te registreren. GET en HEAD mogen nooit alleen-lezen-operaties zijn en vormen dus geen belangrijke acties. Het registreren op het niveau INFO in antwoord op GET of HEAD verzoeken zal waarschijnlijk tot significante logboeklawaai leiden daardoor het moeilijker maken om nuttige informatie in logboekdossiers te identificeren. Het registreren wanneer het behandelen van KRIJGT of HEAD verzoeken zou of op de WARN of FOUTniveaus moeten zijn wanneer iets verkeerd is gegaan of op de DEBUG of niveaus van het SPOOR als de diepere het oplossen van problemeninformatie nuttig zou zijn.

>[!CAUTION]
>
>Dit is niet op access.log-type registreren voor elke verzoeken van toepassing.

#### Niet-compatibele code {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Compatibele code {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Gebruik Exception.getMessage() niet als de eerste parameter van een logboekinstructie {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**Sleutel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

Als beste praktijken, zouden de logboekberichten contextuele informatie over moeten verstrekken waar in de toepassing een uitzondering is voorgekomen. Hoewel de context ook door het gebruik van stapelsporen kan worden bepaald, over het algemeen zal het logboekbericht gemakkelijker zijn te lezen en te begrijpen. Dientengevolge, wanneer het registreren van een uitzondering, is het een slechte praktijk om het bericht van de uitzondering als logboekbericht te gebruiken - het uitzonderingsbericht zal bevatten wat verkeerd ging terwijl het logboekbericht zou moeten worden gebruikt om een logboeklezer te vertellen wat de toepassing deed toen de uitzondering gebeurde. Het uitzonderingsbericht zal nog worden geregistreerd; door uw eigen bericht te specificeren zullen de logboeken eenvoudig te begrijpen zijn.

#### Niet-compatibele code {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Compatibele code {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Aanmelden van vangstblokken moet zich op het WARN- of FOUTniveau bevinden {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Sleutel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

Zoals de naam al aangeeft, moeten Java-uitzonderingen altijd in *uitzonderlijke* omstandigheden worden gebruikt. Dientengevolge, wanneer een uitzondering wordt gevangen, is het belangrijk om ervoor te zorgen dat de logboekberichten op het aangewezen niveau - of WARN of FOUT worden geregistreerd. Dit zorgt ervoor dat die berichten correct in de logboeken verschijnen.

#### Niet-compatibele code {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Compatibele code {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Stapelsporen niet naar de console afdrukken {#do-not-print-stack-traces-to-the-console}

**Sleutel**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

Zoals vermeld, is de context kritiek wanneer het begrip van logboekberichten. Wanneer u Exception.printStackTrace() gebruikt, wordt **alleen** de stacktracering uitgevoerd naar de standaardfoutenstream, waardoor alle context verloren gaat. Bovendien kunnen in een toepassing met meerdere threads, zoals AEM, als meerdere uitzonderingen parallel met deze methode worden afgedrukt, de stacksporen elkaar overlappen, wat tot aanzienlijke verwarring leidt. De uitzonderingen zouden door het registrerenkader slechts moeten worden geregistreerd.

#### Niet-compatibele code {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Compatibele code {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Niet uitvoeren naar standaardinvoer of standaardfout {#do-not-output-to-standard-output-or-standard-error}

**Sleutel**: CQRules:CQBP-44—LogLevelConsolePrinters

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

Het registreren in AEM zou altijd door het registrerenkader (SLF4J) moeten worden gedaan. De uitvoer rechtstreeks naar de standaardoutput of de standaardfoutenstromen verliest de structurele en contextafhankelijke informatie die door het registrerenkader wordt verstrekt en kan, in sommige gevallen, prestatieskwesties veroorzaken.

#### Niet-compatibele code {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Compatibele code {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Hardcoded /apps en /libs paden vermijden {#avoid-hardcoded-apps-and-libs-paths}

**Sleutel**: CQRules:CQBP-71

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2018.4.0

In het algemeen moeten paden die beginnen met /libs en /apps niet worden gecodeerd omdat de paden waarnaar ze verwijzen het meest worden opgeslagen als paden ten opzichte van het zoekpad Sling (dat standaard is ingesteld op /libs/apps). Het gebruik van het absolute pad kan leiden tot subtiele defecten die pas later in de levenscyclus van het project verschijnen.

#### Niet-compatibele code {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Compatibele code {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Verkoopplanner mag niet worden gebruikt {#sonarqube-sling-scheduler}

**Sleutel**: CQRules:AMSCORE-554

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

De Planner van de Verkoop moet niet voor taken worden gebruikt die een gewaarborgde uitvoering vereisen. Het verkopen van Geplande Banen garandeert uitvoering en beter geschikt voor zowel gegroepeerde als niet-gegroepeerde milieu&#39;s.

Raadpleeg [Apache Sling Event en Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) voor meer informatie over de manier waarop saldertaken worden verwerkt in een geclusterde omgeving.

### Vervangen API&#39;s van AEM mogen niet worden gebruikt {#sonarqube-aem-deprecated}

**Sleutel**: AMSCORE-553

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

Het AEM API-oppervlak wordt voortdurend herzien om te bepalen voor welke API&#39;s het gebruik wordt ontmoedigd en dus als afgekeurd wordt beschouwd.

In veel gevallen worden deze API&#39;s vervangen door de standaard Java *@Deprecated* -annotatie en, als zodanig, zoals bepaald door `squid:CallToDeprecatedMethod`.

Er zijn echter gevallen waarin een API afgekeurd is in de context van AEM, maar in andere contexten niet mag worden afgekeurd. Deze regel identificeert deze tweede klasse.

## Regels voor OakPAL-inhoud {#oakpal-rules}

U vindt hieronder de OakPAL-controles die zijn uitgevoerd door Cloud Manager.

>[!NOTE]
>OakPAL is een framework dat is ontwikkeld door een AEM-partner (en winnaar van 2019 AEM Rockstar North America) en dat inhoudspakketten valideert met behulp van een zelfstandige Oak-opslagplaats.

### Klantpakketten mogen geen knooppunten onder /libs maken of wijzigen {#oakpal-customer-package}

**Sleutel**: BannedPaths

**Type**: Bug

**Ernst**: Blocker

**Sinds**: Versie 2019.6.0

Het is al lang een goede praktijk dat de /libs inhoudsboom in de AEM inhoudsbewaarplaats als read-only door klanten zou moeten worden beschouwd. Als knooppunten en eigenschappen onder */libs* worden gewijzigd, ontstaat een aanzienlijk risico voor belangrijke en kleine updates. Wijzigingen in */bibliotheken* mogen alleen via officiële kanalen door Adobe worden aangebracht.

### Pakketten mogen geen dubbele OSGi-configuraties bevatten {#oakpal-package-osgi}

**Sleutel**: DuplicateOsgiConfigurations

**Type**: Bug

**Ernst**: Majoor

**Sinds**: Versie 2019.6.0

Een gemeenschappelijk probleem dat op complexe projecten voorkomt is waar de zelfde component OSGi veelvoudige tijden wordt gevormd. Dit leidt tot een dubbelzinnigheid over welke configuratie zal opereerbaar zijn. Deze regel is &quot;runmode-bewust&quot;in die zin dat het slechts kwesties zal identificeren waar de zelfde component veelvoudige tijden op de zelfde runmode (of combinatie runmodes) wordt gevormd.

#### Niet-conforme code {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Compatibele code {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Mappen configureren en installeren mag alleen OSGi-knooppunten bevatten {#oakpal-config-install}

**Sleutel**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Type**: Bug

**Ernst**: Majoor

**Sinds**: Versie 2019.6.0

Om veiligheidsredenen, zijn de wegen die */config/ en /install/* bevatten slechts leesbaar door administratieve gebruikers in AEM en zouden slechts voor configuratie OSGi en bundels moeten worden gebruikt OSGi. Als u andere typen inhoud onder paden plaatst die deze segmenten bevatten, resulteert dit in toepassingsgedrag dat per ongeluk verschilt tussen gebruikers met en zonder beheerdersrechten.

Een veelvoorkomend probleem is het gebruik van knooppunten die `config` in componentdialoogvensters worden genoemd of wanneer u de configuratie van de rich text editor opgeeft voor inlinebewerking. Om dit op te lossen zou de beledigende knoop aan een volgzame naam moeten worden anders genoemd. Voor de rijke configuratie van de tekstredacteur maak gebruik van het `configPath` bezit op de `cq:inplaceEditing` knoop om de nieuwe plaats te specificeren.

#### Niet-conforme code {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Compatibele code {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Pakketten mogen elkaar niet overlappen {#oakpal-no-overlap}

**Sleutel**: PackageOverlaps

**Type**: Bug

**Ernst**: Majoor

**Sinds**: Versie 2019.6.0

Gelijkaardig aan de *Pakketten zouden geen Dubbele OSGi Configuraties* moeten bevatten dit is een gemeenschappelijk probleem op complexe projecten waar de zelfde knoopweg aan door veelvoudige afzonderlijke inhoudspakketten wordt geschreven. Terwijl het gebruiken van inhoudspakketgebiedsdelen kan worden gebruikt om een verenigbaar resultaat te verzekeren, is het beter om overlappingen volledig te vermijden.

### Standaardontwerpmodus mag geen klassieke UI zijn {#oakpal-default-authoring}

**Sleutel**: ClassicUIAuthoringMode

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

De configuratie OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` bepaalt de standaard auteurswijze binnen AEM. Aangezien Klassieke UI sinds AEM 6.4 is afgekeurd, zal een kwestie nu worden opgeheven wanneer de standaard auteurswijze aan Klassieke UI wordt gevormd.

### Componenten met dialoogvensters moeten aanraakinterface-dialoogvensters hebben {#oakpal-components-dialogs}

**Sleutel**: ComponentWithOnlyClassicUIDialog

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

AEM-componenten die een Klassieke UI-dialoogvenster hebben, moeten altijd een corresponderend Touch UI-dialoogvenster hebben voor een optimale ontwerpervaring en compatibel zijn met het implementatiemodel van de Cloud Service, waarbij Klassieke UI niet wordt ondersteund. Deze regel verifieert de volgende scenario&#39;s:

* Een component met een klassieke UI-dialoogvenster (dat wil zeggen een onderliggende dialoognode) moet een overeenkomend dialoogvenster Touch UI hebben (dat wil zeggen een `cq:dialog` onderliggende node).
* Een component met een Klassieke UI-ontwerpdialoogvenster (d.w.z. een design_dialog-knooppunt) moet een overeenkomend dialoogvenster voor het aanraakinterface-ontwerp hebben (dat wil zeggen een `cq:design_dialog` onderliggende node).
* Een component met zowel een dialoogvenster voor klassieke gebruikersinterface als een dialoogvenster voor klassieke gebruikersinterface moet zowel een corresponderend dialoogvenster voor aanraakinterface als een overeenkomstig dialoogvenster voor aanraakgebruikersinterface hebben.

De documentatie van de Hulpmiddelen van de Modernisering AEM verstrekt documentatie en tooling voor hoe te om componenten van Klassieke UI in Aanraakinterface om te zetten. Raadpleeg [de moderniseringsinstrumenten](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) van AEM voor meer informatie.

### Pakketten mogen geen MIP-bestand en onveranderbare inhoud mengen {#oakpal-packages-immutable}

**Sleutel**: ImmutableMutableMixedPackage

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

Om compatibel te zijn met het implementatiemodel van de cloudservice, moeten afzonderlijke inhoudspakketten inhoud bevatten voor de onveranderlijke gebieden van de opslagplaats (dat wil zeggen, `/apps and /libs, although /libs` moeten ze niet worden gewijzigd door de code van de klant en veroorzaken ze een afzonderlijke schending) of het veranderbare gebied (dat wil zeggen alles anders), maar niet beide. Een pakket dat beide bevat, is bijvoorbeeld niet compatibel met Cloud Service en zorgt ervoor dat een probleem wordt gemeld. `/apps/myco/components/text and /etc/clientlibs/myco`

Raadpleeg de [AEM-projectstructuur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) voor meer informatie.

### Reverse Replication Agents mogen niet worden gebruikt {#oakpal-reverse-replication}

**Sleutel**: ReverseReplication

**Type**: Code Smell

**Ernst**: Klein

**Sinds**: Versie 2020.5.0

Ondersteuning voor omgekeerde replicatie is niet beschikbaar in implementaties van cloudservice, zoals beschreven in [Opmerkingen bij de release: Verwijderen van replicatieagents](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents).

Klanten die omgekeerde replicatie gebruiken, moeten contact opnemen met Adobe voor alternatieve oplossingen.





