---
title: Gesundheitsdatenmodell V2
description: Erfahren Sie mehr über einige häufige Anwendungsfälle für das Gesundheitswesen und die besten Klassen, die zugehörigen Feldgruppen und Datentypen, die verwendet werden sollten.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 4d4e68376af914fbfcb005ad950e643f9407ad47
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 16%

---

# [!UICONTROL Healthcare] Datenmodell V2

## Feldergruppen und Klassen {#field-groups}

In der folgenden Tabelle werden die empfohlenen Klassen und Schemafeldgruppen für verschiedene gängige Anwendungsfälle der Gesundheitsfürsorge beschrieben.

<table>
  <thead>
    <tr>
      <th>Anwendungsfälle</th>
      <th>Feldergruppen</th>
      <th>Kompatible Klassen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Patienten erstellen/aktualisieren</strong>: Wenn ein Patient an der Krankenhausfront ankommt, wird ein Patientendatensatz erstellt, der demografische Details wie eine Kennung (optional), den Namen des Patienten, das Geburtsdatum, das Geschlecht und seine Adresse enthält. Dies ist ein wichtiger Bestandteil der IT im Gesundheitswesen.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Impfung</strong>: Erleichterung des Impfprozesses, Verwaltung der Patientenimpfungsunterlagen und Integration von EMRs in Impfmanagementsysteme.</td>
      <td><a href="../field-groups/event/healthcare-immunization.md">Immunisierung</a></td>
      <td>
        <li><a href="../classes/experienceevent.md">XDM-Erlebnisereignis</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Standort</a></td>
      <td>
        <li><a href="../classes/location.md">Standort</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medizin</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Medikationskosten</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Mediationsanfrage</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Einhaltung nach der Behandlung</strong>: Motivieren Sie Patienten und Pflegekräfte, ihre Behandlungspläne abzuschließen und die Überweisungsraten zu reduzieren.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Standort</a></td>
      <td>
        <li><a href="../classes/location.md">Standort</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-care-plan.md">Pflegeplan</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-goal.md">Ziel</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Kundenerlebnis für Versicherungen</strong>: Verbesserung der digitalen Akquise und der Erfahrungen bei Verbrauchern, die für Versicherungen einkaufen. Zu den Beispielen gehören: 
        <li> Verstehen des Verbraucherverhaltens zum Senden von Werbe-E-Mails oder zielgerichteten Anzeigen von Drittanbietern an Personen, die auf Seiten zugreifen, die allgemeine Informationen enthalten (z. B. Pläne, Planungsnamen/Ebenen, Arzneimittel oder Wellness-Programme)
        </li> 
        <li> Versand von Impfstoffinformationen über Herzkrankheiten zur Sensibilisierung der Marke oder zur Aufforderung, Impfstoffe für Personen zu planen, die nach Informationen über Herzgesundheit und Impfstoff suchen.
        </li>
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/plan/healthcare-coverage.md">Reichweite</a></td>
      <td>
        <li><a href="../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-account.md">Konto</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Standort</a></td>
      <td>
        <li><a href="../classes/location.md">Standort</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medizin</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Medikationskosten</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Mediationsanfrage</a></td>
      <td>
        <li><a href="../classes/medication.md">Medizin</a></li>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Verbessertes Anbietererlebnis</strong>: Verwenden von Anbieterdaten aus dem EMR-System, um alternative Anbieter basierend auf Terminverfügbarkeit, Standort und Spezialität vorzuschlagen. <br> <br>Verbessern der Anbietersuche, um Ergebnisse mit der gewünschten Verfügbarkeit anzuzeigen, Überprüfen, ob der ausgewählte Anbieter Teil des Payor-Netzwerks ist, und Bereitstellen von Kostenschätzungen.
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Standort</a></td>
      <td>
        <li><a href="../classes/location.md">Standort</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-organization.md">Organisation</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-practioner.md">Anwendende</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-schedule.md">Zeitplan</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuelles XDM-Profil</a></li>
        <li><a href="../classes/provider.md">Anbieter</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Datentypen {#data-types}

In der folgenden Tabelle sind die gemäß den [!DNL HL7 FHIR Release 5] -Spezifikationen erstellten Datentypen aufgeführt.

| Name | Beschreibung |
| --- | --- |
| [[!UICONTROL Adresse]](../data-types/healthcare/address.md) | Beschreibt eine Adresse, die anhand von Postkonventionen ausgedrückt wird (im Gegensatz zu GPS oder anderen Standortdefinitionsformaten). |
| [[!UICONTROL Anmerkung]](../data-types/healthcare/annotation.md) | Ein Textknoten mit Attribution zum Autor. |
| [[!UICONTROL Verfügbarkeit]](../data-types/healthcare/availability.md) | Verfügbarkeitsdaten für einen Artikel. |
| [[!UICONTROL Codeable Concept]](../data-types/healthcare/codeable-concept.md) | Ein Verweis von einer Ressource zur anderen. |
| [[!UICONTROL Codeable Reference]](../data-types/healthcare/codeable-reference.md) | Ein Verweis auf eine Ressource oder ein Konzept. |
| [[!UICONTROL Kodierung]](../data-types/healthcare/coding.md) | Ein Verweis auf einen von einem Terminologiesystem definierten Code. |
| [[!UICONTROL Kontaktpunkt]](../data-types/healthcare/contact-point.md) | Kontaktinformationen für eine Person. |
| [[!UICONTROL Dosierung]](../data-types/healthcare/dosage.md) | Wie das Arzneimittel eingenommen wird/wurde oder eingenommen werden sollte. |
| [[!UICONTROL Dauer]](../data-types/healthcare/duration.md) | Eine Zeitdauer. |
| [[!UICONTROL Erweiterte Kontaktdetails]](../data-types/healthcare/extended-contact-detail.md) | Informationen eines erweiterten Kontakts. |
| [[!UICONTROL Menschenname]](../data-types/healthcare/human-name.md) | Informationen über den Namen einer menschlichen oder anderen lebenden Entität. |
| [[!UICONTROL ID]](../data-types/healthcare/identifier.md) | Ein Bezeichner für die Berechnung. |
| [[!UICONTROL Money]](../data-types/healthcare/money.md) | Ein wirtschaftlicher Nutzen in einer anerkannten Währung. |
| [[!UICONTROL Zeitraum]](../data-types/healthcare/period.md) | Ein Zeitraum, der durch ein Start- und Enddatum/-zeit definiert wird. |
| [[!UICONTROL Person]](../data-types/healthcare/person.md) | Informationen zu einem generischen Personendatensatz. |
| [[!UICONTROL Quantity]](../data-types/healthcare/quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Bereich]](../data-types/healthcare/range.md) | Ein Satz von Werten, die durch niedrige und hohe Werte gebunden sind. |
| [[!UICONTROL Verhältnis]](../data-types/healthcare/ratio.md) | Ein Verhältnis von zwei [[!UICONTROL Quantity]](../data-types/healthcare/quantity.md) -Werten durch einen Zähler und einen Nenner. |
| [[!UICONTROL Referenz]](../data-types/healthcare/reference.md) | Ein Verweis von einer Ressource zur anderen. |
| [[!UICONTROL Wiederholen]](../data-types/healthcare/repeat.md) | Ein Regelsatz, der beschreibt, wann ein Ereignis geplant wird. |
| [[!UICONTROL Einfache Menge]](../data-types/healthcare/simple-quantity.md) | Ein gemessener oder messbarer Betrag. |
| [[!UICONTROL Timing]](../data-types/healthcare/timing.md) | Informationen zu einem Ereignis, das mehrmals auftreten kann. |
| [[!UICONTROL Virtual Service-Detail]](../data-types/healthcare/virtual-service-detail.md) | Kontaktdaten für den virtuellen Dienst. |
