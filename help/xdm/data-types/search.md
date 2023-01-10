---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Suche; Datentyp; Datentyp; Datentyp; Datentyp
solution: Experience Platform
title: Suchdatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Search Experience Data Model (XDM)".
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 25%

---

# [!UICONTROL Suche] Datentyp

[!UICONTROL Suche] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zur Web-Suchaktivität enthält.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `isPaid` | Boolesch | Wird verwendet, um anzugeben, ob die Suche gebührenpflichtig ist oder nicht. |
| `keywords` | Zeichenfolge | Die Suchbegriffe für die Suche. |
| `pageDepth` | Ganzzahl | Die Klicktiefe in den Suchergebnissen. |
| `position` | Ganzzahl | Die Position oder der Rang der Auflistung auf der Suchergebnisseite. |
| `searchEngine` | Zeichenfolge | Die von der Suche verwendete Suchmaschine. |
| `searchEngineID` | Zeichenfolge | Die anwendungsspezifische Kennung, die zur Identifizierung der Suchmaschine verwendet wird. |
| `slot` | Zeichenfolge | Der benannte Abschnitt der Seite, auf der das Suchergebnis angezeigt wurde. Der Wert dieser Eigenschaft muss mit einem der bekannten Enum-Werte übereinstimmen, die Sie definieren, z. B. `top`, `side`oder `bottom`. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
