---
title: Evaluatie
seo-title: Evaluatie
description: 'Deze pagina dient als uitgangspunt voor het leren van de fase van de Evaluatie in de Tovenaar van de Update van het Product. '
seo-description: Deze pagina dient als uitgangspunt voor het leren van de fase van de Evaluatie in de Tovenaar van de Update van het Product.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: 3bb435aae932b9446867c30b7dd6b0a8e0839ee2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Evaluatiefase {#evaluation}

De eerste fase in de tovenaar van de Update van het Product is **[!UICONTROL Evaluation]** fase.
Hier kunt u de complexiteit van de upgrade beoordelen met de patroondetector die u rechtstreeks vanuit de wizard kunt gebruiken. Aan het einde van deze stap hebt u toegang tot het evaluatieverslag.

Met het gegenereerde rapport kunt u de instantie Auteur controleren op upgradebaarheid door patronen te detecteren die:

* Overtreed bepaalde regels en wordt uitgevoerd op gebieden die door de upgrade worden beïnvloed of overschreven.

* Gebruik een AEM 6.x-functie of een API die niet achterwaarts compatibel is met de nieuwe AEM en die na de upgrade mogelijk kan worden verbroken.

Dit dient als een beoordeling van de ontwikkelingsinspanningen die gepaard gaan met de opwaardering tot Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Als u meer wilt weten over patroondetector, raadpleegt u [De upgradecomplexiteit beoordelen met de patroondetector](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## De evaluator uitvoeren {#running-evaluator}

Voer de onderstaande stappen uit om een evaluatieverslag te genereren:

1. Klik op **[!UICONTROL Run Evaluation]**.

   >[!NOTE]
   >De patroondetector kan in elke omgeving worden uitgevoerd. Nochtans, om het ontdekkingstarief te verhogen en om het even welke vertragingen op bedrijfskritieke instanties te vermijden, zal de Manager van de Wolk het op het opvoeren milieu op de auteursinstantie in werking stellen.

   ![](assets/Run-Evaluation.png)

1. De wizard informeert u over de status van uw handeling. Wanneer het evaluatierapport wordt gegenereerd, wordt u op de hoogte gebracht van **Bezig** of **Voltooid** .

   Nadat het rapport is gegenereerd, kunt u klikken **[!UICONTROL Download report]** om een kopie op te slaan.

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >De huidige versie van de wizard Productupdates in Cloud Manager ondersteunt alleen de **evaluatiefase** . De andere vier fasen, te weten **herstel**, **uitvoering**, **validatie** en **voltooiing** , komen binnenkort.
