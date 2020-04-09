---
title: Uw programma instellen
seo-title: Uw programma instellen
description: Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van het programma moeten doen.
seo-description: 'Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van de Manager van de Wolk van Adobe moeten doen AEM. Dit omvat het instellen van de programmabeschrijving en het definiëren van de KPI''s die voor het testen van de prestaties zullen worden gebruikt. '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 16893b8bcd2b2d681a14bb6be3786e358e1952fb

---


# Uw programma instellen {#setup-your-program}

Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van het programma moeten voltooien. Dit omvat het instellen van de programmabeschrijving en het definiëren van de prestatiekernindicatoren (KPI&#39;s) die zullen worden gebruikt voor het testen van de prestaties. U kunt desgewenst een miniatuur uploaden. Bovendien kan de bedrijfseigenaar de levering van milieu&#39;s vormen terwijl vestiging het programma.

De gedefinieerde KPI&#39;s dienen als basislijn voor het testen van de prestaties die elke keer dat de pijplijn wordt uitgevoerd, wordt doorgegeven.

>[!NOTE]
>
>De gedefinieerde KPI&#39;s worden gemeten bij tests die in de **werkgebiedomgeving** worden uitgevoerd. Doorgaans worden deze KPI&#39;s verkleind om ze aan te passen aan de mogelijkheden van de werkgebiedomgeving.
>
>Bijvoorbeeld, zou een gebruiker die een gemiddelde van 1000 paginameningen per minuut in hun **Milieu** van de Productie verwacht en vier verzender/publiceer servers in productie heeft deze aan 250 paginameningen per minuut (veronderstellend hun werkgebiedmilieu uit slechts één verzender/publiceer serverpaar bestaat) moeten schrapen.
>
>Bovendien zullen vele gebruikers een Netwerk van de Levering van de Inhoud (CDN), zoals Akamai of CloudFront vóór hun productiemilieu hebben. Aangezien [!UICONTROL Cloud Manager] tests tegen het werkgebiedmilieu direct, KPI op slechts het verkeer zou moeten wijzen dat door CDN wordt verwacht over te gaan, namelijk mist het geheime voorgeheugen. Dit zal doorgaans een relatief kleine ondergroep van het totale productieverkeer zijn.

## Gebruikend [!UICONTROL Cloud Manager] om uw Programma te vestigen {#using-cloud-manager-to-setup-your-program}

Voer de onderstaande stappen uit om het programma in te stellen en KPI&#39;s te definiëren:

1. Klik op **Installatieprogramma** om het installatieproces in te starten [!UICONTROL Cloud Manager].

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > U kunt altijd schakelen, bewerken of een nieuw programma toevoegen vanuit de actiebalk, zoals in de onderstaande afbeelding wordt getoond.

   ![image1](assets/set-up-program/setup2.png)


1. Het scherm van het Programma **van de** Opstelling toont de Edit Informatie van het Programma.

1. U ziet drie opties als **Algemeen**, **KPI** en het tabblad **Inrichting** .

1. Upload op het tabblad **Algemeen** een miniatuur naar uw programma. U kunt ook een relevante beschrijving aan uw programma toevoegen.

   ![](assets/Setup_Program-General.png)

1. Onder **KPI**, kunt u uw twee KPIs (verwachtingen voor elke plaatsing) bepalen. Afzonderlijke KPI&#39;s worden gedefinieerd voor **AEM-sites** en **AEM-middelen**. U kunt de KPI&#39;s opgeven voor de producten waarvoor u een licentie hebt.

   **AEM Sites**

   1. Wat is de 95e percentiele reactietijd die voor u aanvaardbaar is?

      * Aanbevolen waarde - 3 seconden
   1. Hoeveel paginaweergaven per minuut onder de piekbelasting?

      * Aanbevolen waarde - weergaven van 200 pagina&#39;s per minuut
   **AEM Assets**

   Vanaf de eerste release van Cloud Manager kunnen de prestaties van AEM Sites-programma&#39;s worden getest. Met deze release is de mogelijkheid toegevoegd om ook prestatietests voor AEM Assets-programma&#39;s uit te voeren. De prestaties van de activa worden getest door elementen herhaaldelijk te uploaden tijdens een testperiode van 30 minuten en de verwerkingstijd voor elk middel en verschillende metingen op systeemniveau te meten.
Tijdens de Opstelling van het Programma, worden de activa-specifieke KPIs gespecificeerd:

   * 95e verwerkingstijd
   * Per minuut geüploade elementen
   ![](assets/Setup_Program-KPIs.png)

1. Onder **Provisioning** kunt u de inrichtingsconfiguratie voor productie- en niet-productieomgevingen in uw programma weergeven of bewerken. U ziet dat **Autoscale is ingeschakeld** als automatische schaling is ingeschakeld voor het programma.

   >[!NOTE]
   >
   >* De functie Automatisch schalen is alleen van toepassing op de productieomgeving en is mogelijk niet voor alle programma&#39;s van de klant beschikbaar.
   >* Schaling op aanvraag is niet beschikbaar voor deze release van [!UICONTROL Cloud Manager].


   ![](assets/Setup_Program-Provisioning.png)

1. Klik op **Opslaan** om de wizard Setup te voltooien.

   >[!NOTE]
   >
   >U kunt het programma altijd bewerken als het oorspronkelijke programma al is ingesteld. Volg de onderstaande stappen voor meer informatie.

## Een programma bewerken

1. Navigeer naar de oplossing op het **hoofdscherm van Cloud Manager** .

   ![](assets/SetUpProgram5.png)

1. Selecteer de oplossing en klik op **Bewerken** om uw programma bij te werken of te wijzigen, zoals in onderstaande afbeelding wordt getoond.

   ![](assets/SetUpProgram6.png)

1. In het scherm Programma **** bewerken kunt u uw programma bijwerken of wijzigen.

   ![](assets/Editing_Program-screen3.png)

## De volgende stappen {#the-next-steps}

Als u reeds opstelling de **Pijpleiding** hebt, zal de volgende uitvoering uw bijgewerkte montages in aanmerking nemen. Als u nog niet opstelling de pijpleiding hebt, volg de stappen eerst aan opstelling uw pijpleiding.

Gelieve te zien [vorm uw CI/CD Pijpleiding](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) voor vestiging de pijpleiding.
