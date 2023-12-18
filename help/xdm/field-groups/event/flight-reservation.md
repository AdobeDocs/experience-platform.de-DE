---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Flug;
title: Feldergruppe "Flugreservierungsschema"
description: Erfahren Sie mehr über die Feldergruppe Flugreservierungsschema .
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 5%

---

# [!UICONTROL Flugreservierung] Schemafeldgruppe

[!UICONTROL Flugreservierung] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) zur Erfassung von Informationen über eine Flugreservierung verwendet werden.

Die Feldergruppe ist eine Erweiterung der [!UICONTROL Buchungsdetails] Feldergruppe und enthält alle gleichen Felder unter einem Feld vom Typ &quot;Objekt&quot;, `reservations`. Zusätzlich zu diesen allgemeinen Feldern [!UICONTROL Flugreservierung] auch `flightReservations` Array. Dieses Objekt dient zur Beschreibung einer oder mehrerer Reservierungen mit Eigenschaften, die für Flugreisen eindeutig sind.

>[!NOTE]
>
>In diesem Dokument werden die Details der `flightReservations` Array. Für Informationen über die anderen Felder, die im `reservations` -Objekt, siehe [[!UICONTROL Buchungsdetails] Feldergruppenreferenz](./reservation-details.md).

![Struktur der Flugreservierung](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` ist ein Array von Objekten, das eine Liste von Flugreservierungen darstellt. Wenn ein Reservierungsereignis Reservierungen für mehrere Anschlussflüge auf einer Reise beinhaltet, können diese Reservierungen beispielsweise als einzelne Objekte unter `flightReservations` für ein einzelnes Ereignis.

Die Struktur der einzelnen Objekte, die unter `flightReservations` ist unten angegeben.

![Struktur der Flugreservierungen](../../images/field-groups/flight-reservation/flightReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `flightCheckIn` | Objekt | Erfasst Details zum Check-in. Das -Objekt umfasst die folgenden Eigenschaften:<ul><li>`arrivalAirportCode`: (String) Der Flughafen-Code der Ankunftsstadt.</li><li>`boardingGroup`: (String) Der fluglinien-spezifische Indikator der Boarding-Reihenfolge.</li><li>`checkInMethod`: (String) Die Methode, die den Einchecken verwendet hat, z. B. Zähler, Online, Kiosk oder Self-Service.</li><li>`checkedBags`: (Integer) Die Anzahl der Gepäckstücke, die für den Flug geprüft wurden.</li><li>`checkedPassengers`: (Integer) Die Anzahl der Fluggäste, die für den Flug eingecheckt wurden, wenn für dieselbe Buchungsnummer mehrere Fluggäste vorhanden sind.</li><li>`confirmationNumber`: (String) Die Buchungsbestätigungsnummer oder -kennung.</li><li>`departureAirportCode`: (String) Der Flughafen-Code der Abflugstadt.</li><li>`flightNumber`: (String) Die Flugnummer für den reservierten Flug.</li></ul> |
| `flightStatusSearch` | Objekt | Erfasst die bei der Statussuche des Fluges zurückgegebenen Daten. Das -Objekt umfasst die folgenden Eigenschaften:<ul><li>`arrivalAirportCode`: (String) Der Flughafen-Code der Ankunftsstadt.</li><li>`boardingGroup`: (String) Der fluglinien-spezifische Indikator der Boarding-Reihenfolge.</li><li>`departureAirportCode`: (String) Der Flughafen-Code der Abflugstadt.</li><li>`departureDate`: (DateTime) Das Abflugdatum des reservierten Fluges.</li><li>`flightNumber`: (String) Die Flugnummer für den reservierten Flug.</li><li>`searchCount`: (Integer) Die Anzahl der Suchen nach dem Status des reservierten Fluges.</li></ul> |
| `agentID` | Zeichenfolge | Der für die Reservierung verantwortliche Vertreter oder Bucher, falls zutreffend. |
| `aircraftID` | Zeichenfolge | Eine Kennung für das Luftfahrzeug. |
| `aircraftType` | Zeichenfolge | Der Typ des Luftfahrzeugs. |
| `arrivalAirportCode` | Zeichenfolge | Der Flughafencode der Ankunftsstadt. |
| `arrivalDate` | DateTime | Ankunftsdatum des reservierten Fluges. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung abgebrochen wurde. |
| `confirmationNumber` | Zeichenfolge | Die Buchungsbestätigungsnummer oder -kennung. |
| `created` | Zeichenfolge | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für den Kauf verwendet wird. |
| `departureAirportCode` | Zeichenfolge | Der Flughafencode der Abflugstadt. |
| `departureDate` | DateTime | Das Abflugdatum des reservierten Fluges. |
| `fareClass` | Zeichenfolge | Die Flugklasse des reservierten Fluges. |
| `flightNumber` | Zeichenfolge | Die Flugnummer des reservierten Fluges. |
| `length` | Ganzzahl | Die Gesamtanzahl der Tage für die Reservierung. |
| `loyaltyID` | Zeichenfolge | Die Kennung des Treueprogramms oder Belohnungsprogramms für den in der Reservierung aufgeführten Passagier. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt der letzten Änderung der Reservierung. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `passengerID` | Zeichenfolge | Fluggastinformationen, die mit der Reservierung verbunden sind. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `salesChannel` | Zeichenfolge | Der Vertriebskanal, über den die Reservierung gebucht wurde. |
| `securityScreening` | Zeichenfolge | Die Art der Sicherheitsüberprüfung, der der Fluggast unterzogen wird. |
| `status` | Zeichenfolge | Der Status der Flugreservierung. |
| `ticketNumber` | Zeichenfolge | Die Reservierungsnummer oder -kennung. |
| `tripType` | Zeichenfolge | Gibt an, ob die Reservierung für eine Einweg-, Hin- und Rückfahrt oder für eine mehrstündige Reise gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
