---
title: Werken met uw eigen GitHub-opslagplaatsen in Cloud Manager
description: Leer hoe te de Manager van de opstelling Cloud om met uw eigen bewaarplaatsen te werken GitHub.
feature: Release Information
exl-id: e0d103c9-c147-4040-bf53-835e93d78a0b
source-git-commit: 3bb59686a3c25e47e5c747bb8d5f626055e54a06
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Werken met uw eigen GitHub-opslagplaatsen in Cloud Manager {#byo-github}

Door de Manager van de Wolk te vormen om met uw eigen bewaarplaatsen te werken GitHub, kunt u uw code direct binnen uw bewaarplaats GitHub door de Manager van de Wolk bevestigen, die de behoefte elimineert om uw code met de bewaarplaats van de Adobe constant te synchroniseren.

>[!NOTE]
>
>Deze functie is alleen beschikbaar voor [het programma voor vroegtijdige adoptie .](/help/release-notes/current.md#early-adoption)

## Configuratie {#configuration}

De configuratie bestaat uit twee hoofdstappen:

1. [Opslagplaats toevoegen](#add-repo)
1. [Eigendom van privéopslagplaats valideren](#validate-ownership)

### Opslagplaats toevoegen {#add-repo}

1. In Cloud Manager, via de **Programmaoverzicht** pagina, tik of klik op **Opslagplaatsen** tab naar **Opslagplaatsen** pagina en klik op **Opslagplaats toevoegen**.

1. In de **Opslagplaats toevoegen** dialoogvenster, selecteren **Particuliere opslagplaats** als het type opslagplaats.

1. Geef de gegevens van uw opslagplaats op

   * **Naam opslagplaats** - Een expressienaam
   * **URL opslagplaats** - De URL van de opslagplaats, die moet eindigen in `.git`
   * **Beschrijving** (optioneel) - Een langere beschrijving van de opslagplaats indien nodig

   ![Eigen opslagplaats toevoegen](/help/assets/repositories/add-own-github.png)

1. Tik of klik op **Opslaan**.

>[!TIP]
>
>Zie het document voor meer informatie over het beheer van opslagruimten in Cloud Manager [Opslagplaatsen voor Cloud Manager.](/help/managing-code/repositories.md)

### Eigendom van privéopslagplaats valideren {#validate-ownership}

Cloud Manager weet nu van uw bewaarplaats GitHub, maar het heeft nog toegang tot het nodig. Om toegang te verlenen, moet u de Adobe toepassing GitHub installeren en verifiëren dat u de gespecificeerde bewaarplaats bezit.

1. Nadat u uw eigen opslagplaats hebt toegevoegd, **Eigendom van privéopslagplaats valideren** wordt geopend.

   ![Eigendom van privéopslagplaats valideren](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager gebruikt een GitHub-app om veilig te communiceren met uw opslagplaats.
   * Een eigenaar van uw GitHub-organisatie moet de toepassing installeren die zich bevindt op `https://github.com/apps/cloud-manager-for-aem` en toegang verlenen tot de gegevensopslagruimte.
   * Gelieve te verwijzen naar de documentatie van GitHub voor details over hoe dit wordt gedaan.

1. Om de beveiliging te verbeteren, moet u een geheim bestand maken in de standaardvertakking van uw opslagplaats. Tik of klik op **Genereren**.

1. Bevestig het genereren van het geheime bestand door te tikken of te klikken **Bevestigen**.

   ![Bevestig geheime generatie](/help/assets/repositories/confirm-generation.png)

1. Terug in de **Eigendom van privéopslagplaats valideren** venster heeft Cloud Manager de inhoud van het privébestand gegenereerd in het dialoogvenster **Beveiligde bestandsinhoud** veld. Kopieer de inhoud van dat veld.

   * De inhoud van het geheime bestand wordt slechts eenmaal weergegeven. Als u de inhoud niet kopieert voordat u dit venster sluit, moet u het geheim opnieuw genereren.

   ![Inhoud van geheim bestand kopiëren](/help/assets/repositories/new-secret.png)

1. Creeer een nieuw dossier in de standaardtak van uw geroepen reactie GitHub `.well-known/adobe/cloud-manager-challenge` en plak de geheime dossierinhoud in dat dossier en bewaar.

1. Zodra de app is geïnstalleerd en het geheime bestand in de opslagplaats aanwezig is, kunt u tikken of op **Valideren** in de **Eigendom van privéopslagplaats valideren** in.

De app kan worden geïnstalleerd en een geheim bestand kan in elke willekeurige volgorde worden gemaakt. Beide stappen moeten echter worden uitgevoerd voordat u de validatie kunt uitvoeren.

Tot de validatie wordt de repository weergegeven met een rood pictogram dat aangeeft dat deze nog niet is gevalideerd en nog niet kan worden gebruikt.

![Niet-gevalideerde repo](/help/assets/repositories/unvalidated-repo.png)

Let erop dat de **Type** kolom identificeert gemakkelijk door Adobe verschafte opslagplaatsen (**Adobe**) en uw eigen GitHub-opslagplaatsen (**GitHub**).

Als u op een latere datum naar de opslagplaats moet terugkeren om de validatie te voltooien, gaat u naar de **Opslagplaatsen** pagina, tik of klik de ellipsknoop in de rij die de bewaarplaats vertegenwoordigt GitHub u enkel toevoegde en selecteert **Eigenaarsvalidatie** in het keuzemenu.

## Uw eigen GitHub-opslagplaatsen gebruiken met Cloud Manager {#using}

Nadat de gegevensopslagplaats GitHub in de Manager van de Wolk wordt bevestigd wordt de integratie voltooid en u kunt de bewaarplaats met de Manager van de Wolk gebruiken.

1. Wanneer u een trekkingsverzoek creeert, zal een controle GitHub automatisch beginnen.

   ![GitHub-controles](/help/assets/repositories/github-checks.png)

1. Voor elk trekkingsverzoek wordt een [volledige stackcodekwaliteitpijplijn](/help/using/managing-pipelines.md) wordt automatisch gemaakt. Deze pijpleiding is begonnen bij elke update van het trekkingsverzoek.

1. De controle GitHub blijft in een lopende staat tot de controles van de codekwaliteit volledig. De resultaten van de codekwaliteit zullen dan aan de controle worden verspreid GitHub.

   ![GitHub-kwaliteitscontroles](/help/assets/repositories/github-code-quality.png)

Wanneer het trekkingsverzoek wordt gesloten of samengevoegd, wordt de volledige pijpleiding van de kwaliteit van de stapelcode gecreeerd automatisch geschrapt.

## Beperkingen {#limitations}

Houd rekening met de volgende beperkingen wanneer u uw eigen GitHub-opslagruimten gebruikt met Cloud Manager.

* U kunt niet de bewaarplaatsen GitHub als directe bewaarplaatsbron voor de pijpleidingen gebruiken u beheert.
   * Deze functionaliteit is gepland.
* U kunt niet de bevestiging van het trekkingsverzoek pauzeren gebruikend de controle GitHub van wolkenmanager.
   * Als de gegevensopslagplaats GitHub in de Manager van de Wolk wordt bevestigd, zal de Manager van de Wolk altijd proberen om de trekkingsverzoeken te bevestigen die voor die bewaarplaats worden gecreeerd.
Als de Adobe GitHub app wordt verwijderd uit uw organisatie GitHb, zal dit de trekrekverzoekbevestigingseigenschap voor alle bewaarplaatsen verwijderen.
