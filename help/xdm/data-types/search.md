---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Suche;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp suchen
description: Erfahren Sie mehr über den Datentyp „Experience-Datenmodell (XDM) suchen“.
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 18%

---

# [!UICONTROL Suche] Datentyp

[!UICONTROL Suche] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zur Web-Suchaktivität enthält.

![Suchbild](../images/data-types/search.PNG){width=500}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `isPaid` | Boolesch | Wird verwendet, um anzugeben, ob die Suche gebührenpflichtig ist. |
| `keywords` | String | Die Suchbegriffe für die Suche. |
| `pageDepth` | Ganzzahl | Die Klicktiefe in den Suchergebnissen. |
| `position` | Ganzzahl | Die Position oder der Rang des Listeneintrags auf der Suchergebnisseite. |
| `searchEngine` | String | Die von der Suche verwendete Suchmaschine. |
| `searchEngineID` | String | Die anwendungsspezifische Kennung, die zur Identifizierung der Suchmaschine verwendet wird. |
| `slot` | String | Der benannte Abschnitt der Seite, auf der das Suchergebnis erschienen ist. Der Wert dieser Eigenschaft muss gleich einem der bekannten von Ihnen definierten Aufzählungswerte sein, z. B. `top`, `side` oder `bottom`. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
