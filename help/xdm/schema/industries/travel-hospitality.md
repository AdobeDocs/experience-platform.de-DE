---
solution: Experience Platform
title: Datenmodell für die Reise- und Gastgewerbe
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (ERD) an, das ein standardisiertes Datenmodell für die Reise- und Gastgewerbe beschreibt, das mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---

# [!UICONTROL Reise- und Gastgewerbe] Branchendatenmodell ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Reise- und Gastgewerbe dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Speicherung von Daten in Adobe Experience Platform präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Erlebnis-Datenmodell (XDM)-Klasse](../composition.md#class).
* Die unter einem übergeordneten Feld eingerückten Felder stellen ein untergeordnetes Feld oder Unterfeld dar, das zur Feldergruppe des übergeordneten Felds gehört.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![Ein Beispiel-ERD für ein Datenmodell für Reisegastfreundlichkeit](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält das Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

## Anwendungsfälle für [!UICONTROL Reise und Gastfreundschaft]

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle für die Reise- und Gastgewerbe aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Gastfreundschaft und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li><li>[Restaurantreservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdetails](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktdetails für die Arbeit](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Gastfreundschaft und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Restaurantreservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdetails](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktdetails für die Arbeit](../../field-groups/profile/work-contact-details.md)</li><li>[Details zum Treueprogramm](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotel und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdetails](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktdetails für die Arbeit](../../field-groups/profile/work-contact-details.md)</li><li>[Details zum Treueprogramm](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Up-Sell-Flug und andere lokale Attraktionen für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reservierungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Flugreservierung](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktdetails](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktdetails für die Arbeit](../../field-groups/profile/work-contact-details.md)</li><li>[Details zum Treueprogramm](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
