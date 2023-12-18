---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Reservierung; Reservierungsdetails;
title: Feldergruppe "Buchungsdetails"
description: Erfahren Sie mehr über die Feldergruppe Buchungsdetails .
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 8%

---

# [!UICONTROL Buchungsdetails] Schemafeldgruppe

[!UICONTROL Buchungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) dient zur Erfassung von Informationen über eine Reservierung, einschließlich der Länge, Änderung, erstattungsfähigen Status und der Anzahl der Zimmer.

Die Feldergruppe stellt ein einzelnes Feld vom Typ Objekt bereit, `reservations`. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

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
| `modificationDate` | DateTime | Der Zeitpunkt der letzten Änderung der Reservierung. |
| `numberOfAdults` | Ganzzahl | Die Anzahl der Erwachsenen, die mit der Reservierung verbunden sind. |
| `numberOfChildren` | Ganzzahl | Die Anzahl der mit der Reservierung verbundenen Kinder. |
| `purpose` | Zeichenfolge | Der Zweck der Reservierung, in der Regel geschäftlich oder persönlich. |
| `startDate` | DateTime | Das Startdatum für die Reservierung. |
| `triptype` | Zeichenfolge | Gibt an, ob die Reservierung für eine Einweg-, Hin- und Rückfahrt oder für eine mehrstündige Reise gilt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Branchenspezifische Reservierungsfeldgruppen

Es gibt mehrere weitere Standardfeldgruppen, die die [!UICONTROL Buchungsdetails] Schema für branchenspezifische Anwendungsfälle. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [[!UICONTROL Restaurantreservierung]](./dining-reservation.md)
* [[!UICONTROL Flugreservierung]](./flight-reservation.md)
* [[!UICONTROL Unterkunftsreservierung]](./lodging-reservation.md)
