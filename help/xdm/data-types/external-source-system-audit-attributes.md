---
title: Datentyp der externen Quell-System-Prüfattribute
description: Dieses Dokument bietet einen Überblick über den Datentyp "External Source System Audit Attributes Experience Data Model (XDM)".
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 13%

---

# [!UICONTROL Audit-Attribute des externen Quellsystems] Datentyp

>[!NOTE]
>
>Dieser Datentyp ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition von Adobe Real-time Customer Data Platform haben.

[!UICONTROL Audit-Attribute des externen Quellsystems] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B-Quelle]](./b2b-source.md) | Eine zusammengesetzte Kennung für die Quelle, die für die Prüfung verwendet wird. |
| `createdBy` | Zeichenfolge | Der Name des Benutzers, der diesen Datensatz erstellt hat. |
| `createdDate` | DateTime | Das Datum, an dem dieser Datensatz erstellt wurde. |
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
