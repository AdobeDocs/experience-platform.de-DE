---
title: Verhältnis-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Ratio Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# Datentyp [!UICONTROL Verhältnis]

[!UICONTROL Verhältnis] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der über einen Zähler und einen Nenner ein Verhältnis von zwei [[!UICONTROL Quantity]](../data-types/quantity.md) -Werten liefert. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Ratio-Datentyps](../../../images/healthcare/data-types/ratio.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Der Wert des Nenners. |
| [!UICONTROL Zähler] | `numerator` | [[!UICONTROL Quantity]](../data-types/quantity.md) | Der Wert des Zählers. |

>[!NOTE]
>
> Die `denominator` und `numerator` weisen aufgrund der gemäß HL7 FHIR Release 5 erstellten Spezifikation unterschiedliche Datentypen auf.

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
