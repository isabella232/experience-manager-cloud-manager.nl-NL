---
title: De wizard gebruiken
description: Volg deze pagina om te leren hoe u de wizard kunt gebruiken om een AEM Application Project te maken
translation-type: tm+mt
source-git-commit: 7146a41d64365c9de03d32f4fc4c33f9e366c244
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 9%

---


# De wizard {#using-wizard-to-create-an-aem-application-project} gebruiken

Als klanten aan boord zijn van Cloud Manager, krijgen ze een lege git-opslagplaats. Huidige klanten van Adobe Managed Services (AMS) (of on-premise AEM klanten die naar AMS migreren) hebben doorgaans al hun projectcode in git (of een ander versiecontrolesysteem) en zullen hun project importeren in de opslagplaats van Cloud Manager. Nieuwe klanten hebben echter geen bestaande projecten.

Om nieuwe klanten aan de slag te helpen, kan Cloud Manager nu een minimaal AEM project maken als startpunt. Dit proces is gebaseerd op [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).


Voer de onderstaande stappen uit om een AEM toepassingsproject te maken in Cloud Manager:

1. Nadat u zich hebt aangemeld bij Cloud Manager en de basisconfiguratie van het programma is voltooid, wordt een speciale aanroep naar een actiekaart weergegeven op het scherm **Overzicht** als de opslagplaats leeg is.

   ![](assets/image2018-10-3_14-29-44.png)

1. Klik op **Maken tot aan** om een dialoogvenster te openen waarin de gebruiker de parameters kan opgeven die vereist zijn voor het AEM Projectarchetype. In zijn standaardvorm, vraagt de dialoogdoos twee waarden:

   * **Titel**  - standaard wordt deze ingesteld op  *Programmanaam*

   * **Nieuwe Branch Name**  - deze is standaard  *master*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   Het dialoogvenster heeft een lade die kan worden geopend door op de handgreep naar de onderkant van het dialoogvenster te klikken. In zijn uitgebreide vorm, toont de dialoog alle configuratieparameters voor Archetype. Veel van deze parameters hebben standaardwaarden die worden geproduceerd gebaseerd op **Title**.

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >Als **Title** bijvoorbeeld ***We.Finance*** is, wordt de parameter Base Maven Artifact Id gegenereerd als ***com.wefinance***. Deze waarden kunnen desgewenst worden gewijzigd.
   >
   >
   >U kunt bijvoorbeeld de gegenereerde ***value com.wefinance*** wijzigen in ***net.wefinance***.

1. Klik **creeer** in de voorafgaande stap om het starterproject tot stand te brengen door archetype te gebruiken en aan de genoemde git tak vast te leggen. Zodra dit wordt gedaan, kunt u opstelling de pijpleiding.