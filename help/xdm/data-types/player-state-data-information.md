---
title: Datentyp "Player State Data Information"
description: Erfahren Sie mehr über den Datentyp Player State Data Information Experience Data Model (XDM) .
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 5%

---

# [!UICONTROL Player-Statusinformationen] Datentyp

[!UICONTROL Player-Statusinformationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die verschiedenen Status und deren Vorkommen in einem Medienplayer beschreibt. Verwenden Sie die [!UICONTROL Player-Statusinformationen] Datentyp , um verschiedene Player-Status zu erfassen, z. B. Vollbild, Stummschaltung, Untertitel, Bild-in-Bild und Fokusstatus. Für jeden Status wird aufgezeichnet, ob der Status festgelegt ist, die Anzahl der Vorkommen und die Gesamtdauer, die er während der Medienwiedergabe aktiv bleibt.

![Ein Diagramm des Datentyps Player-Statusdaten .](../images/data-types/player-state-data-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |
| [!UICONTROL Player-Statusset] | `isSet` | boolean | Gibt an, ob der Player-Status für diesen Status festgelegt ist. |
| [!UICONTROL Player-Statusanzahl] | `count` | integer | Die Häufigkeit, mit der der Player-Status im Stream festgelegt wurde. |
| [!UICONTROL Player-Statuszeit] | `time` | integer | Die Gesamtdauer dieses Player-Status. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
