---
title: Toegang tot opslagplaatsen
seo-title: Toegang tot opslagplaatsen
description: Op deze pagina wordt beschreven hoe u de Git-opslagplaats kunt openen en beheren.
seo-description: Volg deze pagina voor meer informatie over het openen en beheren van uw Git-opslagplaats.
feature: Opslagplaatsen voor git
exl-id: 403fc93d-60fc-4439-8c9d-0a512ca34458
source-git-commit: 5bbe76a46b7a15ccbab85c4487d2a20aaf59a4e7
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---

# Toegang tot opslagplaatsen {#accessing-repos}

U kunt de Git Repository openen en beheren met Self-Service Git Account Management vanuit de interface van Cloud Manager.

## Het gebruik van Self-Service Git Account Management {#self-service-git}

Gebruik de **Access Repo Info** knoop beschikbaar bij de UI van de Manager van de Wolk, het meest opvallend op de pijpleidingskaart.

1. Navigeer naar **Pipelines** kaart van uw **Overzicht van het Programma** pagina.

1. U zult **Toegang Repo Info** optie bekijken om tot uw Bewaarplaats van de Bewaarplaats van de Git toegang te hebben en te beheren.

   ![](assets/access-repo1.png)

   Bovendien, als u **niet-Productie** pijpleidingslusje selecteert, zult u de **optie van de Reactie van de Toegang ook daar bekijken Info**.

   ![](assets/access-repo-nonprod.png)


   >[!NOTE]
   >De optie **Repo-info benaderen** is zichtbaar voor gebruikers in de rol Developer of Deployment Manager. Als u op deze knop klikt, wordt een dialoogvenster geopend waarin de gebruiker de URL naar zijn of haar gegevensopslagruimte voor de Intel Health Care Management Suite kan vinden, samen met de gebruikersnaam en het wachtwoord.

   ![](assets/access-repo-create.png)

   De belangrijkste aspecten voor het beheer van uw Git in Cloud Manager zijn:

   * **URL**: De URL van de gegevensopslagruimte
   * **Gebruikersnaam**: De gebruikersnaam
   * **Wachtwoord**: De waarde die wordt weergegeven wanneer op de knop **Wachtwoord genereren** wordt geklikt.


      >[!NOTE]
      >Een gebruiker kan een kopie van de code uitchecken en wijzigingen aanbrengen in de lokale gegevensopslagruimte. Als de gebruiker klaar is, kan hij of zij de wijzigingen in de code doorvoeren naar de externe opslagplaats voor code in Cloud Manager.
