---
title: Datentyp für Player-Statusberichte
description: Erfahren Sie mehr über den Datentyp des Player-Status-Datenberichts mit dem Experience-Datenmodell (XDM).
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# Datentyp [!UICONTROL Player-Status]Datenberichte)

[!UICONTROL Player State Data Reporting] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die verschiedenen Status und deren Vorkommen in einem Media-Player beschreibt. Verwenden Sie den [!UICONTROL Datentyp Player-Status], um verschiedene Player-Status wie Vollbild, Stummschaltung, Untertitel, Bild-in-Bild- und Fokusstatus zu erfassen. Für jeden Status wird aufgezeichnet, ob der Status festgelegt ist, die Anzahl der Vorfälle und die Gesamtdauer, während der er während der Medienwiedergabe aktiv bleibt.

![Abbildung des Datentyps für Player-Status-Datenberichte.](../images/data-types/player-state-data-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Der Name des Player-Status. Aufgezählt: „fullscreen“, „mute“, „closedCaptioning“, „pictureInPicture“, „inFocus“ mit jeweiligen Bedeutungen. |
| [!UICONTROL Player-Status festgelegt] | `isSet` | Boolescher Wert | Gibt an, ob der Zustand des Players auf diesen Zustand eingestellt ist oder nicht. |
| [!UICONTROL Player-Status-Anzahl] | `count` | integer | Gibt an, wie oft der Player-Status im Stream gesetzt wurde. |
| [!UICONTROL Player State Time] | `time` | integer | Die Gesamtdauer dieses Player-Zustands. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
