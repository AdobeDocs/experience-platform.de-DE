---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Suche; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Suchdatentyp
description: Erfahren Sie mehr über den Datentyp "Search Experience Data Model"(XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 18%

---

# [!UICONTROL Suche] Datentyp

[!UICONTROL Suche] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zur Web-Suchaktivität enthält.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `isPaid` | Boolesch | Wird verwendet, um anzugeben, ob die Suche bezahlt wurde oder nicht. |
| `keywords` | Zeichenfolge | Die Suchbegriffe für die Suche. |
| `pageDepth` | Ganzzahl | Die Klicktiefe in den Suchergebnissen. |
| `position` | Ganzzahl | Die Position oder der Rang der Auflistung auf der Suchergebnisseite. |
| `searchEngine` | Zeichenfolge | Die von der Suche verwendete Suchmaschine. |
| `searchEngineID` | Zeichenfolge | Die anwendungsspezifische Kennung, die zur Identifizierung der Suchmaschine verwendet wird. |
| `slot` | Zeichenfolge | Der benannte Abschnitt der Seite, auf der das Suchergebnis angezeigt wurde. Der Wert dieser Eigenschaft muss einem der bekannten Enum-Werte entsprechen, die Sie definieren, z. B. `top`, `side`oder `bottom`. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
