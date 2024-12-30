---
title: Speicherort-Schemafeldgruppe
description: Erfahren Sie mehr über die Feldgruppe des Standortschemas.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# [!UICONTROL Speicherort] Schemafeldgruppe

[!UICONTROL Location] ist eine standardmäßige Schemafeldgruppe für die [[!DNL Location] class](../classes/location.md). Es bietet ein einzelnes Feld vom Typ „Objekt“, `healthcareLocation` Details und Positionsinformationen für einen Ort erfasst.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/location.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../data-types/address.md) | Die Adresse des physischen Standorts. |
| [!UICONTROL Merkmal] | `characteristic` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Eine Sammlung der Standortmerkmale. |
| [!UICONTROL Kontakt] | `contact` | Array von [[!UICONTROL erweiterten Kontaktdetails]](../data-types/extended-contact-detail.md) | Die Kontaktdetails für den Standort. |
| [!UICONTROL Endpunkt] | `endpoint` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die technischen Endpunkte, die Zugriff auf Betriebsdienste für den Standort bieten. |
| [!UICONTROL Formular] | `form` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die physische Form des Standorts. |
| [!UICONTROL Betriebsstunden] | `hoursOfOperation` | Array von [[!UICONTROL Verfügbarkeit]](../data-types/availability.md) | An welchen Tagen und zu welchen Zeiten dieser Ort normalerweise geöffnet ist (einschließlich Ausnahmen). |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Der eindeutige Code oder die Nummer, die den Standort identifiziert. |
| [!UICONTROL Organisation verwalten] | `managingOrganization` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die für Bereitstellung und Wartung verantwortlich ist. |
| [!UICONTROL Betriebsstatus] | `operationalStatus` | [[!UICONTROL Kodierung]](../data-types/coding.md) | Der Betriebsstatus für den Standort. |
| [!UICONTROL Teil des Standorts] | `partOf` | [[!UICONTROL Referenz]](../data-types/reference.md) | Der Speicherort, zu dem dieser Speicherort gehört. |
| [!UICONTROL Position] | `position` | Objekt | Die absolute geografische Lage. Enthält drei Eigenschaften im Doppelformat: <li>`longitude`: Längengrad mit WGS84-Datum</li> <li>`latitude`: Latitude mit WGS84-Datum.</li> <li>`altitude`: Höhe mit WGS84-Datum.</li> |
| [!UICONTROL Typ] | `type` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Typ der am Standort ausgeführten Funktion. |
| [!UICONTROL Virtueller Service] | `virtualService` | Array von [[!UICONTROL Virtual Service Detail]](../data-types/virtual-service-detail.md) | Die Verbindungsdetails eines virtuellen Services. |
| [!UICONTROL Alias] | `alias` | Zeichenfolgen-Array | Eine Liste mit alternativen Namen, unter denen der Speicherort angegeben ist oder bekannt war. |
| [!UICONTROL Beschreibung] | `description` | String | Weitere Informationen zur Identifizierung des Standorts über seinen Namen hinaus. |
| [!UICONTROL Modus] | `mode` | String | Der Modus des Standorts. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Name] | `name` | String | Der Name des Speicherorts. |
| [!UICONTROL Status] | `status` | String | Der Status des Standorts. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
