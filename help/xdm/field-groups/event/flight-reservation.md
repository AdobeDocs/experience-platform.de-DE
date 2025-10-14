---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Reservierung;Flug;
title: Feldergruppe „Flugreservierungsschema“
description: Erfahren Sie mehr über die Schemafeldgruppe „Flugreservierung“.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# [!UICONTROL Flugreservierung] Schemafeldgruppe

[!UICONTROL Flugreservierung] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM ExperienceEvent] , &#x200B;](../../classes/experienceevent.md) verwendet wird, um Informationen zu einer Flugreservierung zu erfassen.

Die Feldergruppe ist eine Erweiterung der Feldergruppe [!UICONTROL Reservierungsdetails] und enthält alle gleichen Felder unter einem einzigen Feld vom Typ „Objekt“, `reservations`. Zusätzlich zu diesen generischen Feldern enthält [!UICONTROL Flugreservierung] auch `flightReservations` Array. Dieses Array von Objekten wird verwendet, um eine oder mehrere Reservierungen mit einzigartigen Eigenschaften für Flugreisen zu beschreiben.

>[!NOTE]
>
>In diesem Dokument werden die Details des `flightReservations`-Arrays behandelt. Informationen zu den anderen Feldern, die unter dem `reservations` Objekt bereitgestellt werden, finden Sie in der [[!UICONTROL Reservierungsdetails] Feldergruppenreferenz](./reservation-details.md).

![Struktur der Flugreservierung](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` ist ein Array von Objekten, das eine Liste der Flugreservierungen darstellt. Wenn ein Reservierungsereignis beispielsweise Reservierungen für mehrere Anschlussflüge auf einer Reise umfasst, können diese Reservierungen als einzelne Objekte unter `flightReservations` für ein einzelnes Ereignis aufgeführt werden.

Die Struktur der einzelnen -Objekte, die unter `flightReservations` bereitgestellt werden, wird unten angezeigt.

![flightReservations-Struktur](../../images/field-groups/flight-reservation/flightReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `flightCheckIn` | Objekt | Erfasst Details zum Check-in. Das Objekt enthält die folgenden Eigenschaften:<ul><li>`arrivalAirportCode`: (String) Der Flughafencode der Ankunftsstadt.</li><li>`boardingGroup`: (String) Der fluggesellschaftsspezifische Indikator für die Einsteigereihenfolge.</li><li>`checkInMethod`: (String) Die beim Einchecken verwendete Methode, z. B. Schalter, Online, Kiosk oder Self-Service.</li><li>`checkedBags`: (Integer) Die Anzahl der für den Flug aufgegebenen Gepäckstücke.</li><li>`checkedPassengers`: (Integer) Die Anzahl der für den Flug eingecheckten Passagiere, wenn mehrere Passagiere für dieselbe Reservierungsnummer vorhanden sind.</li><li>`confirmationNumber`: (String) Die Reservierungsbestätigungsnummer oder -kennung.</li><li>`departureAirportCode`: (String) Der Flughafen-Code der Abflugstadt.</li><li>`flightNumber`: (String) Die Flugnummer für den reservierten Flug.</li></ul> |
| `flightStatusSearch` | Objekt | Erfasst die Details, die zurückgegeben werden, wenn der Status des Fluges durchsucht wird. Das Objekt enthält die folgenden Eigenschaften:<ul><li>`arrivalAirportCode`: (String) Der Flughafencode der Ankunftsstadt.</li><li>`boardingGroup`: (String) Der fluggesellschaftsspezifische Indikator für die Einsteigereihenfolge.</li><li>`departureAirportCode`: (String) Der Flughafen-Code der Abflugstadt.</li><li>`departureDate`: (DateTime) Das Abflugdatum des zu reservierenden Fluges.</li><li>`flightNumber`: (String) Die Flugnummer für den reservierten Flug.</li><li>`searchCount`: (Integer) Die Häufigkeit, mit der der Status des reservierten Fluges gesucht wurde.</li></ul> |
| `agentID` | String | Der Agent oder Bucher, der für die Reservierung verantwortlich ist, falls zutreffend. |
| `aircraftID` | String | Eine Kennung für das Luftfahrzeug. |
| `aircraftType` | String | Der Flugzeugtyp. |
| `arrivalAirportCode` | String | Der Flughafencode der Ankunftsstadt. |
| `arrivalDate` | DateTime | Das Ankunftsdatum des zu reservierenden Fluges. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung storniert wurde. |
| `confirmationNumber` | String | Die Nummer oder Kennung der Reservierungsbestätigung. |
| `created` | String | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `currencyCode` | String | Der ISO 4217-Währungscode, der für den Kauf verwendet wurde. |
| `departureAirportCode` | String | Der Flughafencode der Abflugstadt. |
| `departureDate` | DateTime | Das Abflugdatum des zu reservierenden Fluges. |
| `fareClass` | String | Die Tarifklasse des zu reservierenden Fluges. |
| `flightNumber` | String | Die Flugnummer des zu reservierenden Fluges. |
| `length` | Ganzzahl | Die Gesamtzahl der Tage für die Reservierung. |
| `loyaltyID` | String | Die ID des Treue- oder Prämienprogramms für den in der Reservierung aufgeführten Passagier. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der Kinder, die mit der Reservierung verknüpft sind. |
| `passengerID` | String | Fahrgastinformationen, die mit der Reservierung verbunden sind. |
| `purpose` | String | Der Zweck der Reservierung, in der Regel entweder geschäftlich oder privat. |
| `salesChannel` | String | Der Vertriebskanal, über den die Reservierung gebucht wurde. |
| `securityScreening` | String | Art der Sicherheitskontrolle, der der Fluggast unterzogen wird. |
| `status` | String | Der Status der Flugreservierung. |
| `ticketNumber` | String | Die Reservierungsnummer oder -kennung. |
| `tripType` | String | Gibt an, ob die Reservierung für eine einfache Fahrt, eine Hin- und Rückfahrt oder eine Reise mit mehreren Städten gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
