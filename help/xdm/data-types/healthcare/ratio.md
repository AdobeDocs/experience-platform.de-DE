---
title: Verhältnis-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Ratio Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# Datentyp [!UICONTROL Verhältnis]

[!UICONTROL Verhältnis] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der über einen Zähler und einen Nenner ein Verhältnis von zwei [[!UICONTROL Quantity]](../healthcare/quantity.md) -Werten liefert. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Ratio-Datentyps](../../images/data-types/healthcare/ratio.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Einfache Menge]](../healthcare/simple-quantity.md) | Der Wert des Nenners. |
| [!UICONTROL Zähler] | `numerator` | [[!UICONTROL Quantity]](../healthcare/quantity.md) | Der Wert des Zählers. |

>[!NOTE]
>
> Die `denominator` und `numerator` weisen aufgrund der gemäß HL7 FHIR Release 5 erstellten Spezifikation unterschiedliche Datentypen auf.

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
