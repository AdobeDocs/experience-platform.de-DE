---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Reservierungsdetails;
title: Feldergruppe "Buchungsdetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe "Buchungsdetails".
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 6%

---


# [!UICONTROL Feldergruppe ] &quot;Reservierungsdetails&quot;

[!UICONTROL Reservierungsdetails ] sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) Klasse, die verwendet wird, um Informationen zu einer Reservierung zu erfassen, einschließlich der Länge, Änderung, erstattbarem Status und der Anzahl der Zimmer.

Die Feldergruppe stellt ein einzelnes Objekt-Feld bereit, `reservations`. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

![Struktur der Buchungsdetails](../../images/field-groups/reservation-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `nonRefundableAmount` | [Währung](../../data-types/currency.md) | Die Höhe des Reservierungspreises, der als nicht erstattbar gekennzeichnet ist. |
| `transaction` | [Transaktion](../../data-types/transaction.md) | Beschreibt die Währungstransaktion für die Reservierung. |
| `id` | Zeichenfolge | Eine eindeutige Kennung für die Reservierung. |
| `cancellation` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung abgebrochen wurde. |
| `confirmationNumber` | Zeichenfolge | Die Bestätigungsnummer oder die Kennung für die Reservierung. |
| `created` | Ganzzahl | Dieser Wert wird erfasst, wenn die Reservierung erstellt wurde. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für den Kauf verwendet wird. |
| `endDate` | DateTime | Das Enddatum für die Reservierung (Abbruch, Rückgabe oder Checkout). |
| `length` | Ganzzahl | Die Gesamtanzahl der Tage für die Reservierung. |
| `modification` | Ganzzahl | Dieser Wert wird erfasst, wenn eine Reservierung geändert wurde. |
| `modificationDate` | DateTime | Der Zeitpunkt, zu dem die Reservierung zuletzt geändert wurde. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `startDate` | DateTime | Das Startdatum für die Reservierung. |
| `triptype` | Zeichenfolge | Gibt an, ob die Reservierung für eine Einweg-, Hin- und Rückfahrt oder für eine mehrstündige Reise gilt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Branchenspezifische Reservierungsfeldgruppen

Es gibt mehrere weitere Standardfeldgruppen, die das Schema [!UICONTROL Reservierungsdetails] für branchenspezifische Anwendungsfälle erweitern. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [[!UICONTROL Speisereservierung]](./dining-reservation.md)
* [[!UICONTROL Flugreservierung]](./flight-reservation.md)
* [[!UICONTROL Unterkunftsreservierung]](./lodging-reservation.md)