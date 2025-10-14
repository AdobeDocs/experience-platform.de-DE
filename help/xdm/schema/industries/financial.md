---
solution: Experience Platform
title: Datenmodell ERD der Finanzdienstleistungsbranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) an, das ein standardisiertes Datenmodell für die Banken-, Finanz- und Versicherungsbranche (BFSI) beschreibt. Dieses Datenmodell ist mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---

# [!UICONTROL Finanzdienstleistungen] Datenmodell ERD der Branche

Das folgende Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) stellt ein standardisiertes Datenmodell für die Banken-, Finanz- und Versicherungsbranche (BFSI) dar. Das ERD wird absichtlich auf entnormierte Weise und unter Berücksichtigung der Art und Weise präsentiert, wie Daten in Adobe Experience Platform gespeichert werden.

>[!NOTE]
>
>Das ERD wie beschrieben ist eine Empfehlung dafür, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Experience Platform verwenden zu können, müssen Sie die empfohlenen Schemata und ihre Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zur Verwaltung [Schemata](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Folgende Legende verwenden, um dieses ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-](../composition.md#class).
* Unter einem übergeordneten Feld eingerückte Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kundinnen und Kunden verwendet werden können, werden als „Identität“ gekennzeichnet, wobei eine dieser Eigenschaften als „primäre Identität“ markiert ist.
* Entitätsbeziehungen werden als nicht abhängig gekennzeichnet, da Cookie-basierte Ereignisse häufig nicht die Person oder Einzelperson bestimmen können, die die Transaktion durchgeführt hat.

![Ein Beispiel für ein ERD für ein Datenmodell der Finanzbranche](../../images/industries/financial.png)

>[!NOTE]
>
>Die Erlebnisereignisentität enthält ein Feld „_ID“, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für [&#x200B; Wert erwartet wird, finden Sie &#x200B;](../../classes/experienceevent.md) Referenzdokument unter XDM ExperienceEvent .

## [!UICONTROL Finanzdienstleistungen] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige finanzielle Anwendungsfälle aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Personalisierung in jedem Maßstab für bevorzugte Segmente durch Omni-Channel-Reporting-Insights und Automatisierung von Journey, um die Registrierung für ein bevorzugtes Prämienprogramm zu erhöhen. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Details zur Angebotsanfrage]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Einzahlungsdetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Saldoübertragungen]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimieren Sie die kanalübergreifende Personalisierung über Online- und Offline-Kanäle. | <ul><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Fördern Sie neue Umsatzmöglichkeiten, indem Sie Einblicke aus der kanalübergreifenden Verhaltensanalyse nutzen und Muster der Produktnutzung identifizieren, die zu neuen Produktangeboten führen könnten. | <ul><li>**[[!UICONTROL Richtlinie]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produkt]](../../classes/product.md)**:<ul><li>[[!UICONTROL Produktkategorie]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Kartenaktionen]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Support-Site-Suche]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Einzahlungsdetails]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Kanaldetails]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demografische Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Persönliche Kontaktdaten]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Treuedetails]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
