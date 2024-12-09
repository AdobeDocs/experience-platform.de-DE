---
title: Erweiterter Kontaktdetaildatentyp
description: Erfahren Sie mehr über den Datentyp "Extended Contact Detail Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 8%

---

# [!UICONTROL Erweiterter Datentyp &quot;Kontaktdetails&quot;]

[!UICONTROL Erweiterte Kontaktdetails] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der die Informationen eines erweiterten Kontakts beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![ Erweiterte Struktur der Kontaktinformationen-Datentypen](../../images/data-types/healthcare/extended-contact-detail.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../healthcare/address.md) | Die Adresse des Kontakts. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../healthcare/human-name.md) | Name(n) der Kontakt(en). |
| [!UICONTROL Organisation] | `organization` | [[!UICONTROL Referenz]](../healthcare/reference.md) | Die Organisation, die die Kontaktdaten verarbeitet/überwacht. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../healthcare/period.md) | Der Zeitraum, in dem der Kontakt für die Nutzung gültig ist oder war. |
| [!UICONTROL Zweck] | `purpose` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Die Art des Kontakts. |
| [!UICONTROL Telecom] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../healthcare/contact-point.md) | Die Kontaktdaten. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
