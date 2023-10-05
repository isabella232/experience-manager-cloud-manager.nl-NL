---
title: Opmerkingen bij de release 2023.10.0
description: Dit zijn de opmerkingen bij de release 2023.10.0 voor Cloud Manager.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 851364e74864c28b3bcd9285dfbe06ddb530eb10
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Opmerkingen bij de release 2023.10.0 voor Cloud Manager {#release-notes}

Op deze pagina worden de opmerkingen bij de release voor [!UICONTROL Cloud Manager] release 2023.10.0.

>[!NOTE]
>
>Raadpleeg voor de meest recente releaseopmerkingen voor Cloud Manager in AEM as a Cloud Service de [Cloud Manager in AEM opmerkingen bij de huidige release van as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] release 2023.10.0 is 5 oktober 2023. De volgende release is gepland voor 2 november 2023.

## Wat is er nieuw? {#what-is-new}

* De **Implementatiebeheer** rol kan [vormt een reeks inhoudspaden die of ongeldig of uit het geheime voorgeheugen van de AEM Dispatcher zal worden gespoeld wanneer een niet productiepijplijn in werking wordt gesteld.](/help/using/non-production-pipelines.md)
   * Deze geheim voorgeheugenacties zullen als deel van de stap van de plaatsingspijpleiding worden uitgevoerd, enkel nadat om het even welke inhoudspakketten worden opgesteld.
   * Deze instellingen gebruiken het standaardgedrag AEM Dispatcher.
* Met de release van oktober 2023 van Cloud Manager worden Java-versies bijgewerkt via een gefaseerde implementatie.
   * De kleine versies voor Java 8 en 11 en Maven zijn bijgewerkt en zullen in de komende twee maanden geleidelijk worden geïmplementeerd. De nieuwe versie heeft veelvoudige veiligheidsmoeilijke situaties en insecten. De nieuwe versies zijn:
   * *Gemaakt: 3.8.8*
   * *Java 8-versie: /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11-versie: /usr/lib/jvm/jdk-11.0.20*
   * [Zie het advies van OpenJDK](https://openjdk.org/groups/vulnerability/advisories/) voor meer informatie over de beveiliging en foutoplossingen in deze JDK-updates.
