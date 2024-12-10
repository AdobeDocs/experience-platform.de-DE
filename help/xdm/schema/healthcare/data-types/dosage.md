---
title: Dosierungsdatentyp
description: Erfahren Sie mehr über den Datentyp des Dosierung Experience-Datenmodells (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!UICONTROL Dosierung]-Datentyp

[!UICONTROL Dosierung] ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der beschreibt, wie die Medikation eingenommen wird/eingenommen wurde oder eingenommen werden sollte. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Dosierungsdatentyps](../../../images/healthcare/data-types/dosage/dosage.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zusätzliche Anweisungen] | `additionalInstruction` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Zusätzliche Hinweise oder Warnhinweise für den Patienten. |
| [!UICONTROL Wie für ] erforderlich | `asNeededFor` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschreibt die Frage, für die das Arzneimittel nach Bedarf eingenommen werden sollte. |
| [!UICONTROL Dosis und Rate] | `doseAndRate` | Array von Objekten | Die Menge der verabreichten Medikamente, die verabreicht werden sollen, oder die typische Menge, die verabreicht werden soll. Weitere Informationen finden Sie im Abschnitt [unter ](#dose-and-rate) . |
| [!UICONTROL Max. Dosis pro Anwendung] | `maxDosePerAdministration` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die obere Grenze der Medikation pro Verabreichung. |
| [!UICONTROL Max. Dosis pro Lebensdauer] | `maxDosePerLifetime` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die obere Grenze der Medikation pro Lebensdauer des Patienten. |
| [!UICONTROL Max. Dosis pro Zeitraum] | `maxDosePerPeriod` | Array von [[!UICONTROL Ratio]](../data-types/ratio.md) | Die obere Grenze der Medikation pro Zeiteinheit. |
| [!UICONTROL Methode] | `method` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Technik zur Verabreichung von Arzneimitteln. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Wie das Medikament in den Körper gelangen soll. |
| [!UICONTROL Textkörper-Site] | `site` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Körperstelle, an der das Medikament verabreicht wird. |
| [!UICONTROL Timing] | `timing` | [[!UICONTROL Timing]](../data-types/timing.md) | Wann die Medikation verabreicht werden sollte. |
| [!UICONTROL Nach Bedarf] | `asNeeded` | Boolesch | Ein Indikator dafür, ob das Arzneimittel nach Bedarf eingenommen werden sollte. |
| [!UICONTROL Patientenanweisungen] | `patientInstruction` | String | Anweisungen in Begriffen, die vom Patienten oder Verbraucher zu verstehen sind. |
| [!UICONTROL Sequenz] | `Integer` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Reihenfolge der Dosierungsanweisungen. |
| [!UICONTROL Text] | `text` | String | Planen Sie Anweisungen zur Textdosierung. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Struktur der Dosis und Rate](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Dosismenge] | `doseQuantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge der Medikamente pro Dosis. |
| [!UICONTROL Dosisbereich] | `doseRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Menge der Medikamente pro Dosis. |
| [!UICONTROL Rate Quantity] | `rateQuantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Ratenbereich] | `rateRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Ratenverhältnis] | `rateRatio` | [[!UICONTROL Verhältnis]](../data-types/ratio.md) | Die Menge der Medikation pro Zeiteinheit. |
| [!UICONTROL Typ] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Art der angegebenen Dosis oder Rate. |
