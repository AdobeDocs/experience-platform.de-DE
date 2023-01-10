---
solution: Experience Platform
title: Datenmodell der Finanzdienstleistungsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (ERD) an, in dem ein standardisiertes Datenmodell für die Bank-, Finanz- und Versicherungsbranche (BFSI) beschrieben wird. Dieses Datenmodell ist mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 11%

---

# [!UICONTROL Finanzdienstleistungen] Branchendatenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für den Banken-, Finanz- und Versicherungssektor (BFSI) dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Art und Weise, wie Daten in Adobe Experience Platform gespeichert werden, präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Siehe Handbücher zur Verwaltung [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche für weitere Informationen.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einem zugrunde liegenden [Experience-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität jede Zeile, die in **fett** stellt eine Feldergruppe oder einen Datentyp mit den entsprechenden Feldern dar, die unten im unfetteten Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![](../../images/industries/financial.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält ein Feld &quot;_ID&quot;, das die eindeutige Kennung (`_id`), das von der XDM ExperienceEvent-Klasse bereitgestellt wird. Siehe Referenzdokument unter [XDM ExperienceEvent](../../classes/experienceevent.md) für weitere Details darüber, was für diesen Wert erwartet wird.

## [!UICONTROL Finanzdienstleistungen] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige finanzielle Anwendungsfälle aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Personalisierung für bevorzugte Segmente im Maßstab durch Omnichannel-Reporting-Einblicke und die Automatisierung von Journey, um die Registrierung zu einem bevorzugten Prämienprogramm zu verbessern. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Anführungsanfragedetails]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Einlagendetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Bilanzübertragungen]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimieren Sie die kanalübergreifende Personalisierung über Online- und Offline-Kanäle hinweg. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| treiben Sie neue Umsatzmöglichkeiten, indem Sie Einblicke aus der kanalübergreifenden Verhaltensanalyse nutzen und Muster der Produktnutzung identifizieren, die zu neuen Produktangeboten führen könnten. | <ul><li>**[[!UICONTROL Richtlinie]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Support Site Search]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Einlagendetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
