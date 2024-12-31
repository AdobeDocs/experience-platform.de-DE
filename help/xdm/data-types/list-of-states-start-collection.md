---
title: Liste der Status Start Collection Datentyp
description: Erfahren Sie mehr über den Datentyp Liste der Startstatus des Datentyps Experience-Datenmodell (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Liste der Status Start] Datentyp

Der [!UICONTROL Start-Liste]-Datentyp ist ein Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Startstatus verschiedener Player-Attribute darstellt. Sie enthält die Eigenschaften [!UICONTROL Player State Name], die den spezifischen Attributstatus angeben (z. B. „fullscreen“, „mute“, „closedCaptioning„). Dieser Datentyp wird verwendet, um die Anfangsbedingungen verschiedener Player-Status zu erfassen und zu beschreiben.

![Ein Diagramm vom [!UICONTROL Liste der Status Start] Datentyp.](../images/data-types/list-of-states-start-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufgezählt: „fullscreen“, „mute“, „closedCaptioning“, „pictureInPicture“, „inFocus“ mit jeweiligen Bedeutungen. |

{style="table-layout:auto"}
