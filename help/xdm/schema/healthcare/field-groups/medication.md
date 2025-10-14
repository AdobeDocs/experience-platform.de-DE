---
title: Feldergruppe „Medikationsschema“
description: Erfahren Sie mehr über die Feldergruppe des Medikationsschemas.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 7%

---

# [!UICONTROL Medizin] Schemafeldgruppe

[!UICONTROL Medizin] ist eine Standardschemafeldgruppe für die Klasse [[!DNL Medication] &#x200B;](../../../classes/medication.md). Es bietet ein einzelnes Objekttyp-Feld, `healthcareMedication` die Informationen einer Medikation erfasst.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/medication/medication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| ---|  --- | --- | --- |
| [!UICONTROL Batch] | `batch` | Objekt | Details zu einem verpackten Medikament. Enthält zwei Eigenschaften: <li>`lotNumber`: Ein Zeichenfolgenwert für die Kennung, die dem Batch zugewiesen wurde.</li> <li>`expirationDate`: Ein DateTime-Wert für den Zeitpunkt, zu dem der Batch abläuft.</li> |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Code, der dieses Medikament identifiziert. |
| [!UICONTROL Definition] | `definition` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Definition der Medikation. |
| [!UICONTROL Dosierungsform] | `doseForm` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschreibt die Darreichungsform des Arzneimittels, z. B. Tabletten oder Kapseln. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine Kennung für das Medikament. |
| [!UICONTROL Zutat] | `ingredient` | Array von Objekten | Beschreibt die Inhaltsstoffinformationen für das Medikament. Weitere Informationen finden [&#x200B; im &#x200B;](#ingredient) Abschnitt unten. |
| [!UICONTROL PHARMAZEUTISCHER UNTERNEHMER] | `marketingAuthorizationHolder` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die über die Genehmigung für das Inverkehrbringen des Arzneimittels verfügt. |
| [!UICONTROL Gesamtvolumen] | `totalVolume` | [[!UICONTROL Menge]](../data-types/quantity.md) | Die Produktmenge, die in dem Medikament bereitgestellt wird, wenn der Produktcode keine Paketgröße ableitet. |
| [!UICONTROL Status] | `status` | String | Der Status des Medikaments. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Struktur der Inhaltsstoffe](../../../images/healthcare/field-groups/medication/ingredient.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Element] | `item` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Die Zutat, die beschrieben wird. |
| [!UICONTROL Strength codierbares Konzept] | `strengthCodeableConcept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Menge des Inhaltsstoffs, ausgedrückt in einer systemdefinierten Terminologie. |
| [!UICONTROL Festigkeitsmenge] | `strengthQuantity` | [[!UICONTROL Menge]](../data-types/quantity.md) | Die Menge der vorhandenen Zutat. |
| [!UICONTROL Festigkeitsverhältnis] | `strengthRatio` | [[!UICONTROL Verhältnis]](../data-types/ratio.md) | Das Verhältnis der vorhandenen Zutat. |
| [!UICONTROL Ist aktiv] | `isActive` | Boolesch | Zeigt an, ob der Inhaltsstoff aktiv ist. |
