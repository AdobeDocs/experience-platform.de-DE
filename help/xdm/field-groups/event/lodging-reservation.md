---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Unterbringung;
title: Feldergruppe "Reservierungsschema"
description: Erfahren Sie mehr über die Feldergruppe "Reservierungsschema".
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# [!UICONTROL Reservierungsreservierung] Schemafeldgruppe

[!UICONTROL Reservierung unterbringen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die zum Erfassen von Informationen zu einer Reservierung verwendet wird.

Die Feldergruppe ist eine Erweiterung der Feldergruppe [!UICONTROL Reservierungsdetails] und enthält alle gleichen Felder unter einem einzigen Feld vom Typ &quot;Objekt&quot;, `reservations`. Zusätzlich zu diesen generischen Feldern enthält [!UICONTROL Reservierung unterbringen] auch das Array `lodgingReservations` . Dieses Objekt dient zur Beschreibung einer oder mehrerer Reservierungen mit Eigenschaften, die für die Unterkunft eindeutig sind.

>[!NOTE]
>
>In diesem Dokument werden die Details des `lodgingReservations` -Arrays behandelt. Informationen zu den anderen Feldern, die unter dem Objekt `reservations` bereitgestellt werden, finden Sie in der Feldgruppenreferenz [[!UICONTROL Reservierungsdetails] ](./reservation-details.md).

![Reservierungsstruktur unterbringen](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` ist ein Array von Objekten, die eine Liste von Reservierungen für Unterkünfte darstellen. Wenn eine Reservierung mehrere verschiedene Hotels entlang der Route einer Reise beinhaltet, können diese Reservierungen beispielsweise als einzelne Objekte unter `lodgingReservations` für eine einzelne Veranstaltung aufgeführt werden.

Die Struktur der einzelnen Objekte, die unter &quot;`lodgingReservations`&quot;bereitgestellt werden, ist unten aufgeführt.

![lodgingReservations structure](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der durchschnittliche Tagespreis des Hotelzimmers. |
| `lodgingCheckIn` | Objekt | Ein Objekt, das die Unterbringung von Check-in-Details beschreibt. Umfasst die folgenden Werte:<ul><li>`digitalKey`: (Integer) Gibt an, wann ein Gast beim Einchecken die Verwendung eines digitalen Schlüssels auswählt.</li><li>`earlyCheckInRequested`: (Integer) Gibt an, wann ein Gast vor den normalen Eincheckzeiten einen Check-in anfordert.</li><li>`lateCheckInRequested`: (Integer) Gibt an, wann ein Gast einen Check-in zu einem späteren Zeitpunkt als zu den normalen Check-in-Stunden anfordert.</li><li>`noRoomCheckIn`: (Integer) Dieser Wert wird erfasst, wenn ein Gast die Anmeldung abgeschlossen hat, wenn zu diesem Zeitpunkt keine Zimmer verfügbar sind.</li><li>`oneRoomCheckIn`: (Integer) Dieser Wert wird erfasst, wenn ein Gast die Anmeldung abgeschlossen hat, wenn zu diesem Zeitpunkt nur ein Zimmer verfügbar ist.</li><li>`roomKeys`: (Integer) Die Anzahl der Standard-Zimmerschlüssel, die beim Check-in bereitgestellt werden.</li><li>`userSelectedRoom`: (Boolesch) Gibt an, ob der Gast beim Einchecken sein Zimmer ausgewählt hat.</li></ul> |
| `rackrate` | [[!UICONTROL Währung]](../../data-types/currency.md) | Die Kosten für eine Buchung am selben Tag ohne vorherige Reservierung. |
| `ID` | Zeichenfolge | Die Reservierungsnummer oder -kennung. |
| `agentID` | Zeichenfolge | Die mit der Hotelbuchung verknüpfte Agenten-ID. |
| `basePrice` | Zeichenfolge | Der Basispreis vor Rabatten wird hinzugefügt. |
| `bookingID` | Zeichenfolge | Die mit der Hotelbuchung verknüpfte Buchungskennung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung abgebrochen wurde. |
| `checkInDate` | DateTime | Das Check-in Datum für die Zimmerreservierung. |
| `checkOutDate` | DateTime | Das Datum des Auscheckens für die Zimmerreservierung. |
| `confirmationNumber` | Zeichenfolge | Die Buchungsbestätigungsnummer oder -kennung. |
| `couponCode` | Zeichenfolge | Gutscheincode für die Hotelbuchung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für den Kauf verwendet wird. |
| `discountPercent` | Double | Der mit der Buchung verbundene Rabattprozentsatz. |
| `freeCancelation` | Boolesch | Gibt an, ob das Zimmer kostenfrei storniert werden kann. |
| `guestID` | Zeichenfolge | Die mit der Hotelbuchung verknüpfte Gast-ID. |
| `length` | Ganzzahl | Die Gesamtanzahl der Tage für die Reservierung. |
| `loyaltyID` | Zeichenfolge | Die Kennung des Treueprogramms für den in der Reservierung aufgelisteten Gast. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt der letzten Änderung der Reservierung. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `numberOfRooms` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Zimmer. |
| `propertyID` | Zeichenfolge | Kennung des Hotels oder Resorts für die Reservierung. |
| `propertyName` | Zeichenfolge | Der Name des Hotels oder Resorts für die Reservierung. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `ratePlan` | Zeichenfolge | Das Tarifangebot, zu dem das Zimmer verkauft wurde. |
| `refundable` | Boolesch | Gibt an, ob das Zimmer erstattbar ist. |
| `reservationStatus` | Zeichenfolge | Der Status der Reservierung. |
| `roomAccessibilityType` | Zeichenfolge | Der Barrierefreiheitstyp des Raums, z. B. Mobilität, Anhörung oder andere. |
| `roomCapacity` | Ganzzahl | Die Anzahl der Personen im Hotelzimmer. |
| `roomType` | Zeichenfolge | Die Art des reservierten Zimmers. |
| `smoking` | Boolesch | Gibt an, ob das Rauchen in dem Zimmer erlaubt ist. |
| `tripType` | Zeichenfolge | Gibt an, ob die Reservierung für eine Einweg-, Hin- und Rückfahrt oder für eine mehrstündige Reise gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
