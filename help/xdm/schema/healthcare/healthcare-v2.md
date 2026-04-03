---
title: Gesundheitsdatenmodell v2
description: Erfahren Sie mehr über einige gängige Anwendungsfälle im Gesundheitswesen und die besten Klassen, zugehörigen Feldergruppen und zu verwendenden Datentypen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 3%

---

# [!UICONTROL Healthcare]-Datenmodell v2

## Feldergruppen und -klassen {#field-groups}

In der folgenden Tabelle sind die empfohlenen Klassen und Schemafeldgruppen für mehrere gängige Anwendungsfälle im Gesundheitswesen aufgeführt.

| Anwendungsfall | Feldergruppen und kompatible Klassen |
| --- | --- |
| **Patient erstellen/aktualisieren**: Wenn ein Patient an der Klinik ankommt, wird eine Patientenakte erstellt, einschließlich demografischer Details wie einer Kennung (optional), dem Patientennamen, dem Geburtsdatum, dem Geschlecht und der Adresse. Dies ist ein wichtiger Bestandteil der IT im Gesundheitswesen. | <ul><li>**[Individuelle XDM-Profile](../../classes/individual-profile.md)**:<ul><li>[Patient](./field-groups/patient.md)</li></ul></li></ul> |
| **Impfung**: Erleichterung des Impfprozesses, Verwaltung der Patientenimpfakten und Integration von EMRs mit Impfmanagement-Systemen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Immunisierung](./field-groups/immunization.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Standort](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Medizin](../../classes/medication.md)**:<ul><li>[Medizin](./field-groups/medication.md)</li><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li></ul></li><li>**[Provider](../../classes/provider.md)**:<ul><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li></ul></li></ul> |
| **Nachsorge-Compliance**: Patienten und Betreuer dazu motivieren, ihre Behandlungspläne zu vervollständigen und die Überweisungsraten zu reduzieren. | <ul><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Betreuungsplan](./field-groups/care-plan.md)</li><li>[Ziel](./field-groups/goal.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Standort](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Provider](../../classes/provider.md)**:<ul><li>[Ziel](./field-groups/goal.md)</li></ul></li></ul> |
| **Verbrauchererlebnis für Versicherungen**: Verbessern Sie die digitale Akquise und die Erlebnisse von Verbrauchern, die Versicherungen kaufen. Zu den Beispielen gehören: <li> Verstehen des Verbraucherverhaltens zum Senden von Werbe-E-Mails oder zielgerichteten Anzeigen von Drittanbietern an Personen, die auf Seiten zugreifen, die allgemeine Informationen enthalten (z. B. Pläne, Plannamen/Ebenen, Medicaid oder Wellness-Programme)</li><li> Senden von Informationen über die Herzgesundheit, um das Markenbewusstsein zu schärfen, oder Anfragen zur Planung von Impfungen an Personen, die nach Informationen über die Herzgesundheit und Impfstoffe suchen. </li> | <ul><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Konto](./field-groups/account.md)</li><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Standort](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Medizin](../../classes/medication.md)**:<ul><li>[Medizin](./field-groups/medication.md)</li><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li></ul></li><li>**[Provider](../../classes/provider.md)**:<ul><li>[Konto](./field-groups/account.md)</li><li>[Medikamentenabgabe](./field-groups/medication-dispense.md)</li><li>[Medikamentenanfrage](./field-groups/medication-request.md)</li></ul><li>**[Plan](../../classes/plan.md)**:<ul><li>[Ziel](./field-groups/coverage.md)</li></ul></li></ul> |
| **Verbessertes Anbietererlebnis**: Verwenden von Anbieterdaten aus dem EMR-System, um alternative Anbieter auf der Grundlage von Terminverfügbarkeit, Standort und Fachgebiet vorzuschlagen. <br> <br>Verbessern der Anbietersuche, um Ergebnisse mit der gewünschten Verfügbarkeit anzuzeigen, Überprüfen, ob der ausgewählte Anbieter Teil des Payor-Netzwerks ist, und Bereitstellen von Kostenschätzungen. | <ul><li>**[Individuelle XDM-Profile](../../classes/individual-profile.md)**:<ul><li>[Termin](./field-groups/appointment.md)</li><li>[Organisation](./field-groups/organization.md)</li><li>[Patient](./field-groups/patient.md)</li><li>[Praktiker](./field-groups/practioner.md)</li><li>[Planung](./field-groups/schedule.md)</li></ul></li><li>**[Standort](./classes/location.md)**:<ul><li>[Ort](./field-groups/location.md)</li></ul><li>**[Provider](../../classes/provider.md)**:<ul><li>[Termin](./field-groups/appointment.md)</li><li>[Organisation](./field-groups/organization.md)</li><li>[Praktiker](./field-groups/practioner.md)</li><li>[Planung](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:fixed"}

## Datentypen {#data-types}

In der folgenden Tabelle sind die Datentypen aufgeführt, die gemäß den [!DNL HL7 FHIR Release 5] erstellt wurden.

| Name | Beschreibung |
| --- | --- |
| [[!UICONTROL Address]](./data-types/address.md) | Beschreibt eine Adresse, die mithilfe von Postkonventionen (im Gegensatz zu GPS oder anderen Standortdefinitionsformaten) ausgedrückt wird. |
| [[!UICONTROL Annotation]](./data-types/annotation.md) | Ein Textknoten mit Zuordnung zum Autor. |
| [[!UICONTROL Availability]](./data-types/availability.md) | Verfügbarkeitsdaten für ein Element. |
| [[!UICONTROL Codeable Concept]](./data-types/codeable-concept.md) | Ein Verweis von einer Ressource auf eine andere. |
| [[!UICONTROL Codeable Reference]](./data-types/codeable-reference.md) | Ein Verweis auf eine Ressource oder ein Konzept. |
| [[!UICONTROL Coding]](./data-types/coding.md) | Ein Verweis auf einen Code, der von einem Terminologiesystem definiert wird. |
| [[!UICONTROL Contact Point]](./data-types/contact-point.md) | Kontaktdaten für eine Person. |
| [[!UICONTROL Dosage]](./data-types/dosage.md) | Wie das Arzneimittel eingenommen wurde/wurde oder eingenommen werden sollte. |
| [[!UICONTROL Duration]](./data-types/duration.md) | Ein langer Zeitraum. |
| [[!UICONTROL Extended Contact Details]](./data-types/extended-contact-detail.md) | Die Informationen eines erweiterten Kontakts. |
| [[!UICONTROL Human Name]](./data-types/human-name.md) | Informationen über den Namen eines Menschen oder einer anderen lebenden Entität. |
| [[!UICONTROL Identifier]](./data-types/identifier.md) | Ein Bezeichner, der für Berechnungen vorgesehen ist. |
| [[!UICONTROL Money]](./data-types/money.md) | Ein wirtschaftlicher Nutzen in einer anerkannten Währung. |
| [[!UICONTROL Period]](./data-types/period.md) | Ein Zeitraum, der durch ein Start- und Enddatum/-uhrzeit definiert wird. |
| [[!UICONTROL Person]](./data-types/person.md) | Informationen zu einem generischen Personendatensatz. |
| [[!UICONTROL Quantity]](./data-types/quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Range]](./data-types/range.md) | Ein Satz von Werten, die durch niedrige und hohe Werte gebunden sind. |
| [[!UICONTROL Ratio]](./data-types/ratio.md) | Ein Verhältnis von zwei [[!UICONTROL Quantity]](./data-types/quantity.md) durch einen Zähler und einen Nenner. |
| [[!UICONTROL Reference]](./data-types/reference.md) | Ein Verweis von einer Ressource auf eine andere. |
| [[!UICONTROL Repeat]](./data-types/repeat.md) | Ein Regelsatz, der beschreibt, wann ein Ereignis geplant ist. |
| [[!UICONTROL Simple Quantity]](./data-types/simple-quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Timing]](./data-types/timing.md) | Informationen zu einem Ereignis, das mehrmals auftreten kann. |
| [[!UICONTROL Virtual Service Detail]](./data-types/virtual-service-detail.md) | Kontaktinformationen für den virtuellen Dienst. |

