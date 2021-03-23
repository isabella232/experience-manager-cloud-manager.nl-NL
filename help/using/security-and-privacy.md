---
title: Beveiliging en privacy
seo-title: Beveiliging en privacy voor AEM Cloud Manager
description: Volg deze pagina voor meer informatie over de beveiliging en privacy van uw elementen (code/artefacten).
seo-description: Volg deze pagina voor meer informatie over de beveiliging en privacy van uw elementen (code/artefacten) met AEM Cloud Manager.
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: Aan de slag
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Beveiliging en privacy {#security-and-privacy}

[!UICONTROL Cloud Manager] heeft pre-gevormde rollen met aangewezen toestemmingen. In deze sectie worden de beveiliging en privacy van uw elementen (code/artefacten) gemarkeerd met AEM Cloud Manager. Bovendien [!UICONTROL Cloud Manager] heeft pre-gevormde rollen met aangewezen toestemmingen.

Om over de mogelijke rollen te leren u in de Admin Console en gebruikersroltoestemmingen kunt toewijzen, verwijs naar [Op rol gebaseerde Toestemmingen](/help/using/role-based-permissions.md).


## Bronisolatie {#resource-isolation}

Klanten die [!UICONTROL Cloud Manager] gebruiken, hebben hun IMS-referenties nodig om te worden geverifieerd, aangezien alle machtigingen die aan [!UICONTROL Cloud Manager] zijn gekoppeld, worden geconfigureerd en gekoppeld aan hun IMS-organisatie. Tijdens het aan boord gaan proces, zorgt het provisioningteam ervoor dat de middelisolatie in [!UICONTROL Cloud Manager] wordt afgedwongen.

## Gegevensbeveiliging {#data-security}

De code in [!UICONTROL Cloud Manager] wordt gecodeerd in transit. Binaire bestanden die in Cloud Manager worden gemaakt, worden ook tijdens de opslag versleuteld en versleuteld.

Elke klant krijgt zijn eigen **Git Repository** en zijn code is veilig en wordt niet gedeeld met andere **Organisaties**.

## Gegevensprivacy {#data-privacy}

[!UICONTROL Cloud Manager] zich houdt aan de privacybeginselen die door Adobe zijn gedefinieerd. Ontwikkelaars drukken code veilig in de **Git Repository** via HTTPS.

De gebruikersinterface (UI) voor [!UICONTROL Cloud Manager] wordt gebouwd bovenop de diensten die aan een gemeenschappelijk controlekader voldoen dat door Adobe wordt bepaald. Gebruikersinterface voor [!UICONTROL Cloud Manager] gebruikt beveiligde services van verschillende cloudproviders.
