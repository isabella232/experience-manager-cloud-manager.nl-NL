---
title: Opmerkingen bij de release 2019.12.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2019.12.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.12.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.12.0.
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Opmerkingen bij de release voor 2019.12.0 {#release-notes-for}

De volgende sectie schetst de algemene Nota&#39;s van de Versie voor [!UICONTROL Cloud Manager] Versie 2019.12.0 en voegt updates aan pijpleidingsuitvoering en verhogingen aan de scans van de codekwaliteit toe.
Volg de onderstaande secties voor meer informatie.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.12.0 is 12 december 2019.

## Wat is er nieuw?{#whats-new}

* De stappen in de pijpleidingsuitvoering tonen nu de voltooiingstijd voor elke stap.
* Scans voor de kwaliteit van de code voor projecten die geen code Java bevatten meldt nu een codecijfer van 100%.
* De health check van de CQ Dispatcher Configuration is verwijderd.

## Opgeloste problemen {#bug-fixes}

* Datums worden niet correct weergegeven in bepaalde browsers.
* In zeldzame gevallen zou de productiepijplijn naar de goedkeuringsstap gaan terwijl de prestatietests nog actief waren.
* In bepaalde toestanden zijn de knoppen in het bovenste gebied van de overzichtspagina niet correct uitgelijnd.
* In bepaalde omstandigheden zagen onbevoegde gebruikers een knoop om de pijpleiding te beginnen, hoewel de knoop zelf niet klikbaar was.
* De actieknoppen voor niet-productiepijpleidingen worden soms op de verkeerde locatie weergegeven.
* Pakketten met de graniet:Het knooppunttype Rangschikken kon niet voor bepaalde schendingen van de kwaliteitsregel worden gescand.
* Bepaalde fouten in het codekwaliteitsproces zijn onjuist als fouten geteld.
* De gegevens van de controle konden niet voor bepaalde topologieën worden geladen.
