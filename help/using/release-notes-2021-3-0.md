---
title: Opmerkingen bij de release 2021.3.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2021.3.0
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Opmerkingen bij de release 2021.3.0 {#release-notes-for}

In de volgende sectie worden de algemene opmerkingen bij de release beschreven voor [!UICONTROL Cloud Manager] Release 2021.3.0.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] Versie 2021.3.0 is 11 maart 2021.
De volgende release is gepland voor 8 april 2021.

## Wat is er nieuw? {#whats-new}

* Een nieuw gereedschap voor codekwaliteit [Gereedschap Verzendoptimalisatie](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) is geïntroduceerd om de configuratie van de klantendispatcher te bevestigen.

* Gebruikers kunnen hun rol(en) in Cloud Manager nu bekijken door de **rol(en) in Cloud Manager weergeven** optie na het navigeren aan het pictogram van het Profiel van de Gebruiker (hoogste recht) van Verenigde Shell.

* Het label **Goedkeuringsaanvraag** is opnieuw gelabeld aan **Erkenning productie** voor meer duidelijkheid.

* De **Versie** label is opnieuw gelabeld aan **Git-tag** in het scherm van de de pijpleiding van de Productie uitvoeren.

* De labels die het gedrag definiëren wanneer belangrijke metriek niet aan de gedefinieerde drempel voldoen, zijn opnieuw gelabeld om hun werkelijke gedrag weer te geven - **Direct annuleren** en **Direct goedkeuren**. Zie [Het vormen van de Montages van de Pijpleiding](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) voor meer informatie .

* De lijsten met klassen en methoden zijn bijgewerkt op basis van versie `2021.3.4997.20210303T022849Z-210225` van de SDK van AEM Cloud Service.

## Opgeloste problemen {#bug-fixes}

* Bepaalde kwaliteitsproblemen zijn niet goed ontdekt wanneer pakketten in andere pakketten waren ingesloten.

* Wanneer de gebruiker bij gelegenheid vanaf de pagina voor de uitvoering van de pijpleiding navigeert onmiddellijk nadat een pijpleiding is gestart, wordt een foutbericht weergegeven met de mededeling dat de handeling is mislukt, hoewel de uitvoering daadwerkelijk wordt gestart.
