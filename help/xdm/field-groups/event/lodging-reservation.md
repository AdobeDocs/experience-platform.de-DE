---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Unterbringung;
title: Feldergruppe "Reservierungsschema"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe "Reservierungsschema".
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 7%

---

# [!UICONTROL Unterkunftsreservierung] Schemafeldgruppe

[!UICONTROL Unterkunftsreservierung] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) verwendet, um Informationen über eine Reservierung zu erfassen.

Die Feldergruppe ist eine Erweiterung der [!UICONTROL Buchungsdetails] Feldergruppe und enthält alle gleichen Felder unter einem Feld vom Typ &quot;Objekt&quot;, `reservations`. Zusätzlich zu diesen allgemeinen Feldern [!UICONTROL Unterkunftsreservierung] auch `lodgingReservations` Array. Dieses Objekt dient zur Beschreibung einer oder mehrerer Reservierungen mit Eigenschaften, die für die Unterkunft eindeutig sind.

>[!NOTE]
>
>In diesem Dokument werden die Details der `lodgingReservations` Array. Für Informationen über die anderen Felder, die im `reservations` -Objekt, siehe [[!UICONTROL Buchungsdetails] Feldergruppenreferenz](./reservation-details.md).

![Buchungsstruktur](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` ist eine Gruppe von Objekten, die eine Liste von Reservierungen für Unterkünfte darstellen. Wenn ein Reservierungsereignis Reservierungen in mehreren Hotels entlang der Route einer Reise beinhaltet, können diese Reservierungen beispielsweise als einzelne Objekte unter `lodgingReservations` für ein einzelnes Ereignis.

Die Struktur der einzelnen Objekte, die unter `lodgingReservations` ist unten angegeben.

![lodgingReservations structure](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der durchschnittliche Tagespreis des Hotelzimmers. |
| `lodgingCheckIn` | Objekt | Ein Objekt, das die Unterbringung von Check-in-Details beschreibt. Umfasst die folgenden Werte:<ul><li>`digitalKey`: (Ganzzahl) Gibt an, wann ein Gast beim Einchecken die Verwendung eines digitalen Schlüssels auswählt.</li><li>`earlyCheckInRequested`: (Ganzzahl) Gibt an, wann ein Gast vor dem normalen Einchecken einen Check-in anfordert.</li><li>`lateCheckInRequested`: (Ganzzahl) Gibt an, wann ein Gast einen Check-in zu einem späteren Zeitpunkt als zu den normalen Check-in-Stunden anfordert.</li><li>`noRoomCheckIn`: (Ganzzahl) Dieser Wert wird erfasst, wenn ein Gast die Anmeldung abschließt, wenn zu diesem Zeitpunkt keine Zimmer verfügbar sind.</li><li>`oneRoomCheckIn`: (Ganzzahl) Dieser Wert wird erfasst, wenn ein Gast die Anmeldung abgeschlossen hat, wenn zu diesem Zeitpunkt nur ein Zimmer verfügbar ist.</li><li>`roomKeys`: (Ganzzahl) Die Anzahl der Standard-Zimmerschlüssel, die beim Check-in bereitgestellt werden.</li><li>`userSelectedRoom`: (Boolesch) Gibt an, ob der Gast beim Einchecken sein Zimmer ausgewählt hat.</li></ul> |
| `rackrate` | [[!UICONTROL Währung]](../../data-types/currency.md) | Die Kosten für eine Buchung am selben Tag ohne vorherige Reservierung. |
| `ID` | Zeichenfolge | Die Reservierungsnummer oder -kennung. |
| `agentID` | Zeichenfolge | Die mit der Hotelbuchung verknüpfte Agenten-ID. |
| `basePrice` | Zeichenfolge | Der Basispreis vor Rabatten wird hinzugefügt. |
| `bookingID` | Zeichenfolge | Die mit der Hotelbuchung verbundene Buchungskennung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung abgebrochen wurde. |
| `checkInDate` | DateTime | Das Check-in Datum für die Zimmerreservierung. |
| `checkOutDate` | DateTime | Das Datum des Auscheckens für die Zimmerreservierung. |
| `confirmationNumber` | Zeichenfolge | Die Reservierungsbestätigungsnummer oder -kennung. |
| `couponCode` | Zeichenfolge | Gutscheincode für die Hotelbuchung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für den Kauf verwendet wird. |
| `discountPercent` | Double | Der mit der Buchung verbundene Rabattprozentsatz. |
| `freeCancelation` | Boolesch | Gibt an, ob das Zimmer kostenfrei storniert werden kann. |
| `guestID` | Zeichenfolge | Die mit der Hotelbuchung verknüpfte Gast-ID. |
| `length` | Ganzzahl | Die Gesamtanzahl der Tage für die Reservierung. |
| `loyaltyID` | Zeichenfolge | Die Kennung des Treueprogramms für den in der Reservierung aufgelisteten Gast. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `numberOfRooms` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Zimmer. |
| `propertyID` | Zeichenfolge | Kennung des Hotels oder Resorts für die Reservierung. |
| `propertyName` | Zeichenfolge | Der Name des Hotels oder Resorts für die Reservierung. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `ratePlan` | Zeichenfolge | Der Preis, auf den das Zimmer verkauft wurde. |
| `refundable` | Boolesch | Gibt an, ob das Zimmer erstattbar ist. |
| `reservationStatus` | Zeichenfolge | Der Status der Reservierung. |
| `roomAccessibilityType` | Zeichenfolge | Der Barrierefreiheitstyp des Raums, z. B. Mobilität, Anhörung oder andere. |
| `roomCapacity` | Ganzzahl | Die Anzahl der Personen im Hotelzimmer. |
| `roomType` | Zeichenfolge | Die Art des reservierten Zimmers. |
| `smoking` | Boolesch | Gibt an, ob das Rauchen in dem Zimmer erlaubt ist. |
| `tripType` | Zeichenfolge | Gibt an, ob die Reservierung für eine Einweg-, Hin- und Rückfahrt oder für eine mehrstündige Reise gilt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
