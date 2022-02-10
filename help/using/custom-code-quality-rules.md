---
title: Aangepaste regels voor codekwaliteit
description: Op deze pagina worden de regels voor de kwaliteit van aangepaste code beschreven die door Cloud Manager worden uitgevoerd als onderdeel van het testen van de kwaliteit van de code. Zij zijn gebaseerd op beste praktijken van AEM Techniek.
uuid: a7feb465-1982-46be-9e57-e67b59849579
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
feature: Code Quality Rules
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 834508109e34eb1e052abac482e981735c72d43d
workflow-type: tm+mt
source-wordcount: '3611'
ht-degree: 3%

---


# Aangepaste regels voor codekwaliteit {#custom-code-quality-rules}

Op deze pagina worden de kwaliteitsregels voor aangepaste code beschreven die door Cloud Manager worden uitgevoerd als onderdeel van [testen van de codekwaliteit.](understand-your-test-results.md) Zij zijn gebaseerd op beste praktijken van AEM Techniek.

>[!NOTE]
>
>Raadpleeg voor meer informatie over de aangepaste kwaliteitsregels voor Cloud Manager in AEM as a Cloud Service [aan deze documentatie.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/custom-code-quality-rules.html#using-cloud-manager).

>[!NOTE]
>
>De hier gegeven codevoorbeelden zijn slechts voor illustratieve doeleinden. Zie [Documentatie bij Concepts van SonarQube](https://docs.sonarqube.org/7.4/user-guide/concepts/) kennis te nemen van zijn concepten en kwaliteitsregels.

## SonarQube-regels {#sonarqube-rules}

In de volgende sectie worden SonarQube-regels beschreven die door Cloud Manager worden uitgevoerd.

### Gebruik geen potentieel gevaarlijke functies {#do-not-use-potentially-dangerous-functions}

* **Sleutel**: CQRules:CWE-676
* **Type**: Kwetsbaarheid
* **Ernst**: Majoor
* **Sinds**: Versie 2018.4.0

De methoden `Thread.stop()` en `Thread.interrupt()` kan problemen veroorzaken die moeilijk te reproduceren zijn en, in sommige gevallen, veiligheidskwetsbaarheden. Het gebruik ervan moet zorgvuldig worden gecontroleerd en gevalideerd. Over het algemeen is het doorgeven van berichten een veiligere manier om vergelijkbare doelen te bereiken.

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

* **Sleutel**: CQRules:CWE-134
* **Type**: Kwetsbaarheid
* **Ernst**: Majoor
* **Sinds**: Versie 2018.4.0

Het gebruiken van een formaatkoord van een externe bron (zoals een verzoekparameter of user-generated inhoud) kan een toepassing aan ontkenning van de dienstaanvallen blootstellen. Er zijn omstandigheden waarin een indelingstekenreeks extern kan worden beheerd, maar alleen is toegestaan vanuit vertrouwde bronnen.

#### Niet-compatibele code {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP-aanvragen moeten altijd een Socket- en Connect-time-out hebben {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Sleutel**: CQRules:ConnectionTimeoutMechanism
* **Type**: Bug
* **Ernst**: Kritiek
* **Sinds**: Versie 2018.6.0

Wanneer het uitvoeren van HTTP- verzoeken van binnen een AEM toepassing, is het kritiek om ervoor te zorgen dat juiste onderbrekingen worden gevormd om onnodige draadconsumptie te vermijden. Jammer genoeg, het standaardgedrag van allebei de standaardHTTP- Cliënt van Java, `java.net.HttpUrlConnection`en de veelgebruikte client voor Apache HTTP Components moet nooit een time-out maken. Daarom moeten time-outs expliciet worden ingesteld. Als beste praktijken, zouden deze onderbrekingen niet meer dan 60 seconden moeten zijn.

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

### Objecten ResourceResolver moeten altijd worden gesloten {#resourceresolver-objects-should-always-be-closed}

* **Sleutel**: CQRules:CQBP-72
* **Type**: Code Smell
* **Ernst**: Majoor
* **Sinds**: Versie 2018.4.0

`ResourceResolver` objecten verkregen uit `ResourceResolverFactory` verbruikt systeembronnen. Hoewel er maatregelen bestaan om deze middelen terug te vorderen wanneer een `ResourceResolver` niet meer in gebruik is, is het efficiënter om geopende `ResourceResolver` objecten aanroepen `close()` methode.

Eén relatief gebruikelijke misvatting is dat `ResourceResolver` objecten die met een bestaande JCR-sessie zijn gemaakt, mogen niet expliciet worden gesloten of de onderliggende JCR-sessie wordt afgesloten. Dat is niet het geval. Ongeacht hoe een `ResourceResolver` wordt geopend, moet het worden gesloten wanneer het niet meer wordt gebruikt. Sinds `ResourceResolver` implementeert de `Closeable` -interface, is het ook mogelijk de `try-with-resources` syntaxis in plaats van expliciet aan te roepen `close()`.

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

### Servlet-paden niet gebruiken om Servlets te registreren {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Sleutel**: CQRules:CQBP-75
* **Type**: Code Smell
* **Ernst**: Majoor
* **Sinds**: Versie 2018.4.0

Zoals beschreven in het [Verkoopdocumentatie](http://sling.apache.org/documentation/the-sling-engine/servlets.html)bindingen van servlets via paden worden afgeraden. Padgebonden servers kunnen geen standaard JCR-toegangsbesturingselementen gebruiken en vereisen daarom extra beveiligingsstrengheid. In plaats van het gebruiken van weg-gebonden servlets, wordt het geadviseerd om knopen in de bewaarplaats tot stand te brengen en servlets te registreren door middeltype.

#### Niet-compatibele code {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Afgehandelde uitzonderingen moeten worden geregistreerd of gegenereerd, niet beide {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Sleutel**: CQRules:CQBP-44—CatchAndOrLogOrThrow
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

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

### Gebruik geen logboekinstructies die direct worden gevolgd door de instructies Throw {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Sleutel**: CQRules:CQBP-44—ConsecutivelyLogAndThrow
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

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

* **Sleutel**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Type**: Code Smell
* **Ernst**: Klein

In het algemeen, zou het INFO logboekniveau moeten worden gebruikt om belangrijke acties te afbakenen en, door gebrek, AEM wordt gevormd om bij het INFO niveau of boven te registreren. GET- en HEAD-methoden mogen nooit alleen-lezen zijn en vormen dus geen belangrijke acties. Het registreren op het niveau INFO in antwoord op GET of HEAD verzoeken zal waarschijnlijk tot significante logboeklawaai leiden daardoor het moeilijker maken om nuttige informatie in logboekdossiers te identificeren. Het registreren wanneer de behandeling van GET of HEAD- verzoeken of op de niveaus van de WAARSCHUWING of van de FOUT zou moeten zijn wanneer iets verkeerd is gegaan of op de niveaus DEBUG of van de TRACE als de diepere het oplossen van problemeninformatie nuttig zou zijn.

>[!NOTE]
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

### Gebruik Exception.getMessage() niet als de eerste parameter van een Logging-instructie {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Sleutel**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

Als beste praktijken, zouden de logboekberichten contextuele informatie over moeten verstrekken waar in de toepassing een uitzondering is voorgekomen. Hoewel de context ook door het gebruik van stapelsporen kan worden bepaald, over het algemeen zal het logboekbericht gemakkelijker zijn te lezen en te begrijpen. Dientengevolge, wanneer het registreren van een uitzondering, is het een slechte praktijk om het bericht van de uitzondering als logboekbericht te gebruiken. Het uitzonderingsbericht zal bevatten wat verkeerd ging terwijl het logboekbericht zou moeten worden gebruikt om een logboeklezer te vertellen wat de toepassing deed toen de uitzondering gebeurde. Het uitzonderingsbericht zal nog worden geregistreerd. Door uw eigen bericht te specificeren zullen de logboeken enkel gemakkelijker te begrijpen zijn.

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

### Aanmelden bij Vangstblokken moet plaatsvinden op het WAARSCHUWINGSniveau of FOUTniveau {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Sleutel**: CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

Zoals de naam al aangeeft, moeten Java-uitzonderingen altijd worden gebruikt in uitzonderlijke omstandigheden. Dientengevolge, wanneer een uitzondering wordt gevangen, is het belangrijk om ervoor te zorgen dat de logboekberichten op het aangewezen niveau worden geregistreerd: WAARSCHUWING of FOUT. Dit zorgt ervoor dat die berichten correct in de logboeken verschijnen.

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

* **Sleutel**: CQRules:CQBP-44—ExceptionPrintStackTrace
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

De context is kritiek wanneer het begrip van logboekberichten. Gebruiken `Exception.printStackTrace()` zorgt ervoor dat alleen de stacktracering wordt uitgevoerd naar de standaardfoutenstream, waardoor alle context verloren gaat. Bovendien kunnen in een multithread-toepassing, zoals AEM, meerdere uitzonderingen parallel met deze methode worden afgedrukt, de stacksporen ervan overlappen, wat tot grote verwarring leidt. De uitzonderingen zouden door het registrerenkader slechts moeten worden geregistreerd.

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

* **Sleutel**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

Het registreren in AEM zou altijd door het registrerenkader, SLF4J moeten worden gedaan. De uitvoer rechtstreeks naar de standaardoutput of de standaardfoutenstromen verliest de structurele en contextafhankelijke informatie die door het registrerenkader wordt verstrekt en kan, in sommige gevallen, prestatieskwesties veroorzaken.

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

* **Sleutel**: CQRules:CQBP-71
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2018.4.0

In het algemeen beginnen paden met `/libs` en `/apps` moeten niet worden gecodeerd omdat de paden waarnaar ze verwijzen het meest worden opgeslagen als paden ten opzichte van het zoekpad Schuivend (dat is ingesteld op `/libs,/apps` standaard). Het gebruik van het absolute pad kan leiden tot subtiele defecten die pas later in de levenscyclus van het project verschijnen.

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

* **Sleutel**: CQRules:AMSCORE-554
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

De Planner van de Verkoop moet niet voor taken worden gebruikt die een gewaarborgde uitvoering vereisen. Het verkopen van Geplande Banen garandeert uitvoering en beter geschikt voor zowel gegroepeerde als niet-gegroepeerde milieu&#39;s.

Zie [Apache Sling Event- en Job Handling-documentatie](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) om meer over te leren hoe het Verdelen van Banen in een gegroepeerde milieu&#39;s worden behandeld.

### Verouderde API&#39;s AEM niet mogen worden gebruikt {#sonarqube-aem-deprecated}

* **Sleutel**: AMSCORE-553
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

Het AEM API-oppervlak wordt voortdurend herzien om te bepalen voor welke API&#39;s het gebruik wordt ontmoedigd en dus als afgekeurd wordt beschouwd.

In veel gevallen worden deze API&#39;s vervangen door de standaard Java *@Deprecated* annotatie en, als zodanig, zoals geïdentificeerd door `squid:CallToDeprecatedMethod`.

Er zijn echter gevallen waarin een API afgekeurd is in de context van AEM, maar in andere contexten niet mag worden afgekeurd. Deze regel identificeert deze tweede klasse.

## Regels voor OakPAL-inhoud {#oakpal-rules}

In de volgende sectie worden de OakPAL-controles beschreven die door Cloud Manager zijn uitgevoerd.

>[!NOTE]
>
>OakPAL is een framework dat inhoudspakketten valideert met behulp van een zelfstandige Oak-opslagplaats. Het werd ontwikkeld door een AEM partner en winnaar van de prijs AEM Rockstar North America 2019.

### Product-API&#39;s die zijn voorzien van een annotatie met @ProviderType mogen niet worden geïmplementeerd of uitgebreid door klanten {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Sleutel**: CQBP-84
* **Type**: Bug
* **Ernst**: Kritiek
* **Sinds**: Versie 2018.7.0

De AEM-API bevat Java-interfaces en -klassen die alleen door aangepaste code mogen worden gebruikt, maar niet geïmplementeerd. De interface `com.day.cq.wcm.api.Page` is bijvoorbeeld ontworpen om alleen door AEM te worden geïmplementeerd.

Wanneer nieuwe methoden aan deze interfaces worden toegevoegd, beïnvloeden deze aanvullende methoden geen bestaande code die deze interfaces gebruikt en daardoor wordt de toevoeging van nieuwe methoden aan deze interfaces beschouwd als compatibel met eerdere versies. Als echter door aangepaste code één van deze interfaces wordt geïmplementeerd, heeft deze aangepaste code een risico voor compatibiliteit met eerdere versies voor de klant geïntroduceerd.

Interfaces en klassen die alleen door AEM moeten worden geïmplementeerd, zijn voorzien van een annotatie `org.osgi.annotation.versioning.ProviderType` of, in sommige gevallen, een gelijkaardige erfenisaantekening `aQute.bnd.annotation.ProviderType`. Deze regel identificeert de gevallen waarin een dergelijke interface wordt uitgevoerd of een klasse door douanecode wordt uitgebreid.

#### Niet-compatibele code {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Klantpakketten mogen geen knooppunten onder /libs maken of wijzigen {#oakpal-customer-package}

* **Sleutel**: BannedPath
* **Type**: Bug
* **Ernst**: Blocker
* **Sinds**: Versie 2019.6.0

Het is al lang een goede praktijk dat de `/libs` de inhoudsstructuur in de AEM-inhoudgegevensopslagruimte moet door klanten als alleen-lezen worden beschouwd. Knooppunten en eigenschappen wijzigen onder `/libs` brengt een aanzienlijk risico met zich mee voor belangrijke en kleine updates. Wijzigingen in `/libs` alleen door Adobe via officiële kanalen te doen.

### Pakketten mogen geen dubbele OSGi-configuraties bevatten {#oakpal-package-osgi}

* **Sleutel**: DuplicateOsgiConfigurations
* **Type**: Bug
* **Ernst**: Majoor
* **Sinds**: Versie 2019.6.0

Een gemeenschappelijk probleem dat op complexe projecten voorkomt is waar de zelfde component OSGi veelvoudige tijden wordt gevormd. Dit leidt tot een dubbelzinnigheid over welke configuratie zal opereerbaar zijn. Deze regel is &quot;runmode-bewust&quot;in die zin dat het slechts kwesties zal identificeren waar de zelfde component veelvoudige tijden op de zelfde runmode of combinatie runmodes wordt gevormd.

#### Niet-conforme code {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Compatibele code {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Mappen configureren en installeren mag alleen OSGi-knooppunten bevatten {#oakpal-config-install}

* **Sleutel**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Type**: Bug
* **Ernst**: Majoor
* **Sinds**: Versie 2019.6.0

Om veiligheidsredenen, paden die `/config/` en `/install/` alleen leesbaar zijn door administratieve gebruikers in AEM en alleen moeten worden gebruikt voor OSGi-configuratie en OSGi-bundels. Als u andere typen inhoud onder paden plaatst die deze segmenten bevatten, resulteert dit in toepassingsgedrag dat per ongeluk verschilt tussen gebruikers met en zonder beheerdersrechten.

Een veelvoorkomend probleem is het gebruik van knooppunten met de naam `config` binnen componentendialogen of wanneer het specificeren van de rijke configuratie van de tekstredacteur voor gealigneerde het uitgeven. Om dit op te lossen zou de beledigende knoop aan een volgzame naam moeten worden anders genoemd. Voor de rijke configuratie van de tekstredacteur gebruik maken van `configPath` eigenschap op de `cq:inplaceEditing` knooppunt om de nieuwe locatie op te geven.

#### Niet-conforme code {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Compatibele code {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Pakketten mogen elkaar niet overlappen {#oakpal-no-overlap}

* **Sleutel**: PackageOverlaps
* **Type**: Bug
* **Ernst**: Majoor
* **Sinds**: Versie 2019.6.0

Vergelijkbaar met de [De pakketten zouden geen dubbele OSGi configuratieregel moeten bevatten,](#oakpal-package-osgi)  dit is een gemeenschappelijk probleem bij complexe projecten waar de zelfde knoopweg aan door veelvoudige afzonderlijke inhoudspakketten wordt geschreven. Terwijl het gebruiken van inhoudspakketgebiedsdelen kan worden gebruikt om een verenigbaar resultaat te verzekeren, is het beter om overlappingen volledig te vermijden.

### Standaardontwerpmodus mag geen klassieke UI zijn {#oakpal-default-authoring}

* **Sleutel**: ClassicUIAuthoringMode
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

De OSGi-configuratie `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definieert de standaardontwerpmodus in AEM. Omdat [de klassieke gebruikersinterface sinds AEM 6.4 is afgekeurd,](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) een kwestie zal nu worden opgeheven wanneer de standaard auteurswijze aan Klassieke UI wordt gevormd.

### Componenten met dialoogvensters moeten aanraakinterface-dialoogvensters hebben {#oakpal-components-dialogs}

* **Sleutel**: ComponentWithOnlyClassicUIDialog
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

AEM Componenten die een Klassieke UI dialoog hebben zouden altijd een overeenkomstige dialoog van de Aanraking UI moeten hebben zowel om een optimale auteurservaring te verstrekken als met het de plaatsingsmodel van de Cloud Service compatibel te zijn, waar Klassieke UI niet wordt gesteund. Deze regel verifieert de volgende scenario&#39;s:

* Een component met een klassieke UI-dialoogvenster (een `dialog` onderliggende node) moet een corresponderend Touch UI-dialoogvenster hebben (dat wil zeggen een `cq:dialog` onderliggende node).
* Een component met een dialoogvenster voor het ontwerpen van een klassieke gebruikersinterface (d.w.z. een `design_dialog` knooppunt) moet een corresponderend dialoogvenster voor het ontwerpen van een aanraakinterface hebben (dat wil zeggen een `cq:design_dialog` onderliggende node).
* Een component met zowel een dialoogvenster voor klassieke gebruikersinterface als een dialoogvenster voor klassieke gebruikersinterface moet zowel een corresponderend dialoogvenster voor aanraakinterface als een overeenkomstig dialoogvenster voor aanraakgebruikersinterface hebben.

De documentatie van de Hulpmiddelen van de Modernisering van het AEM verstrekt details en tooling voor hoe te om componenten van Klassieke UI in Aanraakinterface om te zetten. Zie [De documentatie van de AEM Moderniseringshulpmiddelen ](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) voor meer informatie .

### Pakketten mogen geen MIP-bestand en onveranderbare inhoud mengen {#oakpal-packages-immutable}

* **Sleutel**: ImmutableMutableMixedPackage
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

Om compatibel te zijn met het implementatiemodel van de Cloud Service, moeten afzonderlijke inhoudspakketten ofwel inhoud bevatten voor de onveranderlijke gebieden van de opslagplaats (dat wil zeggen: `/apps` en `/libs`) of het veranderbare gebied (dat wil zeggen alles niet in `/apps` of `/libs`), maar niet beide. Bijvoorbeeld een pakket dat beide bevat `/apps/myco/components/text and /etc/clientlibs/myco` niet verenigbaar is met de Cloud Service en ertoe zal leiden dat een probleem wordt gerapporteerd.

Zie [AEM documentatie over de projectstructuur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) voor meer informatie .

>[!NOTE]
>
>De regel [Klantpakketten mogen geen knooppunten onder /libs maken of wijzigen](#oakpal-customer-package) altijd van toepassing.

### Reverse Replication Agents mogen niet worden gebruikt {#oakpal-reverse-replication}

* **Sleutel**: ReverseReplication
* **Type**: Compatibiliteit van code met Cloud Service/Smal
* **Ernst**: Klein
* **Sinds**: Versie 2020.5.0

Ondersteuning voor reverse-replicatie is niet beschikbaar in Cloud Service-implementaties, zoals beschreven in [Opmerkingen bij de release: Verwijderen van replicatieagents.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html#replication-agents)

De klanten die omgekeerde replicatie gebruiken zouden Adobe voor alternatieve oplossingen moeten contacteren.

### De middelen in volmacht-Toegelaten Bibliotheken van de Cliënt zouden in een Omslag moeten zijn genoemde middelen {#oakpal-resources-proxy}

* **Sleutel**: ClientlibProxyResource
* **Type**: Bug
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM clientbibliotheken kunnen statische bronnen bevatten, zoals afbeeldingen en lettertypen. Zoals beschreven in het [Gebruikend Cliënt-zij documentatie van Bibliotheken,](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html#using-preprocessors) bij het gebruik van proxy-clientbibliotheken moeten deze statische bronnen zich in een onderliggende map bevinden met de naam `resources` om effectief naar de publicatie-instanties te kunnen verwijzen.

#### Niet-conforme code {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Compatibele code {#compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Gebruik van Cloud Service niet-compatibele workflowprocessen {#oakpal-usage-cloud-service}

* **Sleutel**: CloudServiceIncompatibleWorkflowProcess
* **Type**: Code Smell
* **Ernst**: Blocker
* **Sinds**: Versie 2021.2.0

Met de overstap naar Asset micro-services voor de verwerking van bedrijfsmiddelen op AEM Cloud Service zijn verschillende workflowprocessen die werden gebruikt in on-premise en AMS-versies van AEM niet ondersteund of onnodig geworden.

Het migratiehulpmiddel in [AEM Assets as a Cloud Service GitHub-opslagplaats](https://github.com/adobe/aem-cloud-migration) kan worden gebruikt om workflowmodellen bij te werken tijdens de migratie naar AEM as a Cloud Service.

### Het gebruik van statische sjablonen wordt ontmoedigd ten gunste van bewerkbare sjablonen {#oakpal-static-template}

* **Sleutel**: StaticTemplateUsage
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

Terwijl het gebruik van statische malplaatjes historisch zeer algemeen in AEM projecten is geweest, worden de editable malplaatjes hoogst geadviseerd aangezien zij de meeste flexibiliteit verstrekken en extra eigenschappen steunen die niet in statische malplaatjes aanwezig zijn. Meer informatie vindt u in de [Paginasjablonen - Bewerkbare documentatie.](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html)

De migratie van statische aan editable malplaatjes kan grotendeels worden geautomatiseerd gebruikend [AEM moderniseringsinstrumenten.](https://opensource.adobe.com/aem-modernize-tools/)

### Het gebruik van verouderde stichtingscomponenten wordt ontmoedigd {#oakpal-usage-legacy}

* **Sleutel**: LegacyFoundationComponentUsage
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

De oudere Componenten van de Stichting (d.w.z. componenten onder `/libs/foundation`) zijn vervangen voor verschillende AEM [Core Components.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) Het gebruik van de componenten van de erfenisStichting als basis voor douanecomponenten, hetzij door bedekking of overerving, wordt ontmoedigd en zou in de overeenkomstige kerncomponent moeten worden omgezet.

Deze conversie kan worden vergemakkelijkt door de [AEM moderniseringsinstrumenten.](https://opensource.adobe.com/aem-modernize-tools/)

### Alleen ondersteunde namen en volgorde van de uitvoermodus mogen worden gebruikt {#oakpal-supported-runmodes}

* **Sleutel**: SupportedRunmode
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service past een strikt naamgevingsbeleid toe voor runmode-namen en een strikte volgorde voor deze runmodes. De lijst met ondersteunde runmodi vindt u in het gedeelte [Distribueren naar AEM as a Cloud Service documentatie](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes) en elke afwijking hiervan zal als een kwestie worden aangemerkt .

### De de definitieknoden van de indexdefinitie van het Onderzoek van de douane moeten directe kinderen van /eikel zijn:index {#oakpal-custom-search}

* **Sleutel**: OakIndexLocation
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service vereist dat definities van aangepaste zoekindexen (dat wil zeggen knooppunten van het type) `oak:QueryIndexDefinition`) zijn directe onderliggende knooppunten van `/oak:index`. Indexen op andere locaties moeten worden verplaatst om compatibel te zijn met AEM Cloud Service. Meer informatie over zoekindexen vindt u in de [Documentatie voor zoeken en indexeren van inhoud.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### Knooppunten voor definitie van aangepaste zoekindex moeten een compatVersion van 2 hebben {#oakpal-custom-search-compatVersion}

* **Sleutel**: IndexCompatVersion
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service vereist dat definities van aangepaste zoekindexen (dat wil zeggen knooppunten van het type) `oak:QueryIndexDefinition`) moet de `compatVersion` eigenschap ingesteld op `2`. Een andere waarde wordt niet ondersteund door AEM Cloud Service. Meer informatie over zoekindexen vindt u in de [Documentatie voor zoeken en indexeren van inhoud.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### De afstammende knopen van de Definitie van de Index van het Onderzoek van het Douane moeten van type zijn:niet gestructureerd {#oakpal-descendent-nodes}

* **Sleutel**: IndexDescendantNodeType
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

Problemen met moeilijk op te lossen problemen kunnen optreden wanneer een definitieknoopknooppunt van een aangepaste zoekindex niet-geordende onderliggende knooppunten bevat. Om dit te voorkomen, wordt aanbevolen dat alle afstammende knooppunten van een `oak:QueryIndexDefinition` knooppunt is van type `nt:unstructured`.

### Knooppunten voor aangepaste zoekindexdefinitie moeten een onderliggende node met de naam indexRules bevatten die onderliggende items bevat {#oakpal-custom-search-index}

* **Sleutel**: IndexRulesNode
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

Een correct gedefinieerd definitieknoopknooppunt van een aangepaste zoekindex moet een onderliggend knooppunt met de naam `indexRules` die op hun beurt ten minste één kind moeten hebben. Meer informatie vindt u in de [Oak-documentatie.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Knooppunten voor aangepaste zoekindexdefinitie moeten naamgevingsconventies volgen {#oakpal-custom-search-definitions}

* **Sleutel**: IndexName
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service vereist dat definities van aangepaste zoekindexen (dat wil zeggen knooppunten van het type) `oak:QueryIndexDefinition`) moet een naam krijgen volgens een specifiek patroon dat wordt beschreven op [Inhoud zoeken en indexeren.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)

### De de definitieknoden van de Definitie van de Index van het Onderzoek van de douane moeten de winst van het Type van Index gebruiken  {#oakpal-index-type-lucene}

* **Sleutel**: IndexType
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service vereist dat definities van aangepaste zoekindexen (dat wil zeggen knooppunten van het type) `oak:QueryIndexDefinition`) een `type` eigenschap met de waarde ingesteld op `lucene`. Indexering met oudere indextypen moet worden bijgewerkt voordat u naar AEM Cloud Service gaat. Zie de [Documentatie voor zoeken en indexeren van inhoud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) voor meer informatie .

### De definitieknooppunten van de index van het Onderzoek van de douane moeten geen bezit genoemd zaad bevatten {#oakpal-property-name-seed}

* **Sleutel**: IndexSeedProperty
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service staat definities van aangepaste zoekindexen niet toe (knooppunten van het type) `oak:QueryIndexDefinition`) van het bevatten van een eigenschap met de naam `seed`. Indexering met deze eigenschap moet worden bijgewerkt voordat u naar AEM Cloud Service gaat. Zie de [Documentatie voor zoeken en indexeren van inhoud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) voor meer informatie .

### De definitieknooppunten van de aangepaste zoekindex mogen geen eigenschap met de naam redex bevatten {#oakpal-reindex-property}

* **Sleutel**: IndexReindexProperty
* **Type**: Code Smell
* **Ernst**: Klein
* **Sinds**: Versie 2021.2.0

AEM Cloud Service staat definities van aangepaste zoekindexen niet toe (knooppunten van het type) `oak:QueryIndexDefinition`) van het bevatten van een eigenschap met de naam `reindex`. Indexering met deze eigenschap moet worden bijgewerkt voordat u naar AEM Cloud Service gaat. Zie de [Documentatie voor zoeken en indexeren van inhoud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use) voor meer informatie .

## Gereedschap Verzendoptimalisatie {#dispatcher-optimization-tool-rules}

In de volgende sectie worden de controles vermeld die door Cloud Manager zijn uitgevoerd met het hulpprogramma voor het optimaliseren van patches (DOT). Volg de verbindingen voor elke controle voor zijn definitie en details GitHub.

* [Onverwachte tokens voor configuratie van Dispatcher](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [Distributiesconfiguratie zonder offerte](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [Dispatcher Configuration Missing Brace](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [Dispatcher Configuration Extra Brace](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [Configuratie van verzender ontbreekt verplichte eigenschap](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [Vervangen eigenschap door configuratie van Dispatcher](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [Dispatcher Configuration not found](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [Opgenomen bestand voor HTTP-configuratie niet gevonden](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [Algemene configuratie van verzender](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [De Dispatcher-publicatiecapaciteit van het farm moet serverStaleOnError hebben ingeschakeld](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [Dispatcher publiceert landbouwbedrijffilters zou het gebrek moeten bevatten ontkent regels van de versie 6.x.x van AEM archetype](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [De Dispatcher publiceert landbouwbedrijfgeheime voorgeheugenstateslevel bezit zou >= 2 moeten zijn](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [De Dispatcher publiceerde landbouwbedrijfGracePeriod bezit zou >= 2 moeten zijn](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [Elke Dispatcher-farm moet een unieke naam hebben](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [De Dispatcher publiceert landbouwbedrijfgeheime voorgeheugen zou zijn ignoreUrlParams regels moeten hebben die op een manier van de lijst van gewenste personen worden gevormd](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [De Dispatcher publiceert landbouwbedrijfsfilters zouden de toegestane het Verdelen selecteurs op de manier van de lijst van gewenste personen moeten specificeren](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [De Dispatcher publiceert de landbouwbedrijffilters zouden de toegestane het achtervoegselpatronen van het Sling op de manier van de lijst van gewenste personen moeten specificeren](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [De &quot;Vereisen allen verleend&quot;richtlijn zou niet in een sectie van de Folder VirtualHost met een wortel folder-weg moeten worden gebruikt](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
