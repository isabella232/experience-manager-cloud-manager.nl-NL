---
title: Uw omgevingen bewaken
seo-title: Uw omgevingen bewaken
description: 'null'
seo-description: Volg deze pagina om meer te weten te komen over System Monitoring in Cloud Manager. Dit gebeurt door de afzonderlijke instanties binnen een omgeving te observeren en een aantal verschillende meetgegevens voor elke instantie te volgen.
translation-type: tm+mt
source-git-commit: 16893b8bcd2b2d681a14bb6be3786e358e1952fb

---


# Systeembewaking {#system-monitoring}

Systeemcontrole in [!UICONTROL Cloud Manager] wordt uitgevoerd door de afzonderlijke instanties binnen een omgeving te observeren en een verscheidenheid aan meetgegevens voor elke instantie te volgen. Elke meting heeft twee bepaalde drempels - een *waarschuwingsdrempel* en een *kritieke drempel*.

Als een metrische waarde boven zijn kritische drempel ligt, wordt deze geacht zich in een kritieke toestand te bevinden; als een metrische waarde boven de waarschuwingsdrempel (maar onder de kritische drempel) ligt, wordt hij geacht zich in een waarschuwingsstatus te bevinden. De drempelwaarden worden ingesteld door Adobe Managed Services en kunnen worden weergegeven in [!UICONTROL Cloud Manager]. In de meeste gevallen zijn drempels consistent tussen klanten, maar er zijn gevallen waarin Adobe Managed Services drempelwaarden aanpast aan specifieke klantenvereisten. Vragen over de drempelwaarden moeten worden gericht aan uw Customer Success Engineer (CSE).

## Navigeren naar System Monitoring {#navigating-system-monitoring}

Het navigeren aan de eigenschap van de Controle van het Systeem kan op twee manieren worden gedaan.

1. Meld u aan bij **Beheerde services - bestemmingspagina van programma** &#39;s.

   ![](assets/ProgramLanding.png)

1. Klik op het vierde pictogram op de programmakaart.

   ![](assets/first-timea1.png)

   *Of*,

* Navigeer naar de landingspagina **System Monitoring** via de menuoptie **Reports** global navigation in [!UICONTROL Cloud Manager].


## Overzichtspagina voor systeemcontrole {#system-monitoring-overview-page}

De pagina van het Overzicht van de Controle van het Systeem maakt een lijst van de gecontroleerde milieu&#39;s in het programma en rapporteert over hun gezondheid op hoog niveau over vier afzonderlijke categorieën:

* **Host**
* **Opslag**
* **Netwerk**
* **Toepassing**

De status in elke categorie is een overzicht van individuele metriek - als om het even welke metrisch in een categorie in de kritieke staat is, is de gehele categorie in een kritieke staat voor het doel van de overzichtspagina. Dezelfde samenvatting kan op milieuniveau en op instantieniveau worden bekeken.

