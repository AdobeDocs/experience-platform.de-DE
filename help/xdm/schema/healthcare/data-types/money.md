---
title: Gelddatentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Money Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# Datentyp [!UICONTROL Money]

[!UICONTROL Money] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der in einer anerkannten Währung einen wirtschaftlichen Nutzen bietet. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Geldtyps](../../../images/healthcare/data-types/money.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Währung] | `currency` | String | Der ISO 4217-Währungscode. |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
