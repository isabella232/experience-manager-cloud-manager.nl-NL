---
title: Gebruikers en rollen toevoegen
description: Leer hoe u de Admin Console gebruikt om gebruikers en rollen toe te voegen en profielen te maken.
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 12%

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

>[!NOTE]
>
>Om tot de admin console toegang te hebben en opstelling uw team (gebruikers en rollen), bezoek [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

Om de aangewezen op rol-gebaseerde toestemmingen te verstrekken aan [!UICONTROL Cloud Manager] gebruikers, moet een beheerder in de organisatie van de klant nieuwe productprofielen tot stand brengen onder [!UICONTROL AEM Managed Services] productcontext die overeenkomt met elk van de vier [!UICONTROL Cloud Manager] rollen:

* Zakelijke eigenaar
* Implementatiebeheer
* Ontwikkelaar
* Programmabeheerder

Met de Admin Console kunt u gebruikers/groepen maken of toevoegen aan deze productprofielen.

1. Meld u aan bij de Admin Console en klik op **Nieuw profiel** om een nieuw profiel toe te voegen.

   ![Nieuw profiel](/help/assets/admin_console_roles-1.png)

1. Geef informatie voor het instellen van een nieuwe rol voor [!UICONTROL Cloud Manager].

   * **Profielnaam**
   * **Weergavenaam**
   * **Machtigingengroep**

1. Klikken **Gereed** om de stap voor het maken van profielen te voltooien.

Wanneer u productprofielen maakt, worden **Weergavenaam** moet de technische waarde zijn die wordt gedefinieerd door [!UICONTROL Cloud Manager] (zie de volgende tabel). De **Profielnaam** kan om het even wat zijn, hoewel om verwarring te vermijden het wordt geadviseerd om de waarden in **Aanbevolen profielnaam** kolom. Als u dit wilt doen, schakelt u bij het maken van het productprofiel de optie **Zelfde als profielnaam** uit en geeft u de bijbehorende waarde op als de **Weergavenaam**.

| **Rol** | **Weergavenaam (vereist)** | **Aanbevolen profielnaam** |
|---|---|---|
| Zakelijke eigenaar | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol bedrijfseigenaar |
| Implementatiebeheer | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van implementatiebeheer |
| Ontwikkelaar | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van ontwikkelaar |
| Programmabeheerder | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - Rol van programmamanager |

![Een nieuw profiel maken](/help/assets/screen_shot_2018-05-04at171819.png)

Nadat u een productprofiel hebt gemaakt, kunt u gebruikers (of groepen) aan deze productprofielen toevoegen.

![Gebruiker bewerken](/help/assets/image2018-4-9_15-19-26.png)

![Gebruikersgroepen](/help/assets/image2018-4-9_15-16-47.png)
