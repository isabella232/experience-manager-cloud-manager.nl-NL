---
title: Opmerkingen bij de release 2023.9.0
description: Dit zijn de opmerkingen bij de release 2023.9.0 voor Cloud Manager.
feature: Release Information
source-git-commit: a3e926fa13d54da1322f3a5219519fae07ddb273
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# Opmerkingen bij de release 2023.9.0 van Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2023.9.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2023.9.0 is 14 september 2023. De volgende release is gepland voor 5 oktober 2023.

## Wat is er nieuw? {#what-is-new}

* Deze release bestaat alleen uit opgeloste problemen voor Cloud Manager.

## Opgeloste problemen {#bug-fixes}

* Wanneer een programma wordt geschrapt, wordt om het even welke bijbehorende, lopende pijpleiding ook geschrapt, die ervoor zorgen dat de pijpleiding niet verkeerd als ontbroken status wordt aangewezen.
* Af en toe, wanneer alle stappen van een pijpleidingsuitvoering &quot;voltooid&quot;zijn, wordt de status van de pijpleiding beschouwd als &quot;lopend&quot;, die het schijnen in een vastgelopen staat te zijn. Het wordt nu beschouwd als een &#39;complete&#39;.
* Voor bewaarplaatsaftakkingen die gebruikend het archetype van de codegenerator worden geproduceerd, ontbreekt de pijpleiding van CI/CD.
