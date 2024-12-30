---
title: Schemafeldgruppe planen
description: Erfahren Sie mehr über die Schemafeldgruppe „Zeitplan“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL Zeitplan] Schemafeldgruppe

[!UICONTROL Zeitplan] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es bietet ein einzelnes Objekttyp-Feld, `healthcareSchedule` ein Container für Zeitfenster ist, die für die Buchung von Terminen verfügbar sein können.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/schedule.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Schauspieler] | `actor` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die Zeitnischen, die auf diesen Zeitplan verweisen, mit Angabe der Verfügbarkeitsdetails für diese referenzierten Ressourcen. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Die externen Kennungen für den Zeitplan. |
| [!UICONTROL Planungshorizont] | `planningHorizon` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, den die Zeitnischen, die auf diesen Zeitplan verweisen, abdecken, selbst wenn keine vorhanden sind. |
| [!UICONTROL Service-Kategorie] | `serviceCategory` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Eine breite Kategorisierung des Dienstes, der während des Termins ausgeführt werden soll. |
| [!UICONTROL Service-Typ] | `serviceType` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Der spezifische Service, der während des Termins ausgeführt werden soll. |
| [!UICONTROL Fachgebiet] | `specialty` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Spezialität des Praktikers, die erforderlich wäre, um die im Termin angeforderte Dienstleistung zu erbringen. |
| [!UICONTROL aktiv] | `active` | Boolesch | Gibt an, ob der Zeitplan-Datensatz aktiv verwendet wird. |
| [!UICONTROL Kommentar] | `comment` | String | Kommentare zur Verfügbarkeit mit dem Ziel, erweiterte Informationen zu beschreiben, z. B. benutzerdefinierte Einschränkungen für die Slots. |
| [!UICONTROL Name] | `name` | String | Die Beschreibung des Zeitplans, wie er einem Verbraucher bei der Suche präsentiert werden würde. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
