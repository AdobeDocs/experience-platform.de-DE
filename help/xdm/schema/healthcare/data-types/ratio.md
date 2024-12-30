---
title: Datentyp „Verhältnis“
description: Erfahren Sie mehr über den Datentyp Ratio Experience-Datenmodell (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Verhältnis] Datentyp

[!UICONTROL Ratio] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der ein Verhältnis von zwei [[!UICONTROL Quantity]](../data-types/quantity.md)-Werten über einen Zähler und einen Nenner bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Verhältnis“](../../../images/healthcare/data-types/ratio.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Nenner] | `denominator` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Der Wert des Nenners. |
| [!UICONTROL Zähler] | `numerator` | [[!UICONTROL Menge]](../data-types/quantity.md) | Der Wert des Zählers. |

>[!NOTE]
>
> `denominator` und `numerator` haben aufgrund der Spezifikation, die gemäß HL7 FHIR Release 5 erstellt wurde, unterschiedliche Datentypen.

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
