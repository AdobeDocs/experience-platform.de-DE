---
title: Datentyp der Werbeunterbrechung
description: Dieses Dokument bietet einen Überblick über den Datentyp "Ad Break Experience Data Model (XDM)".
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 17%

---

# [!UICONTROL Werbeunterbrechung] Datentyp

[!UICONTROL Werbeunterbrechung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der beschreibt, wie eine zeitgesteuerte Anzeige in ein zeitgesteuertes Medienelement eingefügt wird.

![Datentypstruktur](../images/data-types/ad-break.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc.title` | Zeichenfolge | Ein benutzerfreundlicher Name für die Werbeunterbrechung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für die Werbeunterbrechung. |
| `offset` | Ganzzahl | Der Versatz der Werbeunterbrechung ab Beginn des Hauptinhalts in Sekunden. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
