---
title: Datentyp der externen Quell-System-Prüfattribute
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM)"der Audit-Attribute des externen Quellsystems.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---

# [!UICONTROL Audit-Attribute des externen Quellsystems] Datentyp

[!UICONTROL Audit-Attribute des externen Quellsystems] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B-Quelle]](./b2b-source.md) | Eine zusammengesetzte Kennung für die für die Prüfung verwendete Quelle. |
| `createdBy` | Zeichenfolge | Der Name des Benutzers, der diesen Datensatz erstellt hat. |
| `createdDate` | DateTime | Das Datum der Erstellung dieses Datensatzes. |
| `externalID` | Zeichenfolge | Externe eindeutige Kennung für die Quelle. Dieser Wert hilft bei der Identifizierung und Deduplizierung bei Bedarf. |
| `lastActivityDate` | DateTime | Das letzte Aktivitätsdatum für das Quellsystem. |
| `lastReferencedDate` | DateTime | Das letzte referenzierte Datum für das Quellsystem. |
| `lastUpdatedBy` | Zeichenfolge | Der Name der Person, die diesen Datensatz zuletzt aktualisiert hat. |
| `lastUpdatedDate` | DateTime | Das letzte aktualisierte Datum für das Quellsystem. |
| `lastViewedDate` | DateTime | Das letzte angezeigte Datum für das Quellsystem. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
