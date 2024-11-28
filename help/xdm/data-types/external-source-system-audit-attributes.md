---
title: Datentyp für externe Source-Systemprüfungsattribute
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM)"für externe Source-Systemaudit-Attribute.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# Datentyp [!UICONTROL Externe Source-Systemprüfungsattribute]

[!UICONTROL Externe Source-Systemprüfungsattribute] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B Source]](./b2b-source.md) | Eine zusammengesetzte Kennung für die für die Prüfung verwendete Quelle. |
| `createdBy` | String | Der Name des Benutzers, der diesen Datensatz erstellt hat. |
| `createdDate` | DateTime | Das Datum der Erstellung dieses Datensatzes. |
| `externalID` | String | Externe eindeutige Kennung für die Quelle. Dieser Wert hilft bei der Identifizierung und Deduplizierung bei Bedarf. |
| `lastActivityDate` | DateTime | Das letzte Aktivitätsdatum für das Quellsystem. |
| `lastReferencedDate` | DateTime | Das letzte referenzierte Datum für das Quellsystem. |
| `lastUpdatedBy` | String | Der Name der Person, die diesen Datensatz zuletzt aktualisiert hat. |
| `lastUpdatedDate` | DateTime | Das letzte aktualisierte Datum für das Quellsystem. Dieser Wert wird von der [Attributzusammenführungsrichtlinie ](../../profile/api/merge-policies.md#attribute-merge) verwendet, um die Priorität im Fall von Zusammenführungskonflikten zu bestimmen. |
| `lastViewedDate` | DateTime | Das letzte angezeigte Datum für das Quellsystem. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
