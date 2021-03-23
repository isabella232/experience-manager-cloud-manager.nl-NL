---
title: Opmerkingen bij de release 2018.5.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2018.5.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2018.5.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2018.5.0.
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
feature: Geen informatie
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---


# Opmerkingen bij de release voor 2018.5.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release voor [!UICONTROL Cloud Manager] Release 2018.5.0 beschreven.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2018.5.0 is 12 juli 2018.

## Wat is er nieuw?{#what-s-new}

* **CI/CD de Berichten**  van de Pijpleiding - De gebruikers zullen nu  [!UICONTROL Experience Cloud] berichten voor pijpleidingsgebeurtenissen zien. Raadpleeg de [Meldingen](notifications.md) voor meer informatie.

* **Geplande Implementaties**  van de Productie - De gebruikers kunnen een datum of een tijd, voor de plaatsingen van de Productie nu plannen. Raadpleeg [Uw code implementeren](deploying-code.md) voor meer informatie.

* **Statuspage** hernoemd naar  **Activity**.

* Specifieke informatie die op homepage voor kwesties wordt getoond die tijdens pijpleidingsuitvoering worden ontmoet.
* Verbeteringen in de infrastructuur voor het testen van prestaties.

## Opgeloste problemen {#bug-fixes}

* Onder bepaalde omstandigheden werd het onjuiste SonarQube-profiel gebruikt, wat leidde tot onjuiste maatstaven voor de codekwaliteit.
* De SonarQube-controle CQBP-75 negeerde bepaalde OSGi-annotaties.
* Toen de CI/CD-pijpleiding werd geannuleerd, werd de staat niet consistent weergegeven.

## Bekende problemen {#known-issues}

* Koppelingen naar **AEM** en **Monitoring** vanuit het scherm Programmalijst vervangen beide het huidige browsertabblad en openen een nieuw tabblad.

