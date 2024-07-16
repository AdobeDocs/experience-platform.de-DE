---
title: Datentyp Player-Status
description: Erfahren Sie mehr über den Datentyp Player State Data Reporting Experience Data Model (XDM) .
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# Datentyp [!UICONTROL Player-Statusdaten - Berichterstellung]

[!UICONTROL Player-Statusdatenberichte] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die verschiedenen Status und deren Vorkommen in einem Medienplayer beschreibt. Verwenden Sie den Datentyp [!UICONTROL Player-Statusdaten-Reporting] , um verschiedene Player-Status zu erfassen, z. B. Vollbild, Stummschaltung, verdeckte Untertitel, Bild-in-Bild-Status und Fokusstatus. Für jeden Status wird aufgezeichnet, ob der Status festgelegt ist, die Anzahl der Vorkommen und die Gesamtdauer, die er während der Medienwiedergabe aktiv bleibt.

![Ein Diagramm des Datentyps Player-Statusdaten-Berichterstellung.](../images/data-types/player-state-data-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |
| [!UICONTROL Player-Status festgelegt] | `isSet` | Boolescher Wert | Gibt an, ob der Zustand des Players auf diesen Zustand eingestellt ist oder nicht. |
| [!UICONTROL Player-Statusanzahl] | `count` | integer | Gibt an, wie oft der Player-Status im Stream gesetzt wurde. |
| [!UICONTROL Player-Statuszeit] | `time` | integer | Die Gesamtdauer dieses Player-Zustands. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
