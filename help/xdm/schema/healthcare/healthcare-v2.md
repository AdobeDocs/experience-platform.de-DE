---
title: Gesundheitsdatenmodell V2
description: Erfahren Sie mehr über einige häufige Anwendungsfälle für das Gesundheitswesen und die besten Klassen, die zugehörigen Feldgruppen und Datentypen, die verwendet werden sollten.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 8eaff2361e76a7856b3371156ed9fe5c542fec28
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 4%

---

# [!UICONTROL Healthcare] Datenmodell V2

## Feldergruppen und Klassen {#field-groups}

In der folgenden Tabelle werden die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle der Gesundheitsfürsorge beschrieben.

| Anwendungsfall | Feldergruppen und kompatible Klassen |
| --- | --- |
| **Patienten erstellen/aktualisieren**: Wenn ein Patient an der Krankenhausfront ankommt, wird ein Patientendatensatz erstellt, der demografische Details wie eine Kennung (optional), den Namen des Patienten, das Geburtsdatum, das Geschlecht und seine Adresse enthält. Dies ist ein wichtiger Bestandteil der IT im Gesundheitswesen. | <ul><li>**[XDM Individual Profiles](../../classes/individual-profile.md)**:<ul><li>[Patient](./field-groups/patient.md)</li></ul></li></ul> |
| **Impfung**: Erleichterung des Impfprozesses, Verwaltung der Patientenimpfungsunterlagen und Integration von EMRs in Impfmanagementsysteme. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Immunisierung](./field-groups/immunization.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Location](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Meditation](../../classes/medication.md)**:<ul><li>[Meditation](./field-groups/medication.md)</li><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li></ul></li><li>**[Provider](../../classes/provider.md)**:<ul><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li></ul></li></ul> |
| **Einhaltung nach der Behandlung**: Motivieren Sie Patienten und Pflegekräfte, ihre Behandlungspläne abzuschließen und die Überweisungsraten zu reduzieren. | <ul><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Care Plan](./field-groups/care-plan.md)</li><li>[Ziel](./field-groups/goal.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Location](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Provider](../../classes/provider.md)**:<ul><li>[Ziel](./field-groups/goal.md)</li></ul></li></ul> |
| **Kundenerlebnis für Versicherungen**: Verbesserung der digitalen Akquise und der Erfahrungen bei Verbrauchern, die für Versicherungen einkaufen. Zu den Beispielen gehören: <li> Verstehen des Verbraucherverhaltens zum Senden von Werbe-E-Mails oder zielgerichteten Anzeigen von Drittanbietern an Personen, die auf Seiten zugreifen, die allgemeine Informationen enthalten (z. B. Pläne, Planungsnamen/Ebenen, Arzneimittel oder Wellness-Programme)</li><li> Versand von Impfstoffinformationen über Herzkrankheiten zur Sensibilisierung der Marke oder zur Aufforderung, Impfstoffe für Personen zu planen, die nach Informationen über Herzgesundheit und Impfstoff suchen. </li> | <ul><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Konto](./field-groups/account.md)</li><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Location](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Meditation](../../classes/medication.md)**:<ul><li>[Meditation](./field-groups/medication.md)</li><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li></ul></li><li>**[Provider](../../classes/provider.md)**:<ul><li>[Konto](./field-groups/account.md)</li><li>[Medikationskosten](./field-groups/medication-dispense.md)</li><li>[Medikationsanfrage](./field-groups/medication-request.md)</li></ul><li>**[Plan](../../classes/plan.md)**:<ul><li>[Ziel](./field-groups/coverage.md)</li></ul></li></ul> |
| **Verbessertes Anbietererlebnis**: Verwenden von Anbieterdaten aus dem EMR-System, um alternative Anbieter basierend auf Terminverfügbarkeit, Standort und Spezialität vorzuschlagen. <br> <br>Verbessern der Anbietersuche, um Ergebnisse mit der gewünschten Verfügbarkeit anzuzeigen, Überprüfen, ob der ausgewählte Anbieter Teil des Payor-Netzwerks ist, und Bereitstellen von Kostenschätzungen. | <ul><li>**[XDM Individual Profiles](../../classes/individual-profile.md)**:<ul><li>[Organisation](./field-groups/organization.md)</li><li>[Patient](./field-groups/patient.md)</li><li>[Praktitioner](./field-groups/practioner.md)</li><li>[Planung](./field-groups/schedule.md)</li></ul></li><li>**[Location](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Provider](../../classes/provider.md)**:<ul><li>[Organisation](./field-groups/organization.md)</li><li>[Praktitioner](./field-groups/practioner.md)</li><li>[Planung](./field-groups/schedule.md)</li></ul></li></ul> |

