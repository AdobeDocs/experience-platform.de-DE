---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Reservierung;Unterkunft;
title: Schemafeldgruppe für die Unterkunftsreservierung
description: Erfahren Sie mehr über die Schemafeldgruppe „Unterkunftsreservierung“.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# [!UICONTROL Unterkunftsreservierung] Schemafeldgruppe

[!UICONTROL Unterkunftsreservierung] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM ExperienceEvent] , &#x200B;](../../classes/experienceevent.md) verwendet wird, um Informationen zu einer Unterkunftsreservierung zu erfassen.

Die Feldergruppe ist eine Erweiterung der Feldergruppe [!UICONTROL Reservierungsdetails] und enthält alle gleichen Felder unter einem einzigen Feld vom Typ „Objekt“, `reservations`. Zusätzlich zu diesen allgemeinen Feldern enthält [!UICONTROL Unterkunftsreservierung] auch `lodgingReservations` Array. Dieses Array von Objekten wird verwendet, um eine oder mehrere Reservierungen mit für die Unterkunft eindeutigen Eigenschaften zu beschreiben.

>[!NOTE]
>
>In diesem Dokument werden die Details des `lodgingReservations`-Arrays behandelt. Informationen zu den anderen Feldern, die unter dem `reservations` Objekt bereitgestellt werden, finden Sie in der [[!UICONTROL Reservierungsdetails] Feldergruppenreferenz](./reservation-details.md).

![Struktur der &#x200B;](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` ist ein Array von Objekten, das eine Liste der Unterkunftsreservierungen darstellt. Wenn ein Reservierungsereignis beispielsweise Reservierungen in mehreren verschiedenen Hotels entlang der Route einer Reise umfasst, können diese Reservierungen als einzelne Objekte unter `lodgingReservations` für ein einzelnes Ereignis aufgeführt werden.

Die Struktur der einzelnen -Objekte, die unter `lodgingReservations` bereitgestellt werden, wird unten angezeigt.

![lodgingReservations-Struktur](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der durchschnittliche Tagespreis des Hotelzimmers. |
| `lodgingCheckIn` | Objekt | Ein Objekt, das Details zum Einchecken in einer Unterkunft beschreibt. Enthält die folgenden Werte:<ul><li>`digitalKey`: (Ganzzahl) Gibt an, wenn ein Gast beim Einchecken die Verwendung eines digitalen Schlüssels auswählt.</li><li>`earlyCheckInRequested`: (Ganzzahl) Gibt an, wenn ein Gast anfordert, früher als die normalen Check-in-Zeiten einzuchecken.</li><li>`lateCheckInRequested`: (Ganzzahl) Gibt an, wenn ein Gast anfordert, später als die normalen Check-in-Zeiten einzuchecken.</li><li>`noRoomCheckIn`: (Ganzzahl) Dieser Wert wird erfasst, wenn ein Gast das Einchecken abschließt, wenn zu diesem Zeitpunkt keine Zimmer verfügbar sind.</li><li>`oneRoomCheckIn`: (Ganzzahl) Dieser Wert wird erfasst, wenn ein Gast das Einchecken abschließt, wenn zu diesem Zeitpunkt nur ein Zimmer verfügbar ist.</li><li>`roomKeys`: (Integer) Die Anzahl der beim Check-in bereitgestellten Standard-Zimmerschlüssel.</li><li>`userSelectedRoom`: (Boolesch) Gibt an, ob der Gast sein Zimmer beim Einchecken ausgewählt hat.</li></ul> |
| `rackrate` | [[!UICONTROL Währung]](../../data-types/currency.md) | Die Kosten für eine Reservierung am selben Tag ohne vorherige Buchungsvereinbarungen. |
| `ID` | String | Die Reservierungsnummer oder -kennung. |
| `agentID` | String | Die Agent-ID, die mit der Hotelbuchung verknüpft ist. |
| `basePrice` | String | Der Grundpreis vor Abzug aller Rabatte. |
| `bookingID` | String | Die mit der Hotelbuchung verknüpfte Buchungs-ID. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung storniert wurde. |
| `checkInDate` | DateTime | Das Eincheckdatum für die Zimmerreservierung. |
| `checkOutDate` | DateTime | Das Check-out-Datum für die Zimmerreservierung. |
| `confirmationNumber` | String | Die Nummer oder Kennung der Reservierungsbestätigung. |
| `couponCode` | String | Ein Couponcode, der mit der Hotelbuchung verknüpft ist. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `currencyCode` | String | Der ISO 4217-Währungscode, der für den Kauf verwendet wurde. |
| `discountPercent` | Double | Der mit der Buchung verknüpfte Rabattprozentsatz. |
| `freeCancelation` | Boolesch | Gibt an, ob das Zimmer über eine kostenlose Stornierungsrichtlinie verfügt. |
| `guestID` | String | Die Gäste-ID, die mit der Hotelbuchung verknüpft ist. |
| `length` | Ganzzahl | Die Gesamtzahl der Tage für die Reservierung. |
| `loyaltyID` | String | Die ID des Treueprogramms für den in der Reservierung aufgeführten Gast. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der Kinder, die mit der Reservierung verknüpft sind. |
| `numberOfRooms` | Ganzzahl | Die Anzahl der Zimmer, die mit der Reservierung verbunden sind. |
| `propertyID` | String | Eine Kennung des Hotels oder Resorts für die Reservierung. |
| `propertyName` | String | Der Name des Hotels oder Resorts für die Reservierung. |
| `purpose` | String | Der Zweck der Reservierung, in der Regel entweder geschäftlich oder privat. |
| `ratePlan` | String | Das Tarifangebot, zu dem das Zimmer verkauft wurde. |
| `refundable` | Boolesch | Gibt an, ob das Zimmer erstattungsfähig ist. |
| `reservationStatus` | String | Der Status der Reservierung. |
| `roomAccessibilityType` | String | Die Art der Barrierefreiheit des Raums, z. B. Mobilität, Gehör oder andere. |
| `roomCapacity` | Ganzzahl | Die Anzahl der Personen im Hotelzimmer. |
| `roomType` | String | Die Art des zu reservierenden Zimmers. |
| `smoking` | Boolesch | Zeigt an, ob das Rauchen im Zimmer erlaubt ist. |
| `tripType` | String | Gibt an, ob die Reservierung für eine einfache Fahrt, eine Hin- und Rückfahrt oder eine Reise mit mehreren Städten gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