![](assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>Wanneer u naar deze pagina navigeert, zijn de exemplaren van de productieomgeving standaard zichtbaar, maar kunnen ook andere omgevingen worden geopend.

## Videozelfstudie {#video-tutorial}

### Overzicht van rapporten in Cloud Manager {#reports-video}

Cloud Manager-rapporten bieden een weergave van de omgevingen en AEM-instanties van het programma aan de hand van een set grafieken die een aantal verschillende meetgegevens voor elke AEM-instantie rapporteren en bijhouden.
Raadpleeg de onderstaande video voor meer informatie.

>[!VIDEO](https://video.tv.adobe.com/v/26315/)

## System Monitoring Detail {#system-monitoring-detail}

Als u de details van bepaalde metriek wilt weergeven, klikt u op een van de categorieën in de linkernavigatie of klikt u op een van de categorie-indicatoren voor een specifiek geval. Elke detailpagina bevat een reeks grafieken voor de meetgegevens in die categorie. U kunt de metriek voor alle instanties in een milieu of voor een specifieke instantie bekijken. U kunt schakelen tussen de omgeving en instanties met behulp van de vervolgkeuzelijsten in de rechterbovenhoek.

![](assets/System_Monitoring1.png)

De navigatie op de linkerzijde zal de beschikbare metriek binnen de momenteel geselecteerde categorie tonen waarvoor er gegevens voor de momenteel geselecteerde milieu en instanties zijn.

![](assets/System_Monitoring2.png)

Een individuele grafiek zal de status en een grafiek van de gegevens in tijd samen met de drempels tonen. Als er meerdere instanties worden weergegeven, bevinden de gegevens van elke instantie zich in een aparte reeks.

![](assets/Monitoring_Graphs1.png)

Individuele reeksen kunnen op een grafiek worden verborgen door op de reeks in de legenda te klikken.
Als u bijvoorbeeld op de waarschuwingsdrempelreeks klikt, ziet u alleen de kritieke drempel.

![](assets/Monitoring_Graphs2.png)

### Metrische definities {#metric-definitions}

**Host**

* Laden per kern: het aantal processen dat door cpu wordt uitgevoerd of in een wachtstand gemiddeld over een (lading1), vijf (lading5), en vijftien (lading15) minieme periode is.
* Procesaantal: het aantal momenteel geopende processen.
* Aantal gebruikers: het aantal gebruikers met een actieve shellsessie.
* Geheugengebruik: het percentage systeemgeheugen dat momenteel is toegewezen.
* JVM-geheugen (heap): de grootte (in megabytes) van de toegewezen Java-heap.
* Ruimte van de oude generatie: het percentage JVM Old Generation-geheugen dat momenteel is toegewezen.

**Netwerk**

* Controle CQ-poort: De responstijd in seconden voor toegang tot de AEM- of Dispatcher-poort. Er zijn verschillende meetgegevens voor auteur, publicatie en verzender.

**Opslag**

* Schijfruimte: De gebruikte schijfruimte (in megabytes) voor elk koppelingspunt op de gastheer. Er zijn verschillende meetwaarden voor elk koppelingspunt. Minstens, zult u metriek voor &quot;/&quot;en &quot;/mnt&quot;zien, maar de extra metriek van het koppelingspunt kan afhankelijk van de specifieke instantieconfiguratie beschikbaar zijn.
* Mapgrootte: AEM-segmentwinkel: De gebruikte schijfruimte (in gigabytes) voor de AEM Segment Store.

**Toepassing**

* Replicatieagent: De tijd, in seconden, voor een gebeurtenis van de testreplicatie. Er zijn afzonderlijke metriek voor elke replicatieagent.
* Uitspoelen van verzender: Het aantal items dat zich momenteel in de verzendingswachtrij bevindt.

## SLA-rapportage {#sla-reporting}

Klanten kunnen de prestaties van hun productie-AEM-omgeving zien in verhouding tot hun contractuele Service Level Agreement (SLA). Dit is beschikbaar door een submenu op het scherm van Rapporten.
De onderstaande grafiek toont bijvoorbeeld het maandelijkse SLA-resultaat voor 2018.

![](assets/SLA-Reports-one.png)

Net als bij systeemgrafieken worden bij het verschuiven van een gegevenspunt de specifieke waarden voor die maand weergegeven.

![](assets/SLA-Reports-two.png)

In het gedeelte Gebeurtenisanalyse onder deze grafiek ziet u de reeks incidenten die zich tijdens het geselecteerde jaar voor het programma hebben voorgedaan. Elk incident heeft een tijdbereik, een oorzaak en een reeks opmerkingen.

![](assets/sla-reporting3.png)

## SLA-waarden {#sla-metrics}

* **Auteurscontract**: Dit is de SLA die is gedefinieerd in uw contract met Adobe Managed Services voor de auteurslaag.

* **AMS-auteur SLA**: Dit is de gemeten uptime van de door Adobe of onze leveranciers veroorzaakte voorvallen met betrekking tot laagfactoring van de productiefunctie.

* **SLA** van auteur: Dit is de gemeten uptime van de auteurslaag die geplande onderbreking zoals onderhoudsvensters negeert.

* **Eindgebruikerscontract**: Dit is de SLA die is gedefinieerd in uw contract met Adobe Managed Services voor de publicatielijst.

* **SLA** eindgebruiker AMS: Dit is de gemeten uptime van de productie publiceer lijstfactoring incidenten die door Adobe of onze verkopers worden veroorzaakt.

* **SLA** eindgebruiker: Dit is de gemeten uptime van de publicatielaag die geplande downtime, zoals onderhoudsvensters, negeert.