---
title: Opmerkingen bij de release 2019.9.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2019.9.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.9.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.9.0.
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c

---

# Opmerkingen bij de release 2019.9.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2019.9.0 werkt de criteria van de veiligheidstest bij, voegt downloadbare controlegrafieken toe, en verhelpt sommige klant-gemelde bruikbaarheidskwesties.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.9.0 is 12 september 2019.

## Nieuwe functies {#whats-new}

* De categorisering van de health check van het filter Verschuivende verwijzing is gewijzigd van Kritiek in Belangrijk.
* De categorisering van de statuscontrole van HTML Library Manager Config is gewijzigd van Kritiek in Belangrijk.
* U kunt grafieken nu controleren. Raadpleeg [Monitor uw omgevingen](monitor-your-environments.md) voor meer informatie.
* Als een programma geen AEM-productieomgeving heeft, kunt u op de programmakaart van de bestemmingspagina klikken om naar de overzichtspagina van Cloud Manager te gaan. Er wordt dan geen dialoogvenster met foutmeldingen weergegeven.
* De **Kaart van Montages** van de Pijpleiding op de pagina van het **Overzicht** is hernoemd aan de Montages **van de Pijpleiding van de** Productie.
* De belangrijke keuzerondjes van het Gedrag van de Mislukt van het Gedrag zijn verwijderd uit code-kwaliteit slechts pijpleidingen.
* De pagina van de **Activiteit** toont nu de naam van de pijpleiding voor elke uitvoering.
* De uitvoeringspagina toont nu de naam van de pijpleiding.
* Het samenvattingsvenster Codekwaliteit bevat nu een beschrijving voor elke classificatie.

## Opgeloste problemen {#bug-fixes}

* Sommige gebruikers konden geen uitvoeringsdetails bekijken toen het op goedkeuring wachtte.
* Op de pagina **Overzicht** was de rechtermarge niet consistent.
* De bouwstijlcontainer kon uit geheugen in grote projecten lopen.
* Onder bepaalde omstandigheden, identificeerde de BannedPaths OakPAL regel geïnstalleerde inhoud onder /libs niet.
* Wanneer een kwaliteitsgate werd geweigerd, werd de dialoogkop nog steeds *Gedeeltelijk goedgekeurd*.

## Bekende problemen {#known-issues}

* Het downloaden van monitoringgrafieken is niet beschikbaar in Safari.
