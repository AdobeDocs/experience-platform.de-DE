---
title: Datentyp der Werbeunterbrechung
description: Erfahren Sie mehr über den Datentyp Ad Break Experience-Datenmodell (XDM).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 21%

---

# [!UICONTROL Anzeigenunterbrechung] Datentyp

[!UICONTROL Werbeunterbrechung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der beschreibt, wie eine zeitgesteuerte Anzeige in ein zeitgesteuertes Medium eingefügt wird.

![Datentypstruktur](../images/data-types/ad-break.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc.title` | Zeichenfolge | Anzeigename für die Werbeunterbrechung. |
| `_id` | String | Eine eindeutige Kennung für die Anzeigenunterbrechung. |
| `offset` | Ganzzahl | Der Versatz der Anzeigenunterbrechung vom Beginn des primären Inhalts in Sekunden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
