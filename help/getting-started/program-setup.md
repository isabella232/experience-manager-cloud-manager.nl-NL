---
title: Programma instellen
description: Na het instappen, zal de bedrijfseigenaar één of andere aanvankelijke opstelling van het programma moeten doen.
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# Programma instellen {#program-setup}

Na het instappen voltooit de bedrijfseigenaar de aanvankelijke opstelling van het programma met inbegrip van het plaatsen van de programmabeschrijving en het bepalen van de belangrijkste prestatiesindicatoren (KPIs), die voor prestatietests worden gebruikt.

## Programma instellen met [!UICONTROL Cloud Manager] {#program-setup-cloud-manager}

Voer de volgende stappen uit om het programma in te stellen en KPI&#39;s te definiëren.

1. Aanmelden bij Cloud Manager [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie.

1. Klikken **Installatieprogramma** om het installatieproces te starten.

   ![Programma instellen](/help/assets/set-up-program/setup1.png)

1. In de **Installatieprogramma** kunt u de programmagegevens op drie tabbladen invoeren:

   * **Algemeen**
   * **KPI**
   * **Inrichting**

1. Op de **Algemeen** toevoegen, een beschrijving voor uw programma toevoegen en desgewenst een miniatuur uploaden door op **Foto wijzigen**.

   ![Tabblad Algemeen](/help/assets/Setup_Program-General.png)

1. Op de **KPI** , definieert u de KPI&#39;s. In dit voorbeeld worden afzonderlijke KPI&#39;s gedefinieerd voor **AEM Sites** en **AEM Assets**. U kunt de KPI&#39;s opgeven voor de producten waarvoor u een licentie hebt.

   * Zie de sectie [KPI&#39;s](#kpis) voor meer informatie over hoe KPI&#39;s worden gemeten in Cloud Manager.

   ![KPI&#39;s definiëren](/help/assets/Setup_Program-KPIs.png)

1. Op de **Inrichting** kunt u de schaalopties op aanvraag voor uw omgeving definiëren als automatische schaling is ingeschakeld voor uw programma.

   * Autoscaling is alleen van toepassing op de productieomgeving en is mogelijk niet voor alle programma&#39;s van de klant beschikbaar.

   ![Inrichtingsopties](/help/assets/Setup_Program-Provisioning.png)

1. Klikken **Opslaan** om de installatiewizard te voltooien.

Uw programma wordt gemaakt. Het kan enige minuten duren voordat de bronnen zijn ingericht voordat het programma klaar is voor gebruik.

## Een programma bewerken {#editing-program}

U kunt programma&#39;s bewerken nadat u ze hebt ingesteld. Voer de volgende stappen uit om een programma te bewerken.

1. Aanmelden bij Cloud Manager [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie.

1. Navigeer naar het programma vanuit het hoofdscherm van Cloud Manager.

1. Klikken op **Programma bewerken** om uw programma bij te werken of te wijzigen van **Overzicht** pagina.

   ![Programma bewerken, optie](/help/assets/set-up-program/edit-program1.png)

1. De **Programma bewerken** wordt weergegeven, zodat u uw programma kunt bijwerken. Zie de sectie [Programmainstelling met Cloud Manager](#program-setup-cloud-manager) voor meer informatie over de beschikbare velden.

   ![Dialoogvenster Programma bewerken](/help/assets/set-up-program/edit-program-general.png)

1. Klikken op **Bijwerken** om uw wijzigingen op te slaan.

Merk op dat de veranderingen onmiddellijk aan de Manager van de Wolk worden bewaard, maar niet in uw milieu&#39;s tot de volgende pijpleidingslooppas zullen worden weerspiegeld.

Als u nog geen pijpleiding hebt gecreeerd zie de documenten [Productiepijpleidingen configureren](/help/using/production-pipelines.md) en [Niet-productiepijpleidingen configureren.](/help/using/non-production-pipelines.md)

## Schakelen tussen programma&#39;s {#swithing-programs}

Wanneer u aan een programma werkt, kunt u snel naar een ander programma schakelen zonder terug te keren naar de overzichtspagina van Cloud Manager.

Gebruik de actiebalk om naar een ander programma te schakelen, het huidige programma te bewerken of een nieuw programma toe te voegen.

![Programmaschakelaar](/help/assets/set-up-program/setup2.png)

## KPI&#39;s {#kpis}

De plaatsen KPIs wordt gemeten op tests die op het opvoeren milieu worden in werking gesteld. Doorgaans worden deze KPI&#39;s verkleind om ze aan te passen aan de mogelijkheden van de testomgeving.

Bijvoorbeeld, zou een gebruiker die een gemiddelde van 1000 paginameningen per minuut in hun productiemilieu verwacht en vier verzender/het publiceren servers in productie heeft dit aan 250 paginameningen per minuut moeten schrapen. Hierbij wordt ervan uitgegaan dat hun testomgeving uit slechts één verzender/publicatieserverpaar bestaat.

De prestaties van de activa worden getest door elementen herhaaldelijk te uploaden tijdens een testperiode van 30 minuten en de verwerkingstijd voor elk middel en verschillende metingen op systeemniveau te meten.

U kunt een netwerk van de inhoudslevering (CDN) zoals Akamai of CloudFront vóór uw productiemilieu hebben. Sinds [!UICONTROL Cloud Manager] tests tegen het het opvoeren milieu direct, zou KPI op slechts het verkeer moeten wijzen dat door CDN wordt verwacht over te gaan, namelijk, mist het geheime voorgeheugen. Dit zal doorgaans een relatief kleine ondergroep van het totale productieverkeer zijn.

## Video-overzicht {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
