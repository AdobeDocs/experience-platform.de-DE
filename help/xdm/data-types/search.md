---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Suche;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp suchen
topic: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Sucherlebnis-Datenmodells (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 16%

---


#  SearchData-Typ

 Search ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der Informationen zur Aktivität der Websuche enthält.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `isPaid` | Boolesch | Wird verwendet, um anzugeben, ob die Suche bezahlt wurde oder nicht. |
| `keywords` | Zeichenfolge | Die Suchbegriffe für die Suche. |
| `pageDepth` | Ganzzahl | Die Klicktiefe in den Suchergebnissen. |
| `position` | Ganzzahl | Die Position oder der Rang der Auflistung auf der Suchergebnisseite. |
| `searchEngine` | Zeichenfolge | Die von der Suche verwendete Suchmaschine. |
| `searchEngineID` | Zeichenfolge | Der anwendungsspezifische Bezeichner, der zur Identifizierung der Suchmaschine verwendet wird. |
| `slot` | Zeichenfolge | Der benannte Abschnitt der Seite, auf der das Suchergebnis angezeigt wurde. Der Wert dieser Eigenschaft muss mit einem der bekannten Enum-Werte übereinstimmen, die Sie definieren, z. B. `top`, `side` oder `bottom`. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)