## Datentypen {#data-types}

In der folgenden Tabelle sind die gemäß den [!DNL HL7 FHIR Release 5] -Spezifikationen erstellten Datentypen aufgeführt.

| Name | Beschreibung |
| --- | --- |
| [[!UICONTROL Adresse]](./data-types/address.md) | Beschreibt eine Adresse, die anhand von Postkonventionen ausgedrückt wird (im Gegensatz zu GPS oder anderen Standortdefinitionsformaten). |
| [[!UICONTROL Anmerkung]](./data-types/annotation.md) | Ein Textknoten mit Attribution zum Autor. |
| [[!UICONTROL Verfügbarkeit]](./data-types/availability.md) | Verfügbarkeitsdaten für einen Artikel. |
| [[!UICONTROL Codeable Concept]](./data-types/codeable-concept.md) | Ein Verweis von einer Ressource zur anderen. |
| [[!UICONTROL Codeable Reference]](./data-types/codeable-reference.md) | Ein Verweis auf eine Ressource oder ein Konzept. |
| [[!UICONTROL Kodierung]](./data-types/coding.md) | Ein Verweis auf einen von einem Terminologiesystem definierten Code. |
| [[!UICONTROL Kontaktpunkt]](./data-types/contact-point.md) | Kontaktinformationen für eine Person. |
| [[!UICONTROL Dosierung]](./data-types/dosage.md) | Wie das Arzneimittel eingenommen wird/wurde oder eingenommen werden sollte. |
| [[!UICONTROL Dauer]](./data-types/duration.md) | Eine Zeitdauer. |
| [[!UICONTROL Erweiterte Kontaktdetails]](./data-types/extended-contact-detail.md) | Informationen eines erweiterten Kontakts. |
| [[!UICONTROL Menschenname]](./data-types/human-name.md) | Informationen über den Namen einer menschlichen oder anderen lebenden Entität. |
| [[!UICONTROL ID]](./data-types/identifier.md) | Ein Bezeichner für die Berechnung. |
| [[!UICONTROL Money]](./data-types/money.md) | Ein wirtschaftlicher Nutzen in einer anerkannten Währung. |
| [[!UICONTROL Zeitraum]](./data-types/period.md) | Ein Zeitraum, der durch ein Start- und Enddatum/-zeit definiert wird. |
| [[!UICONTROL Person]](./data-types/person.md) | Informationen zu einem generischen Personendatensatz. |
| [[!UICONTROL Quantity]](./data-types/quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Bereich]](./data-types/range.md) | Ein Satz von Werten, die durch niedrige und hohe Werte gebunden sind. |
| [[!UICONTROL Verhältnis]](./data-types/ratio.md) | Ein Verhältnis von zwei [[!UICONTROL Quantity]](./data-types/quantity.md) -Werten durch einen Zähler und einen Nenner. |
| [[!UICONTROL Referenz]](./data-types/reference.md) | Ein Verweis von einer Ressource zur anderen. |
| [[!UICONTROL Wiederholen]](./data-types/repeat.md) | Ein Regelsatz, der beschreibt, wann ein Ereignis geplant wird. |
| [[!UICONTROL Einfache Menge]](./data-types/simple-quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Timing]](./data-types/timing.md) | Informationen zu einem Ereignis, das mehrmals auftreten kann. |
| [[!UICONTROL Virtual Service-Detail]](./data-types/virtual-service-detail.md) | Kontaktdaten für den virtuellen Dienst. |
