---
title: Liste der Status Start Collection Datentyp
description: Erfahren Sie mehr über den Datentyp Liste der Startstatus des Datentyps Experience-Datenmodell (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# [!UICONTROL List of States Start] Datentyp

Der [!UICONTROL List of States Start] Datentyp ist ein Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Startstatus verschiedener Player-Attribute darstellt. Sie enthält die [!UICONTROL Player State Name] Eigenschaften, die den spezifischen Attributstatus angeben (z. B. „fullscreen“, „mute“, „closedCaptioning„). Dieser Datentyp wird verwendet, um die Anfangsbedingungen verschiedener Player-Status zu erfassen und zu beschreiben.

![Ein Diagramm [!UICONTROL List of States Start] Datentyps.](../images/data-types/list-of-states-start-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Nein | Der Name des Player-Status. Aufgezählt: „fullscreen“, „mute“, „closedCaptioning“, „pictureInPicture“, „inFocus“ mit jeweiligen Bedeutungen. |

{style="table-layout:auto"}
