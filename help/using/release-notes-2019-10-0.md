---
title: Opmerkingen bij de release 2019.10.0
seo-title: Opmerkingen bij de release AEM Cloud Manager voor 2019.10.0
description: Volg deze pagina voor informatie over Cloud Manager Release 2019.10.0.
seo-description: Volg deze pagina voor informatie over AEM Cloud Manager Release 2019.10.0.
feature: Geen informatie
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Opmerkingen bij de release voor 2019.10.0 {#release-notes-for}

De volgende sectie schetst de algemene Nota&#39;s van de Versie voor [!UICONTROL Cloud Manager] Versie 2019.10.0 en voegt updates aan plaatsingsstappen toe en maakte projectversie behandeling.
Volg de onderstaande secties voor meer informatie.

## Releasedatum {#release-date}

De releasedatum voor [!UICONTROL Cloud Manager] versie 2019.10.0 is 10 oktober 2019.

## Wat is er nieuw?{#whats-new}

* Belangrijke delen van de implementatiestappen zijn beter uitgevoerd.
* Wanneer aangewezen, zal de versie van het bouwstijlproject Maven nu de projectversie in git opnemen.
* Tijdens het samenstellen zijn nieuwe omgevingsvariabelen beschikbaar.
* De pijplijnen van de niet-productie kunnen van de kaart op **Overzicht** pagina evenals API worden geschrapt.
* Er is een nieuwe facultatieve goedkeuringsstap onmiddellijk na de stap van de werkgebiedimplementatie, maar vóór de stap van de veiligheidstest.
* Wanneer het vormen van een pijpleiding CI/CD, kan het losmaken en het vastmaken van de instanties van de verzender van het ladingsverdelingsmechanisme voor dev en werkgebiedmilieu&#39;s worden overgeslagen.
Raadpleeg **[Implementatieproces](deploying-code.md#deployment-process)** voor meer informatie.
* De CLI van Cloud Manager is uitgebreid met ondersteuning voor het openen van logbestanden met uitvoeringsstappen.
* De API van de Manager van de Wolk steunt nu het uitgeven van de gevormde tak van een pijpleiding.
* Verzoeken die tijdens het testen van de prestaties worden uitgevoerd, bevatten nu een specifiek token ***CloudManagerTest*** in de gebruikersagent.

## Opgeloste problemen {#bug-fixes}

* Sommige kaarten op de pagina **Overview** zijn niet verticaal uitgelijnd.
* Door bepaalde slechte omstandigheden werden de executies van pijpleidingen niet correct gemarkeerd en werden latere executies voorkomen.
