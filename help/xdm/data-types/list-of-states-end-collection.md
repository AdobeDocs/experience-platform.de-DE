---
title: Datentyp für das Ende der Datenerfassung in Status
description: Erfahren Sie mehr über den Datentyp „Liste der Status - End-Datenerfassung“ Experience-Datenmodell (XDM) .
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Liste der Status Ende] Datentyp

Der Datentyp List of States End Collection ist ein Datentyp des Experience-Datenmodells (XDM), der Informationen zum Endstatus verschiedener Player-Attribute darstellt. Sie enthält die Eigenschaften [!UICONTROL Player State Name], die den spezifischen Attributstatus angeben (z. B. „fullscreen“, „mute“, „closedCaptioning„). Dieser Datentyp wird verwendet, um die Anfangsbedingungen verschiedener Player-Status zu erfassen und zu beschreiben.

![Ein Diagramm mit dem Datentyp „Liste der Status - Enderfassung“.](../images/data-types/list-of-states-end-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufgezählt: „fullscreen“, „mute“, „closedCaptioning“, „pictureInPicture“, „inFocus“ mit jeweiligen Bedeutungen. |

{style="table-layout:auto"}
