---
title: Dosierungstyp
description: Erfahren Sie mehr über den Datentyp Dosierung - Experience-Datenmodell (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!UICONTROL Dosierung] Datentyp

[!UICONTROL Dosierung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der beschreibt, wie das Medikament eingenommen wird/wurde oder eingenommen werden sollte. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Dosierung](../../../images/healthcare/data-types/dosage/dosage.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zusätzliche Anweisungen] | `additionalInstruction` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Zusätzliche Anweisungen oder Warnhinweise für den Patienten. |
| [!UICONTROL nach Bedarf für] | `asNeededFor` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschreibt, für welches Problem das Medikament nach Bedarf eingenommen werden sollte. |
| [!UICONTROL Dosis und Geschwindigkeit] | `doseAndRate` | Array von Objekten | Die Menge des zu verabreichenden oder zu verabreichenden Arzneimittels oder die typische zu verabreichende Menge. Weitere Informationen finden [ im ](#dose-and-rate) Abschnitt unten |
| [!UICONTROL Max. Dosis pro Anwendung] | `maxDosePerAdministration` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Obergrenze der Medikation pro Verabreichung. |
| [!UICONTROL Max. Dosis pro Lebensdauer] | `maxDosePerLifetime` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Obergrenze der Medikation pro Lebensdauer des Patienten. |
| [!UICONTROL Max. Dosis pro Zeitraum] | `maxDosePerPeriod` | Array von [[!UICONTROL Ratio]](../data-types/ratio.md) | Die Obergrenze der Medikation pro Zeiteinheit. |
| [!UICONTROL Methode] | `method` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Technik zur Verabreichung von Medikamenten. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Wie das Medikament in den Körper eintreten soll. |
| [!UICONTROL Körperseite] | `site` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Körperstelle, an der das Medikament verabreicht wird. |
| [!UICONTROL Timing] | `timing` | [[!UICONTROL Timing]](../data-types/timing.md) | Wann die Medikation verabreicht werden sollte. |
| [!UICONTROL nach Bedarf] | `asNeeded` | Boolesch | Ein Indikator dafür, ob das Medikament bei Bedarf eingenommen werden sollte. |
| [!UICONTROL Patientenanweisungen] | `patientInstruction` | String | Anweisungen in Begriffen, die vom Patienten oder Verbraucher zu verstehen sind. |
| [!UICONTROL Sequenz] | `Integer` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Reihenfolge der Dosierungsanweisungen. |
| [!UICONTROL Text] | `text` | String | Planungstext Dosierungsanweisungen. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Dosis- und Ratenstruktur](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Dosismenge] | `doseQuantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge des Arzneimittels pro Dosis. |
| [!UICONTROL Dosisbereich] | `doseRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Menge des Arzneimittels pro Dosis. |
| [!UICONTROL Mengensatz] | `rateQuantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Tarifbereich] | `rateRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Ratenverhältnis] | `rateRatio` | [[!UICONTROL Verhältnis]](../data-types/ratio.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Typ] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Art der angegebenen Dosis oder Geschwindigkeit. |
