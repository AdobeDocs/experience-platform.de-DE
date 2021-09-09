---
solution: Experience Platform
title: Datenmodell für die Reise- und Gastgewerbe
topic-legacy: overview
description: Zeigen Sie ein Entitätsbeziehungsdiagramm (ERD) an, das ein standardisiertes Datenmodell für die Reise- und Gastgewerbe beschreibt, das mit dem Experience-Datenmodell (XDM) für die Verwendung in Adobe Experience Platform kompatibel ist.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL Datenmodell für die Reise- und ] Gastgewerbe ERD

Das folgende Entitätsbeziehungsdiagramm (ERD) stellt ein standardisiertes Datenmodell für die Reise- und Gastgewerbe dar. Der ERD wird absichtlich denormalisiert und unter Berücksichtigung der Art und Weise, wie Daten in Adobe Experience Platform gespeichert werden, präsentiert.

>[!NOTE]
>
>Der ERD wie beschrieben ist eine Empfehlung, wie Sie Ihre Daten für diesen branchenspezifischen Anwendungsfall modellieren sollten. Um dieses Datenmodell in Platform nutzen zu können, müssen Sie die empfohlenen Schemas und deren Beziehungen selbst erstellen. Weitere Informationen finden Sie in den Handbüchern zum Verwalten von [Schemas](../../ui/resources/schemas.md) und [Beziehungen](../../tutorials/relationship-ui.md) in der Benutzeroberfläche.

Verwenden Sie die folgende Legende, um diese ERD zu interpretieren:

* Jede in angezeigte Entität basiert auf einer zugrunde liegenden [Experience-Datenmodell (XDM)-Klasse](../composition.md#class).
* Für eine bestimmte Entität steht jede in **bold** markierte Zeile für eine Feldergruppe oder einen Datentyp mit den entsprechenden Feldern, die unten in unfettetem Text aufgeführt sind.
* Die wichtigsten Felder für eine bestimmte Entität sind rot hervorgehoben.
* Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;markiert ist.
* Entitätsbeziehungen werden als nicht abhängig markiert, da Cookie-basierte Ereignisse häufig nicht die Person oder Person bestimmen können, die die Transaktion getätigt hat.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>Die Entität &quot;Erlebnisereignis&quot;enthält ein Feld &quot;_ID&quot;, das das von der XDM ExperienceEvent-Klasse bereitgestellte Attribut für die eindeutige Kennung (`_id`) darstellt. Weitere Informationen dazu, was für diesen Wert erwartet wird, finden Sie im Referenzdokument zu [XDM ExperienceEvent](../../classes/experienceevent.md) .

## [!UICONTROL Anwendungsfälle für Reise- und ] Gastgewerbe

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle für die Reise- und Gastgewerbe aufgeführt.

| Anwendungsfall | Empfohlene Klassen und Feldergruppen |
| --- | --- |
| Gastfreundschaft und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Buchungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li><li>[Speisereservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktangaben](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktangaben für Arbeitskontakte](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Gastfreundschaft und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Buchungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Speisereservierung](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktangaben](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktangaben für Arbeitskontakte](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotel und andere Anziehungsmöglichkeiten für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Buchungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Unterkunftsreservierung](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktangaben](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktangaben für Arbeitskontakte](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Up-Sell-Flug und andere lokale Attraktionen für Gäste und Gäste mit bevorstehender Hotelreservierung. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Buchungsdetails](../../field-groups/event/reservation-details.md)</li><li>[Flugreservierung](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Demografische Details](../../field-groups/profile/demographic-details.md)</li><li>[Persönliche Kontaktangaben](../../field-groups/profile/personal-contact-details.md)</li><li>[Kontaktangaben für Arbeitskontakte](../../field-groups/profile/work-contact-details.md)</li><li>[Treuedetails](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
