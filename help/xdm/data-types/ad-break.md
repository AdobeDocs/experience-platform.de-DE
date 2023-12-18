---
title: Datentyp der Werbeunterbrechung
description: Erfahren Sie mehr über den Datentyp "Ad Break Experience Data Model (XDM)".
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 6%

---

# [!UICONTROL Werbeunterbrechung] Datentyp

[!UICONTROL Werbeunterbrechung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der beschreibt, wie eine zeitgesteuerte Anzeige in ein zeitgesteuertes Medienelement eingefügt wird.

![Datentypstruktur](../images/data-types/ad-break.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc.title` | Zeichenfolge | Ein benutzerfreundlicher Name für die Werbeunterbrechung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für die Werbeunterbrechung. |
| `offset` | Ganzzahl | Der Versatz der Werbeunterbrechung ab Beginn des Hauptinhalts in Sekunden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
