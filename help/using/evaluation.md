---
title: Evaluatie
seo-title: Evaluatie
description: 'Deze pagina dient als uitgangspunt voor het leren van de fase van de Evaluatie in de Tovenaar van de Update van het Product. '
seo-description: Deze pagina dient als uitgangspunt voor het leren van de fase van de Evaluatie in de Tovenaar van de Update van het Product.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Aan de slag
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Evaluatiefase {#evaluation}

De eerste fase in de tovenaar van de Update van het Product is **[!UICONTROL Evaluation]** fase.
Hier kunt u de complexiteit van de upgrade beoordelen met de patroondetector die u rechtstreeks vanuit de wizard kunt gebruiken. Aan het einde van deze stap hebt u toegang tot het evaluatieverslag.

Met het gegenereerde rapport kunt u de instantie Auteur controleren op een upgrade door patronen te detecteren die:

* Overtreed bepaalde regels en wordt uitgevoerd op gebieden die door de upgrade worden beïnvloed of overschreven.

* Gebruik een AEM 6.x-functie of een API die niet achterwaarts compatibel is met de nieuwe AEM en die na de upgrade mogelijk kan worden onderbroken.

Dit dient als een beoordeling van de ontwikkelingsinspanningen die gepaard gaan met de opwaardering tot Adobe Experience Manager (AEM) 6.5.

>[!NOTE]
>
>Als u meer wilt weten over patroondetector, raadpleegt u [De upgradecomplexiteit beoordelen met de patroondetector](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## Evaluator {#running-evaluator} uitvoeren

Voer de onderstaande stappen uit om een evaluatieverslag te genereren:

1. Klik op **[!UICONTROL Run Evaluation]**.

   >[!NOTE]
   >
   >De patroondetector kan in elke omgeving worden uitgevoerd. Nochtans, om het ontdekkingstarief te verhogen en om het even welke vertragingen op bedrijfskritieke instanties te vermijden, zal de Manager van de Wolk het op het opvoeren milieu op de auteursinstantie in werking stellen.

   ![](assets/Run-Evaluation.png)

1. De wizard informeert u over de status van uw handeling. U zult **Bezig** of **completed** zoals toepasselijk merken wanneer het evaluatierapport wordt geproduceerd.

   Nadat het rapport is gegenereerd, kunt u op **[!UICONTROL Download report]** klikken om een kopie op te slaan.

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >De huidige versie van de tovenaar van de Update van het Product in de Manager van de Wolk steunt **Evaluatie** slechts fase. De andere vier fasen, te weten **Remediation**, **Execution**, **Validation** en **Completion**, komen binnenkort.
