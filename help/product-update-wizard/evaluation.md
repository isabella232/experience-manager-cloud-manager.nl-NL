---
title: Evaluatiefase
seo-title: Evaluation Phase
description: Leer hoe de de evaluatiefase van de Tovenaar van de Update van het Product de verbeteringsingewikkeldheid met de patroondetector beoordeelt.
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: ce2145da3b9e605e8a41bac28df520f14e255557
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Evaluatiefase {#evaluation}

De eerste fase in de wizard Productupdates is **[!UICONTROL Evaluation]** fase, die de verbeteringsingewikkeldheid met de patroondetector direct binnen de tovenaar beoordeelt. Aan het einde van deze stap hebt u toegang tot een evaluatierapport.

Met het gegenereerde rapport kunt u controleren of de auteurinstantie geschikt is voor upgrades door patronen te detecteren die:

* Overtred bepaalde regels met betrekking tot gebieden die door de upgrade worden beïnvloed of overschreven.

* Gebruik een AEM 6.x-functie of een API die niet achterwaarts compatibel is met de nieuwe versie van AEM en die na de upgrade mogelijk kan worden onderbroken.

Het verslag dient als een beoordeling van de ontwikkelingsinspanningen die gepaard gaan met de opwaardering tot Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Raadpleeg het document voor meer informatie over patroondetector [De complexiteit van upgrades beoordelen met de patroondetector.](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=en)

## De evaluatie uitvoeren {#running}

De patroondetector kan in elke omgeving worden uitgevoerd. Nochtans, om het ontdekkingstarief te verhogen en om het even welke vertragingen op bedrijfskritieke instanties te vermijden, zal de Manager van de Wolk het op het opvoeren milieu van de auteursinstantie in werking stellen.

Voer de volgende stappen uit om het evaluatieverslag te genereren.

1. De wizard starten zoals wordt beschreven in het document [Wizard Productupdates.](/help/product-update-wizard/overview.md)

1. Klikken op **[!UICONTROL Run Evaluation]**.

   ![Evaluatie uitvoeren](/help/assets/Run-Evaluation.png)

1. De wizard informeert u over de status van uw handeling. U zult **In uitvoering** of **voltooid** indien van toepassing wanneer het evaluatieverslag wordt opgesteld.

1. Nadat het rapport is gegenereerd, kunt u op **[!UICONTROL Download report]** om een kopie op te slaan.

   ![Rapport gemaakt](/help/assets/Evaluation-1.png)

De huidige release van de wizard Productupdates in Cloud Manager ondersteunt de functie **Evaluatie** alleen fase. De andere vier fasen, namelijk **Herstel**, **Uitvoering**, **Validatie**, en **Voltooiing** binnenkort.
