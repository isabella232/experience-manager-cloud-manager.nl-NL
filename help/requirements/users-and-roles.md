---
title: Gebruikers en rollen toevoegen
description: Leer hoe u de Admin Console gebruikt om gebruikers en rollen toe te voegen en profielen te maken.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: dd96d773ea3e6b9c45886fe41b28d3dd70cb8a61
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 5%

---


# Gebruikers en rollen toevoegen {#add-users-and-roles}

Veel functies in [!UICONTROL Cloud Manager] specifieke rechten vereisen om te gebruiken. Zo kunnen alleen bepaalde gebruikers de prestatiekernindicatoren (KPI&#39;s) voor een programma instellen. Deze toestemmingen worden logisch gezien gegroepeerd in rollen.

[!UICONTROL Cloud Manager] definieert momenteel vier rollen voor gebruikers die de beschikbaarheid van specifieke functies bepalen:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

>[!NOTE]
>
>Te gebruiken [!UICONTROL Cloud Manager], hebt u een Adobe ID en de Adobe Managed Services-productcontext nodig.

## Roldefinities {#role-definitions}

Deze lijst vat de rollen samen.

| [!UICONTROL Cloud Manager] Rol | Beschrijving |
|--- |--- |
| Zakelijke eigenaar | Deze gebruiker is verantwoordelijk voor het definiëren van KPI&#39;s, het goedkeuren van productieimplementaties en het overschrijven van belangrijke 3-tivelige fouten indien nodig. |
| Programmabeheerder | Deze gebruiker gebruikt [!UICONTROL Cloud Manager] om teamopstelling uit te voeren, status te herzien, KPIs te bekijken, en kan belangrijke 3-rij mislukkingen goedkeuren wanneer noodzakelijk. |
| Implementatiebeheer | Deze gebruiker beheert implementatiebewerkingen en gebruikt [!UICONTROL Cloud Manager] om het opvoeren/productie plaatsingen uit te voeren, CI/CD pijpleidingen uit te geven, belangrijke 3-rij mislukkingen goed te keuren wanneer nodig, en tot de git bewaarplaats te kunnen toegang hebben. |
| Ontwikkelaar | Deze gebruiker ontwikkelt en test de code van de douanetoepassing en hoofdzakelijk gebruikt [!UICONTROL Cloud Manager] om de implementatiestatus te bekijken en toegang te krijgen tot de git-opslagplaats voor codeverplichtingen. |
| Klantsuccesvolle technicus | Deze gebruiker steunt over het algemeen klantensucces voor klanten AMS en wisselt met [!UICONTROL Cloud Manager] voor het uitvoeren van implementaties die toezicht op de bedrijfsorganisatie vereisen. |
| Inhoudsauteur | Deze gebruiker communiceert doorgaans niet met [!UICONTROL Cloud Manager] maar kan [!UICONTROL Cloud Manager] programmaschakelaar om tot AEM toegang te hebben. |

>[!NOTE]
>
>De ontwikkelaar persona in de Admin Console heeft geen verband met de rol van de ontwikkelaar in [!UICONTROL Cloud Manager].

## Admin Console gebruiken om een profiel te maken {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] rollen worden beheerd van de Admin Console. Specifieke rollidmaatschappen worden verstrekt door de gebruiker aan een [!UICONTROL Cloud Manager] productprofiel.

De Admin Console is een centrale plaats voor het beheren van uw rechten van de Adobe over uw volledige organisatie. Raadpleeg de documentatie voor meer informatie over de Adobe Admin Console [Admin Console.](https://helpx.adobe.com/nl/enterprise/using/admin-console.html)

Om de aangewezen op rol-gebaseerde toestemmingen te verstrekken aan [!UICONTROL Cloud Manager] gebruikers, moet een beheerder in de organisatie van de klant nieuwe productprofielen tot stand brengen onder [!UICONTROL AEM Managed Services] productcontext die overeenkomt met elk van de vier [!UICONTROL Cloud Manager] rollen:

* Zakelijke eigenaar
* Implementatiebeheer
* Ontwikkelaar
* Programmabeheerder

Met de Admin Console kunt u gebruikers/groepen maken of toevoegen aan deze productprofielen.

1. Meld u aan bij de Admin Console op [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Klik op de knop **Overzicht** klikt u op het product dat u wilt wijzigen op het tabblad **Producten en diensten** kaart. Als het daar niet wordt vermeld, gebruik **Producten** om het product te zoeken en erop te klikken.

   ![Overzicht van beheerconsole, tabblad](/help/assets/admin-console-overview.png)

1. Op de **Producten** klikt u op de omgeving waaraan u gebruikers/groepen wilt toevoegen aan productprofielen.

   ![Tabblad Admin Console-producten](/help/assets/admin-console-product.png)

1. Op de **Productprofiel** tabblad van het product klikt u op **Nieuw profiel** om een nieuw profiel toe te voegen.

   ![Nieuw profiel](/help/assets/admin-console-product-profiles.png)

1. Geef informatie voor het instellen van een nieuwe rol voor [!UICONTROL Cloud Manager].

   * **Profielnaam** - de **Profielnaam** kan om het even wat zijn, hoewel om verwarring te vermijden het wordt geadviseerd om de waarden in **Aanbevolen profielnaam** kolom.
   * **Weergavenaam** - de **Weergavenaam** moet de technische waarde zijn die wordt gedefinieerd door [!UICONTROL Cloud Manager] (zie de volgende tabel).
   * **Machtigingengroep** - U kunt een machtigingengroep voor het profiel kiezen (niet altijd beschikbaar).

   ![Een nieuw profiel maken](/help/assets/screen_shot_2018-05-04at171819.png)

   | Rol | Weergavenaam (vereist) | Aanbevolen profielnaam |
   |---|---|---|
   | Zakelijke eigenaar | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol bedrijfseigenaar |
   | Implementatiebeheer | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van implementatiebeheer |
   | Ontwikkelaar | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van ontwikkelaar |
   | Programmabeheerder | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van programmamanager |


1. Klikken **Gereed** om het nieuwe profiel op te slaan.

## Profielen toewijzen aan gebruikers of gebruikersgroepen {#assign-profiles}

Nadat u productprofielen hebt gemaakt, kunt u gebruikers of gebruikersgroepen aan deze profielen toewijzen.

1. Meld u aan bij de Admin Console op [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Kies in de Admin Console de optie **Gebruikers** tab.

   ![Tabblad Gebruikers](/help/assets/admin-console-users.png)

1. Klikken op **Gebruikers** in het linkernavigatievenster en klik vervolgens op een gebruiker om deze te wijzigen.

1. Klik op de knop voor ovaal in het dialoogvenster **Producten** en selecteert u **Bewerken**.

   ![Gebruiker bewerken](/help/assets/admin-console-edit-user.png)

1. In de **Producten en gebruikersgroepen bewerken** klikt u op de plusknop en selecteert u de profielen die u aan de gebruiker wilt toewijzen.

   * Als de gebruiker reeds aan de rollen wordt toegewezen, zal de plus knoop een Edit knoop (een potlood) zijn, maar werkt de zelfde manier.

   ![Producten en gebruikersgroepen bewerken](/help/assets/admin-console-edit-products-and-user-groups.png)

1. Klikken **Opslaan** om de profielen op te slaan naar de gebruiker.

Herhaal dezelfde stappen om profielen toe te wijzen aan gebruikersgroepen, maar selecteer **Gebruikersgroepen** van het linkernavigatievenster op **Gebruikers** tab. Klik op een gebruikersgroep en selecteer de optie **Toegewezen productprofielen** en klik op **Productprofiel toewijzen** om profielen toe te wijzen.

![Profielen toewijzen aan groep](/help/assets/admin-console-edit-user-groups.png)
