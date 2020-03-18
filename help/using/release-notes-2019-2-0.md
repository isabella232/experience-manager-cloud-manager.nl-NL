---
title: Opmerkingen bij de release 2019.2.0
seo-title: Opmerkingen bij de release van AEM Cloud Manager voor 2019.2.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.2.0.
seo-description: Volg deze pagina om informatie op te halen voor AEM Cloud Manager Release 2019.2.0.
translation-type: tm+mt
source-git-commit: 98395c4413b1b6bfbb3a565388ffa32dc3880dff

---


# Opmerkingen bij de release 2019.2.0 {#release-notes-for}

De [!UICONTROL Cloud Manager] Versie van 2019.2.0 voegt een nieuw vermogen van de Controle van het Systeem toe. Hierdoor kunnen klanten de status van hun omgeving met Adobe Managed Services op systeemniveau bekijken.


## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.2.0 is 21 februari 2019.

## Nieuwe functies {#whats-new}

* Nieuwe functie voor systeemcontrole. Raadpleeg [Monitor uw omgevingen](monitor-your-environments.md) voor meer informatie.
* De verzender module in tovenaar-geproduceerde projecten bevat nu een README dossier.
* De sorteervolgorde van de problemen bij het scannen van code is verbeterd en afgestemd op de prioriteit van het probleem.
* Werkgebiedinstanties worden nu altijd teruggezet naar het taakverdelingsmechanisme, zelfs in het geval van een implementatiefout.
* Er is een nieuwe API-ontwikkelaarrol beschikbaar in de beheerconsole waarmee specifieke gebruikers toestemming kunnen krijgen om integraties te maken in de Adobe I/O-console. Raadpleeg [Ontwikkelaars](https://www.adobe.com/go/aac_api_prod_learn) beheren voor meer informatie.
* De versie van Maven Archetype is bijgewerkt naar versie 16.
* De versie van Maven is bijgewerkt naar versie 3.6.0.

## Opgeloste problemen {#bug-fixes}

* In sommige omstandigheden zouden pijpleidingen niet worden uitgevoerd wanneer de doelomgeving in Azure werd gehost.
* De volgorde van omgevingen was inconsistent.
* Prestatie-tests kunnen mislukken wanneer ontdekte paginapaden een komma bevatten.
* Wanneer een pijpleidingsuitvoering van Web UI werd begonnen, de browser achterknoop werkte niet correct.
* Met de koppeling Meer informatie op de overzichtspagina is geen nieuw tabblad geopend.
* Tijdens het uploaden van een programmaminiatuur is deze mogelijk niet meteen zichtbaar geweest.
* In sommige gevallen, ontbrak het Scannen van de Code wegens project-specifieke configuratie.
* De link Meer informatie op de kaart voor niet-productiepijpleidingen ging naar de verkeerde locatie.
* Wanneer een kwaliteitspoort werd genegeerd, werd de status inconsistent weergegeven.
* De klanten die koude reservetopologieën gebruiken ontvingen onjuiste resultaten voor veiligheidstests.
* Wanneer het creëren van een nieuw project gebruikend de tovenaar, was het niet mogelijk om een tak tot stand te brengen die het dash karakter bevat.

## Bekende problemen {#known-issues}

* Wanneer de controlegegevens worden vernieuwd, zijn verborgen reeksen niet verborgen.
* Klanten die hun bestaande SLA-rapporten willen bekijken, moeten handmatig navigeren tot de volgende release.

   Als u deze URL wilt formuleren, volgt u het patroon (`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`), bijvoorbeeld als URL voor uw Experience Cloud (`https://weretailprod.experiencecloud.adobe.com`) is, dan rapporteert uw SLA URL (`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`).

   Dit zal naar verwachting in de volgende versie met de beschikbaarheid van SLA rapporten binnen worden opgelost [!UICONTROL Cloud Manager].
