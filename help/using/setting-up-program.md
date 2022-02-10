---
title: Uw programma instellen
seo-title: Set Up Your Program
description: Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van het programma moeten doen.
seo-description: After onboarding, the business owner will need to do some initial setup of Adobe AEM Cloud Manager. This involves setting the program description and defining the KPIs which will be used for performance testing.
feature: Getting Started
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Uw programma instellen {#setup-your-program}

Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van het programma moeten voltooien. Dit omvat het instellen van de programmabeschrijving en het definiëren van de prestatiekernindicatoren (KPI&#39;s) die zullen worden gebruikt voor het testen van de prestaties. U kunt desgewenst een miniatuur uploaden. Bovendien kan de bedrijfseigenaar de levering van milieu&#39;s vormen terwijl vestiging het programma.

De gedefinieerde KPI&#39;s dienen als basislijn voor het testen van de prestaties die elke keer dat de pijplijn wordt uitgevoerd, wordt doorgegeven.

>[!NOTE]
>De gedefinieerde KPI&#39;s worden gemeten bij tests die worden uitgevoerd op de **stadium** milieu. Doorgaans worden deze KPI&#39;s verkleind om ze aan te passen aan de mogelijkheden van de werkgebiedomgeving.
>Bijvoorbeeld, verwacht een gebruiker gemiddeld 1000 paginameningen per minuut in hun productie **Omgeving** en als er vier verzend-/publicatieservers in productie zijn, moet dit worden geschaald naar weergaven van 250 pagina&#39;s per minuut (ervan uitgaande dat hun werkgebiedomgeving slechts uit één verzender/publicatieserverdepaar bestaat).
>Bovendien zullen vele gebruikers een Netwerk van de Levering van de Inhoud (CDN), zoals Akamai of CloudFront vóór hun productiemilieu hebben. Sinds [!UICONTROL Cloud Manager] tests tegen het werkgebiedmilieu direct, zou KPI slechts op het verkeer moeten wijzen dat door CDN wordt verwacht over te gaan, namelijk, mist het geheime voorgeheugen. Dit zal doorgaans een relatief kleine ondergroep van het totale productieverkeer zijn.

## Gebruiken [!UICONTROL Cloud Manager] Om uw Programma te vestigen {#using-cloud-manager-to-setup-your-program}

Voer de onderstaande stappen uit om het programma in te stellen en KPI&#39;s te definiëren:

1. Klikken **Installatieprogramma** om het installatieproces te starten in [!UICONTROL Cloud Manager].

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > U kunt altijd schakelen, bewerken of een nieuw programma toevoegen vanuit de actiebalk, zoals in de onderstaande afbeelding wordt getoond.

   ![image1](assets/set-up-program/setup2.png)


1. De **Installatieprogramma** wordt de Edit Program Information weergegeven.

1. U ziet drie opties als **Algemeen**, **KPI**, en **Inrichting** tab.

1. In **Algemeen** uploadt u een miniatuur naar uw programma. U kunt ook een relevante beschrijving aan uw programma toevoegen.

   ![](assets/Setup_Program-General.png)

1. Onder **KPI**, kunt u uw twee KPIs (verwachtingen voor elke plaatsing) bepalen. Afzonderlijke KPI&#39;s worden gedefinieerd voor **AEM Sites** en **AEM Assets**. U kunt de KPI&#39;s opgeven voor de producten waarvoor u een licentie hebt.

   **AEM Sites**

   1. Wat is de 95e percentiele reactietijd die voor u aanvaardbaar is?

      * Aanbevolen waarde - 3 seconden
   1. Hoeveel paginaweergaven per minuut onder de piekbelasting?

      * Aanbevolen waarde - weergaven van 200 pagina&#39;s per minuut

   **AEM Assets**

   Sinds de eerste release van Cloud Manager kunnen de prestaties van AEM Sites-programma&#39;s worden getest. Met deze release is de mogelijkheid toegevoegd om ook prestatietests voor AEM Assets-programma&#39;s uit te voeren. De prestaties van de activa worden getest door elementen herhaaldelijk te uploaden tijdens een testperiode van 30 minuten en de verwerkingstijd voor elk middel en verschillende metingen op systeemniveau te meten.
Tijdens de Opstelling van het Programma, worden de activa-specifieke KPIs gespecificeerd:

   * 95e Processorverwerkingstijd
   * Per minuut geüploade elementen

   ![](assets/Setup_Program-KPIs.png)

1. Onder **Inrichting** kunt u de inrichtingsconfiguratie voor productie- en niet-productieomgevingen in uw programma weergeven of bewerken. U ziet **Autoscale is ingeschakeld**, als automatische schaling is ingeschakeld voor het programma.

   >[!NOTE]
   >De functie Automatisch schalen is alleen van toepassing op de productieomgeving en is mogelijk niet voor alle programma&#39;s van de klant beschikbaar.

   ![](assets/Setup_Program-Provisioning.png)

1. Klikken **Opslaan** om de installatiewizard te voltooien.

   >[!NOTE]
   >U kunt het programma altijd bewerken als het oorspronkelijke programma al is ingesteld. Volg de onderstaande stappen voor meer informatie.

## Een programma bewerken {#editing-program}

1. Navigeer vanuit het deelvenster **Cloud Manager** beginscherm.

1. Klikken op **Programma bewerken** om uw programma bij te werken of te wijzigen van **Overzicht** pagina, zoals weergegeven in de onderstaande afbeelding.

   ![](assets/set-up-program/edit-program1.png)

1. De **Programma bewerken** schermweergaven waarmee u uw programma kunt bijwerken of wijzigen.

   U kunt uw programmabeschrijving bijwerken via het menu **Algemeen** tab.

   ![](assets/set-up-program/edit-program-general.png)

   Navigeren naar **KPI** om informatie over AEM Sites en Middelen bij te werken.

   ![](assets/set-up-program/edit-program-kpi.png)

   Daarnaast kunt u navigeren naar **Inrichting** om de inrichtingsconfiguratie voor productie- en niet-productieomgevingen in uw programma te bewerken.

   ![](assets/set-up-program/edit-program-provision.png)

1. Klikken op **Bijwerken** om uw bewerkingen op te slaan.

## De volgende stappen {#the-next-steps}

Als u reeds opstelling de Pijpleiding hebt, zal de volgende uitvoering uw bijgewerkte montages in aanmerking nemen. Als u nog niet opstelling de pijpleiding hebt, volg de stappen om uw pijpleiding eerst te opstelling.

Zie de documenten [Productiepijpleidingen configureren](configuring-production-pipelines.md) en [Niet-productiepijpleidingen configureren](configuring-non-production-pipelines.md) voor het opzetten van de pijpleiding.
