---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Speisen;
title: Definieren der Feldergruppe "Reservierungsschema"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Buchungs-Schema definieren.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 6%

---

# [!UICONTROL Definieren ] der Feldergruppe &quot;Reservationschema&quot;

[!UICONTROL Die Essenreservierung ] ist eine Standardschemafeldergruppe für die  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) Klasse, die zur Erfassung von Informationen über eine Essensreservierung verwendet wird.

Die Feldergruppe ist eine Erweiterung der Feldergruppe [!UICONTROL Reservierungsdetails] und enthält alle gleichen Felder unter einem einzigen Feld vom Typ Objekt `reservations`. Zusätzlich zu diesen generischen Feldern enthält [!UICONTROL Definieren der Reservierung] auch `diningReservations` -Array. Dieses Objekt-Array wird verwendet, um eine oder mehrere Reservierungen mit Restaurant-spezifischen Eigenschaften zu beschreiben.

>[!NOTE]
>
>Dieses Dokument behandelt die Details des `diningReservations`-Arrays. Informationen zu den anderen Feldern, die unter dem `reservations`-Objekt bereitgestellt werden, finden Sie in der [[!UICONTROL Reservierungsdetails] Feldgruppenreferenz](./reservation-details.md).

![Präparationsstruktur](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` ist eine Gruppe von Objekten, die eine Liste von Essensreservierungen darstellen. Wenn ein Reservierungsereignis Reservierungen in mehreren verschiedenen Restaurants zu unterschiedlichen Tageszeiten beinhaltet, können diese Reservierungen beispielsweise als einzelne Objekte unter `diningReservations` für eine einzelne Veranstaltung aufgeführt werden.

Die Struktur der einzelnen Objekte, die unter `diningReservations` bereitgestellt werden, finden Sie unten.

![EssReservierungsstruktur](../../images/field-groups/dining-reservation/diningReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ID` | Zeichenfolge | Die Reservierungsnummer oder -kennung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung abgebrochen wurde. |
| `confirmationNumber` | Zeichenfolge | Die Reservierungsbestätigungsnummer oder -kennung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `cuisine` | Ganzzahl | Die Art der Restaurantküche. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für den Kauf verwendet wird. |
| `deliveryPartners` | Zeichenfolge | Im Restaurant stehen Ihnen Versandpartner zur Verfügung. |
| `diningOptions` | Zeichenfolge | Im Restaurant stehen Ihnen Versand- und Speiseoptionen zur Verfügung. |
| `groupReservation` | Boolesch | Gibt an, ob die Reservierung für eine Gruppe vorgenommen wird. |
| `length` | Ganzzahl | Die Gesamtanzahl der Tage für die Reservierung. |
| `loyaltyID` | Zeichenfolge | Die Kennung des Treueprogramms für den in der Reservierung aufgelisteten Gast. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `numberOfRooms` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Zimmer. |
| `partySize` | Ganzzahl | Die Anzahl der Personen auf der Essparty. |
| `priceCategory` | Zeichenfolge | Die Preiskategorie für die Buchung. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `reservationTime` | DateTime | Der Zeitpunkt, zu dem die Speisekarte gebucht wird. |
| `restaurantID` | Zeichenfolge | Eine Kennung für das Restaurant oder den Essort. |
| `reservationStatus` | Zeichenfolge | Der Status der Reservierung. |
| `specialOccasion` | Boolesch | Gibt an, ob die Reservierung für einen besonderen Anlass erfolgt. |
| `status` | Ganzzahl | Der Status der Speisekarte. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
