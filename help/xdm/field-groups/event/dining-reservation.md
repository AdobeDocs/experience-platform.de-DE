---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Reservierung;Speisen;
title: Schemafeldgruppe für Restaurantreservierung
description: Erfahren Sie mehr über die Schemafeldgruppe „Restaurantreservierung“.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# [!UICONTROL Restaurantreservierung] Schemafeldgruppe

[!UICONTROL Restaurantreservierung] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM ExperienceEvent] , &#x200B;](../../classes/experienceevent.md) verwendet wird, um Informationen zu einer Restaurantreservierung zu erfassen.

Die Feldergruppe ist eine Erweiterung der Feldergruppe [!UICONTROL Reservierungsdetails] und enthält alle gleichen Felder unter einem einzigen Feld vom Typ „Objekt“, `reservations`. Zusätzlich zu diesen allgemeinen Feldern enthält [!UICONTROL Restaurantreservierung] auch `diningReservations` Array. Dieses Array von Objekten wird verwendet, um eine oder mehrere Reservierungen mit Restaurantspezifischen Eigenschaften zu beschreiben.

>[!NOTE]
>
>In diesem Dokument werden die Details des `diningReservations`-Arrays behandelt. Informationen zu den anderen Feldern, die unter dem `reservations` Objekt bereitgestellt werden, finden Sie in der [[!UICONTROL Reservierungsdetails] Feldergruppenreferenz](./reservation-details.md).

![Restaurantreservierungsstruktur](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` ist ein Array von Objekten, das eine Liste von Restaurantreservierungen darstellt. Wenn ein Reservierungsereignis beispielsweise Reservierungen in mehreren verschiedenen Restaurants zu unterschiedlichen Tageszeiten beinhaltet, können diese Reservierungen als einzelne Objekte unter `diningReservations` für ein einzelnes Ereignis aufgeführt werden.

Die Struktur der einzelnen -Objekte, die unter `diningReservations` bereitgestellt werden, wird unten angezeigt.

![Restaurantreservierungsstruktur](../../images/field-groups/dining-reservation/diningReservations.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ID` | Zeichenfolge | Die Reservierungsnummer oder -kennung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung storniert wurde. |
| `confirmationNumber` | String | Die Nummer oder Kennung der Reservierungsbestätigung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung erstellt wurde. |
| `cuisine` | Ganzzahl | Die Art der Restaurantküche |
| `currencyCode` | String | Der ISO 4217-Währungscode, der für den Kauf verwendet wurde. |
| `deliveryPartners` | String | Im Restaurant verfügbare Lieferpartner. |
| `diningOptions` | String | Liefer- und Speiseoptionen, die im Restaurant verfügbar sind. |
| `groupReservation` | Boolesch | Gibt an, ob die Reservierung für eine Gruppe vorgenommen wird. |
| `length` | Ganzzahl | Die Gesamtzahl der Tage für die Reservierung. |
| `loyaltyID` | String | Die ID des Treueprogramms für den in der Reservierung aufgeführten Gast. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der Kinder, die mit der Reservierung verknüpft sind. |
| `numberOfRooms` | Ganzzahl | Die Anzahl der Zimmer, die mit der Reservierung verbunden sind. |
| `partySize` | Ganzzahl | Die Anzahl der Personen in der Restaurantgruppe. |
| `priceCategory` | String | Die Preiskategorie für die durchgeführte Reservierung. |
| `purpose` | String | Der Zweck der Reservierung, in der Regel entweder geschäftlich oder privat. |
| `reservationTime` | DateTime | Die Zeit, für die die Restaurantreservierung gebucht ist. |
| `restaurantID` | String | Eine Kennung für das Restaurant oder den Restaurantstandort. |
| `reservationStatus` | String | Der Status der Reservierung. |
| `specialOccasion` | Boolesch | Gibt an, ob die Reservierung für einen besonderen Anlass vorgenommen wird. |
| `status` | Ganzzahl | Der Status der Restaurantreservierung. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
