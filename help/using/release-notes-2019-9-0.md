---
title: Opmerkingen bij de release 2019.9.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2019.9.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.9.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.9.0.
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---

# Opmerkingen bij de release voor 2019.9.0 {#release-notes-for}

Met de [!UICONTROL Cloud Manager] Release 2019.9.0 worden de criteria voor de beveiligingstest bijgewerkt, kunt u downloadbare monitoringgrafieken toevoegen en een aantal door de klant gemelde bruikbaarheidsproblemen verhelpen.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.9.0 is 12 september 2019.

## Wat is er nieuw?{#whats-new}

* De categorisering van de health check van het filter Verschuivende verwijzing is gewijzigd van Kritiek in Belangrijk.
* De categorisering van de statuscontrole van HTML Library Manager Config is gewijzigd van Kritiek in Belangrijk.
* U kunt grafieken nu controleren. Raadpleeg [Uw omgevingen controleren](monitor-your-environments.md) voor meer informatie.
* Als een programma geen productie-AEM heeft, kunt u op de programmacode op de bestemmingspagina klikken om naar de overzichtspagina van Cloud Manager te gaan. Er wordt dan geen dialoogvenster met foutmeldingen weergegeven.
* De **Pipeline Settings** Kaart op **Overzicht** pagina is hernoemd naar **Production Pipeline Settings**.
* De belangrijke keuzerondjes van het Gedrag van de Mislukt van het Gedrag zijn verwijderd uit code-kwaliteit slechts pijpleidingen.
* De **pagina van de Activiteit** toont nu de naam van de pijpleiding voor elke uitvoering.
* De uitvoeringspagina toont nu de naam van de pijpleiding.
* Het samenvattingsvenster Codekwaliteit bevat nu een beschrijving voor elke classificatie.

## Opgeloste problemen {#bug-fixes}

* Sommige gebruikers konden geen uitvoeringsdetails bekijken toen het op goedkeuring wachtte.
* Op de pagina **Overzicht** was de rechtermarge niet consistent.
* De bouwstijlcontainer kon uit geheugen in grote projecten lopen.
* Onder bepaalde omstandigheden, identificeerde de BannedPaths OakPAL regel geïnstalleerde inhoud onder /libs niet.
* Wanneer een kwaliteitsgate is geweigerd, is in de dialoogkop *Gedeeltelijk geslaagd* nog steeds &lt;a0/>getoond.

## Bekende problemen {#known-issues}

* Het downloaden van monitoringgrafieken is niet beschikbaar in Safari.
