---
title: De wizard Nieuw project gebruiken
description: Volg deze pagina om te leren hoe u de wizard kunt gebruiken om een AEM Application Project te maken
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: cb791a4f148ba394687b5e824b75fe1386d83c18
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# De wizard Nieuw project gebruiken {#using-the-wizard}

Als u als nieuwe klant aan Cloud Manager wordt toegevoegd, ontvangt u een lege opslagplaats voor it. Om u te helpen aan de slag te gaan, biedt Cloud Manager een wizard om een minimaal AEM project te maken op basis van de [Projectarchetype AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) als uitgangspunt.

Voer de volgende stappen uit om een AEM project te maken met de wizard.

1. Aanmelden bij Cloud Manager [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) en selecteert u de gewenste organisatie.

1. Als u dat nog niet hebt gedaan, [maakt u uw programma.](program-setup.md) Als het programma eenmaal is gemaakt, herkent Cloud Manager dat de opslagruimten nog niet zijn ingesteld en wordt op de **Overzicht** scherm.

   ![Project CTA maken](/help/assets/image2018-10-3_14-29-44.png)

1. Klikken **Maken** om de wizard te starten en belangrijke waarden op te geven.

   * **Titel** - Dit is de titel van het project en wordt standaard ingesteld op de naam van het programma.
   * **Nieuwe naam vertakking** - Dit is de eerste vertakking van uw it-opslagplaatsen en deze wordt standaard `main`.

   ![Projectwaarden](/help/assets/screen_shot_2018-10-08at55825am.png)

1. Het dialoogvenster heeft een lade die kan worden geopend door op de handgreep naar de onderkant te klikken. In zijn uitgebreide vorm, toont de dialoog alle configuratieparameters voor het AEM project archetype. Deze parameters hebben standaardwaarden die worden gegenereerd op basis van de **Titel** hebt u al opgegeven en hoeft u niets te wijzigen. Ze worden hier uitgelegd voor uw informatie.

   ![Gedetailleerde parameters voor archetype](/help/assets/screen_shot_2018-10-08at60032am.png)

1. Klikken **Maken** om het starterproject tot stand te brengen door archetype te gebruiken en aan de genoemde git tak vast te leggen.

U hebt nu een basisproject! Nu kun je je pijpleidingen opzetten.

## Bestaande of migrerende klanten {#existing-migrating}

Als u een huidige klant van Adobe Managed Services (AMS) of een klant op locatie AEM die naar migreert, hebt u waarschijnlijk al projectcode in git of een ander versiecontrolesysteem.

In dergelijke gevallen importeert u uw project in de git-opslagplaats van Cloud Manager.
