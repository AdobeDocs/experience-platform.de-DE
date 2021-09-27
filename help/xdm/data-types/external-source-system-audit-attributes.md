---
title: Datentyp der externen Quell-System-Prüfattribute
description: Dieses Dokument bietet einen Überblick über den Datentyp "External Source System Audit Attributes Experience Data Model (XDM)".
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 6%

---

# [!UICONTROL Datentyp &quot;External Source System Audit ] Attributes&quot;

>[!NOTE]
>
>Dieser Datentyp ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition der Echtzeit-Kundendatenplattform haben.

[!UICONTROL Die ] Audit-Eigenschaft des externen Quellsystems ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der Prüfdetails zu einem externen Quellsystem erfasst.

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

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
