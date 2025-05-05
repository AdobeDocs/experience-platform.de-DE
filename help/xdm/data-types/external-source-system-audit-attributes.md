---
title: Datentyp der Audit-Attribute des externen Source-Systems
description: Erfahren Sie mehr über den Datentyp „External Source System Audit Attributes Experience Data Model (XDM)“.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# [!UICONTROL &#x200B; Datentyp „External Source System Audit &#x200B;]&quot;

[!UICONTROL External Source System Audit Attributes] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B-Source]](./b2b-source.md) | Eine zusammengesetzte Kennung für die Quelle, die für das Auditing verwendet wird. |
| `createdBy` | String | Der Name des Benutzers, der diesen Datensatz erstellt hat. |
| `createdDate` | DateTime | Das Datum, an dem dieser Datensatz erstellt wurde. |
| `externalID` | String | Externe eindeutige Kennung der Quelle. Dieser Wert wird verwendet, um bei Bedarf zu identifizieren und zu deduplizieren. |
| `lastActivityDate` | DateTime | Das Datum der letzten Aktivität für das Quellsystem. |
| `lastReferencedDate` | DateTime | Das Datum der letzten Referenz für das Quellsystem. |
| `lastUpdatedBy` | String | Der Name der Person, die diesen Datensatz zuletzt aktualisiert hat. |
| `lastUpdatedDate` | DateTime | Das Datum der letzten Aktualisierung für das Quellsystem. Dieser Wert wird von der [Attributzusammenführungsrichtlinie) verwendet](../../profile/api/merge-policies.md#attribute-merge) um die Priorität im Falle von Zusammenführungskonflikten zu bestimmen. |
| `lastViewedDate` | DateTime | Das Datum der letzten Anzeige für das Quellsystem. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
