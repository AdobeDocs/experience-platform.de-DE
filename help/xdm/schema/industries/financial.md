---
solution: Experience Platform
title: Datenmodell der Finanzdienstleistungsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (ERD) an, in dem ein standardisiertes Datenmodell für die Bank-, Finanz- und Versicherungsbranche (BFSI) beschrieben wird. Dieses Datenmodell ist mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# [!UICONTROL Finanzdienstleistungen] Industriedatenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für den Banken-, Finanz- und Versicherungssektor (BFSI) dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Speicherung von Daten in Adobe Experience Platform präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Erlebnis-Datenmodell (XDM)-Klasse](../composition.md#class).
* Die unter einem übergeordneten Feld eingerückten Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![Ein Beispiel-ERD für ein Datenmodell der Finanzbranche](../../images/industries/financial.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält das Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

## Anwendungsfälle für [!UICONTROL Finanzdienstleistungen]

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige finanzielle Anwendungsfälle aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Personalisierung für bevorzugte Segmente im Maßstab durch Omnichannel-Reporting-Einblicke und die Automatisierung von Journey, um die Registrierung zu einem bevorzugten Prämienprogramm zu verbessern. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Anforderungsdetails zitieren]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Einlagendetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Bilanzübertragungen]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Details zum Treueprogramm]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimierung der kanalübergreifenden Personalisierung über Online- und Offline-Kanäle hinweg. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Details zum Treueprogramm]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| treiben Sie neue Umsatzmöglichkeiten, indem Sie Einblicke aus der kanalübergreifenden Verhaltensanalyse nutzen und Muster der Produktnutzung identifizieren, die zu neuen Produktangeboten führen könnten. | <ul><li>**[[!UICONTROL Richtlinie]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Unterstützung der Site-Suche]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Einlagendetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdetails]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Details zum Treueprogramm]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
