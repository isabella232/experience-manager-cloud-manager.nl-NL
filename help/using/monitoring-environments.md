---
title: Monitoringomgevingen
description: Leer hoe u uw omgevingen kunt controleren in Cloud Manager.
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Monitoringomgevingen {#monitoring-environments}

Leer hoe u uw omgevingen kunt controleren in Cloud Manager.

## Metrische drempelwaarden {#thresholds}

Systeemcontrole in [!UICONTROL Cloud Manager] wordt gedaan door de individuele instanties binnen een milieu te observeren en een verscheidenheid van metriek voor elke instantie te volgen. Elke metrisch heeft twee bepaalde drempels: een waarschuwingsdrempel en een kritische drempel.

Als metrisch zijn over zijn kritieke drempel is, wordt het beschouwd om in een kritieke staat te zijn. Als een metrische waarde boven de waarschuwingsdrempel (maar onder de kritische drempel) ligt, wordt deze als een waarschuwingsstatus beschouwd. De drempelwaarden worden ingesteld door Adobe Managed Services en kunnen worden weergegeven in [!UICONTROL Cloud Manager]. In de meeste gevallen zijn drempels consistent tussen klanten, maar er zijn gevallen waarin Adobe Managed Services drempelwaarden aanpast aan specifieke klantenvereisten. Vragen over de drempelwaarden moeten worden gericht aan uw Customer Success Engineer (CSE).

## Toegang tot systeemcontrole {#accessing-system-monitoring}

Volg deze stappen om tot de Controle van het Systeem toegang te hebben.

1. Aanmelden bij **Managed Services - Programma&#39;s** openingspagina.

   ![Beheerde serviceprogramma&#39;s](/help/assets/ProgramLanding.png)

1. Klik op het vierde pictogram op de programmakaart.

   ![Instellingen](/help/assets/first-timea1.png)


U kunt ook naar de **Systeembewaking** landingspagina door de **Rapporten** algemene menu-item voor navigatie binnen [!UICONTROL Cloud Manager].

## Overzicht van systeemcontrole {#system-monitoring-overview}

De overzichtspagina van de Controle van het Systeem maakt een lijst van de gecontroleerde milieu&#39;s in het programma en rapporteert over hun gezondheid op hoog niveau over vier afzonderlijke categorieën:

* Host
* Opslag
* Netwerk
* Toepassing

De status in elke categorie is een overzicht van de afzonderlijke meetwaarden. Als om het even welke metrisch in een categorie in de kritieke staat is, is de gehele categorie in een kritieke staat voor de overzichtspagina. Dezelfde samenvatting kan op milieuniveau en op instantieniveau worden bekeken.

![Systeemcontrole](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>Wanneer u naar deze pagina navigeert, zijn de exemplaren van de productieomgeving standaard zichtbaar, maar kunnen ook andere omgevingen worden weergegeven.

## System Monitoring Detail {#system-monitoring-detail}

Als u de details van bepaalde metriek wilt weergeven, klikt u op een van de categorieën in de linkernavigatie of klikt u op een van de categorie-indicatoren voor een specifiek geval. Elke detailpagina bevat een reeks grafieken voor de meetgegevens in die categorie. U kunt de metriek voor alle instanties in een milieu of voor een specifieke instantie bekijken. U kunt schakelen tussen de omgeving en instanties met behulp van de vervolgkeuzelijsten in de rechterbovenhoek.

![Omgeving selecteren](/help/assets/System_Monitoring1.png)

De navigatie op de linkerzijde zal de beschikbare metriek binnen de momenteel geselecteerde categorie tonen waarvoor er gegevens voor de momenteel geselecteerde milieu en instanties zijn.

![Metrische gegevens controleren](/help/assets/System_Monitoring2.png)

Een individuele grafiek zal de status en een grafiek van de gegevens in tijd samen met de drempels tonen. Als er meerdere instanties worden weergegeven, bevinden de gegevens van elke instantie zich in een aparte reeks.

![Metrische grafiek](/help/assets/Monitoring_Graphs1.png)

Individuele reeksen kunnen op een grafiek worden verborgen door op de reeks in de legenda te klikken.
Als u bijvoorbeeld op de waarschuwingsdrempelreeks klikt, ziet u alleen de kritieke drempel.

![Grafiek wijzigen](/help/assets/Monitoring_Graphs2.png)

### Metrische definities {#metric-definitions}

#### Host {#host}

* **Laden per kern**: Het aantal processen dat door cpu wordt uitgevoerd of in een wachtstand gemiddeld over een (lading1), vijf (lading5), en vijftien (lading15) minieme periode is
* **Procesaantal**: Het aantal momenteel geopende processen
* **Aantal gebruikers**: Het aantal gebruikers met een actieve shellsessie
* **Geheugenverbruik**: Het percentage systeemgeheugen dat momenteel is toegewezen
* **JVM-geheugen**: De grootte (in megabytes) van de toegewezen Java-heap
* **Ruimte van de oude generatie**: Het percentage JVM-geheugen van de oude generatie dat momenteel is toegewezen

#### Netwerk {#network}

* **Poortcontrole CQ**: De reactietijd in seconden om tot de haven van de AEM of van de Verzender toegang te hebben
   * Er zijn verschillende meetgegevens voor auteur, publicatie en verzender.

#### Opslag {#storage}

* **Schijfruimte**: De gebruikte schijfruimte (in megabytes) voor elk onderstelpunt op de host
   * Er zijn verschillende meetwaarden voor elk koppelingspunt.
   * Er zijn minstens metriek voor `/` en `/mnt`, maar mogelijk zijn aanvullende meetgegevens voor het koppelingspunt beschikbaar, afhankelijk van de specifieke instantieconfiguratie.
* **Mapgrootte**
* **AEM**: De gebruikte schijfruimte (in gigabytes) voor de opslag van het AEM Segment

#### Toepassing {#application}

* **Replication Agent**: De tijd (in seconden) voor een gebeurtenis van de testreplicatie
   * Er zijn afzonderlijke metriek voor elke replicatieagent.
* **Dispatcher Flush**: Het aantal items dat zich momenteel in de verzendingswachtrij bevindt

## SLA-rapportage {#sla-reporting}

Klanten kunnen de prestaties van hun productie AEM omgeving zien in verhouding tot hun overeenkomst inzake contractueel serviceniveau (SLA). Dit is beschikbaar via een submenu op het tabblad **Rapporten** scherm.

In de volgende grafiek wordt de maandelijkse SLA-prestaties voor 2018 weergegeven.

![SLA 2018-grafiek](/help/assets/SLA-Reports-one.png)

Net als bij systeemgrafieken worden bij het verschuiven van een gegevenspunt de specifieke waarden voor die maand weergegeven.

![Rollover gegevenspunt](/help/assets/SLA-Reports-two.png)

De **Gebeurtenisanalyse** in deze grafiek wordt de reeks incidenten weergegeven die zich tijdens het geselecteerde jaar voor het programma hebben voorgedaan. Elk incident heeft een tijdbereik, een oorzaak en een reeks opmerkingen.

![Gebeurtenisanalyse](/help/assets/sla-reporting3.png)

## SLA-waarden {#sla-metrics}

* **Auteurscontract**: Dit is de SLA die is gedefinieerd in uw contract met Adobe Managed Services voor de auteurslaag.
* **AMS Author SLA**: Dit is de gemeten uptime van de productiefabrikant van de rij die door Adobe of onze verkopers wordt veroorzaakt.
* **Auteur SLA**: Dit is de gemeten uptime van de auteurslaag die geplande onderbreking zoals onderhoudsvensters negeert.
* **Eindgebruikerscontract**: Dit is de SLA die is gedefinieerd in uw contract met Adobe Managed Services voor de publicatielijst.
* **AMS-SLA eindgebruiker**: Dit is de gemeten uptime van de productie publiceer lijst die incidenten door Adobe of onze verkopers worden veroorzaakt.
* **SLA eindgebruiker**: Dit is de gemeten uptime van de publicatielaag die geplande downtime, zoals onderhoudsvensters, negeert.

## Videozelfstudie {#video-tutorial}

Deze video biedt een overzicht van het gebruik van de diagrammen die zijn gemaakt door Cloud Manager Reports voor een weergave in uw programmaomgevingen.

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
