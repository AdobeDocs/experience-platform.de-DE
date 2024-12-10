---
title: Schemafeldgruppe planen
description: Erfahren Sie mehr über die Feldergruppe Schema planen .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL Schema] Schemafeldgruppe

[!UICONTROL Zeitplan] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es stellt ein einzelnes Objektfeld `healthcareSchedule` bereit, das einen Container für Zeitfenster darstellt, die für Buchungstermine verfügbar sein können.

![Feldgruppenstruktur](../../../images/healthcare/field-groups/schedule.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Akteur] | `actor` | Array von [[!UICONTROL Verweis]](../data-types/reference.md) | Die Slots, die auf diesen Zeitplan verweisen und die Verfügbarkeitsdetails für diese referenzierten Ressourcen angeben. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../data-types/identifier.md) | Die externen Kennungen für den Zeitplan. |
| [!UICONTROL Planungshorizont] | `planningHorizon` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, für den die Zeitnischen, die auf diesen Zeitplan verweisen, gelten, selbst wenn keine Zeitnischen vorhanden sind. |
| [!UICONTROL Dienstkategorie] | `serviceCategory` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Eine umfassende Kategorisierung des Dienstes, der während der Bestellung auszuführen ist. |
| [!UICONTROL Diensttyp] | `serviceType` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Der besondere Dienst, der während der Bestellung ausgeführt werden soll. |
| [!UICONTROL Spezialität] | `specialty` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Spezialität des Praktikanten, die für die Durchführung der in der Ernennung angeforderten Dienstleistung erforderlich wäre. |
| [!UICONTROL Aktiv] | `active` | Boolesch | Gibt an, ob der Plandatensatz aktiv verwendet wird. |
| [!UICONTROL Kommentar] | `comment` | String | Kommentare zur Verfügbarkeit mit dem Ziel, alle erweiterten Informationen zu beschreiben, z. B. benutzerdefinierte Einschränkungen für die Slots. |
| [!UICONTROL Name] | `name` | String | Die Beschreibung des Zeitplans, wie er einem Verbraucher bei der Suche angezeigt würde. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
