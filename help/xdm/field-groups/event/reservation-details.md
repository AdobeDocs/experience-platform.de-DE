---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;felder;schemas;schemas;schema design;feldgruppe;feldergruppe;reservierung;reservierungsdetails;
title: Schemafeldgruppe „Reservierungsdetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Reservierungsdetails“.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 8%

---

# [!UICONTROL Reservierungsdetails] Schemafeldgruppe

[!UICONTROL Reservierungsdetails] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM ExperienceEvent] , &#x200B;](../../classes/experienceevent.md) verwendet wird, um Informationen zu einer Reservierung zu erfassen, einschließlich Länge, Änderung, Erstattungsstatus und Anzahl der Zimmer.

Die Feldergruppe stellt `reservations` ein einzelnes Feld vom Typ „Objekt“ bereit. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

![Struktur der Reservierungsdetails](../../images/field-groups/reservation-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `nonRefundableAmount` | [Währung](../../data-types/currency.md) | Der Betrag des Reservierungspreises, der als nicht erstattungsfähig gekennzeichnet ist. |
| `transaction` | [Transaktion](../../data-types/transaction.md) | Beschreibt die Währungstransaktion für die Reservierung. |
| `id` | String | Eine eindeutige Kennung für die Reservierung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung storniert wurde. |
| `confirmationNumber` | String | Die Bestätigungsnummer oder Kennung für die Reservierung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn die Reservierung erstellt wurde. |
| `currencyCode` | String | Der ISO 4217-Währungscode, der für den Kauf verwendet wurde. |
| `endDate` | DateTime | Das Endabgabe-, Rückgabe- oder Check-out-Datum für die Reservierung. |
| `length` | Ganzzahl | Die Gesamtzahl der Tage für die Reservierung. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der Kinder, die mit der Reservierung verknüpft sind. |
| `purpose` | String | Der Zweck der Reservierung, in der Regel entweder geschäftlich oder privat. |
| `startDate` | DateTime | Das Start-, Abhol-, Ausgangs- oder Check-in-Datum für die Reservierung. |
| `triptype` | String | Gibt an, ob die Reservierung für eine einfache Fahrt, eine Hin- und Rückfahrt oder eine Reise mit mehreren Städten gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Branchenspezifische Reservierungsfeldgruppen

Es gibt mehrere andere Standardfeldgruppen, die das Schema [!UICONTROL Reservierungsdetails] für branchenspezifische Anwendungsfälle erweitern. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [[!UICONTROL Restaurantreservierung]](./dining-reservation.md)
* [[!UICONTROL Flugreservierung]](./flight-reservation.md)
* [[!UICONTROL Unterkunftsreservierung]](./lodging-reservation.md)
