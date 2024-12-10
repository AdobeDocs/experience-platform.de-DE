---
title: Erweiterter Kontaktdetaildatentyp
description: Erfahren Sie mehr über den Datentyp "Extended Contact Detail Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 8%

---

# [!UICONTROL Erweiterter Datentyp &quot;Kontaktdetails&quot;]

[!UICONTROL Erweiterte Kontaktdetails] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der die Informationen eines erweiterten Kontakts beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![ Erweiterte Struktur der Kontaktinformationen-Datentypen](../../../images/healthcare/data-types/extended-contact-detail.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../data-types/address.md) | Die Adresse des Kontakts. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../data-types/human-name.md) | Name(n) der Kontakt(en). |
| [!UICONTROL Organisation] | `organization` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die die Kontaktdaten verarbeitet/überwacht. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Kontakt für die Nutzung gültig ist oder war. |
| [!UICONTROL Zweck] | `purpose` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Art des Kontakts. |
| [!UICONTROL Telecom] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../data-types/contact-point.md) | Die Kontaktdaten. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
