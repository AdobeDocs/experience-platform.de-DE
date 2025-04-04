---
solution: Experience Platform
title: Datenmodell ERD der Reise- und Gastgewerbebranche
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) an, das ein standardisiertes Datenmodell für die Reise- und Gastgewerbebranche beschreibt, das mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# [!UICONTROL Reisen und Gastgewerbe] Datenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) stellt ein standardisiertes Datenmodell für die Reise- und Gastgewerbebranche dar. Das ERD wird absichtlich auf entnormierte Weise und unter Berücksichtigung der Art und Weise präsentiert, wie Daten in Adobe Experience Platform gespeichert werden.

>[!NOTE]
>
>Das ERD wie beschrieben ist eine Empfehlung dafür, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Experience Platform verwenden zu können, müssen Sie die empfohlenen Schemata und ihre Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zur Verwaltung [Schemata](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Folgende Legende verwenden, um dieses ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-](../composition.md#class).
* Unter einem übergeordneten Feld eingerückte Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kundinnen und Kunden verwendet werden können, werden als „Identität“ gekennzeichnet, wobei eine dieser Eigenschaften als „primäre Identität“ markiert ist.
* Entitätsbeziehungen werden als nicht abhängig gekennzeichnet, da Cookie-basierte Ereignisse häufig nicht die Person oder Einzelperson bestimmen können, die die Transaktion durchgeführt hat.

![Ein Beispiel-ERD für ein Reisegesellschaftsdatenmodell](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>Die Erlebnisereignisentität enthält ein Feld „_ID“, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für [ Wert erwartet wird, finden Sie ](../../classes/experienceevent.md) Referenzdokument unter XDM ExperienceEvent .

## [!UICONTROL Reisen und Gastgewerbe] Anwendungsfälle

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige Anwendungsfälle für die Reise- und Gastgewerbebranche aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Crosssell-Restaurants und andere Attraktionen für Besucher des Marktes und Gäste mit bevorstehenden Hotelreservierungen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li><li>[Restaurantreservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdaten](../../field-groups/profile/personal-contact-details.md)</li><li>[Details zum Arbeitskontakt](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Upsell-Restaurants und andere Attraktionen für Gäste des Marktes und Gäste mit bevorstehenden Hotelreservierungen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Restaurantreservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdaten](../../field-groups/profile/personal-contact-details.md)</li><li>[Details zum Arbeitskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Upsell-Hotel und andere residente Attraktionen für Gäste im Markt und Gäste mit bevorstehenden Hotelreservierungen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdaten](../../field-groups/profile/personal-contact-details.md)</li><li>[Details zum Arbeitskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Up-Sell-Flug und andere Attraktionen für Besucher des Marktes und Gäste mit bevorstehenden Hotelreservierungen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Flugreservierung](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdaten](../../field-groups/profile/personal-contact-details.md)</li><li>[Details zum Arbeitskontakt](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
