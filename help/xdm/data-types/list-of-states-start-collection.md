---
title: Liste der Status Beginn der Datenerfassung
description: Erfahren Sie mehr über den Datentyp "List of States Start Data Type Experience Data Model (XDM)".
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Liste der Statusstarts] Datentyp

Die [!UICONTROL Liste der Statusstarts] -Datentyp ist ein Experience-Datenmodell (XDM)-Datentyp, der für die Darstellung von Informationen zum Startstatus verschiedener Player-Attribute entwickelt wurde. Er enthält die [!UICONTROL Player-Statusname] -Eigenschaften, die den jeweiligen Attributstatus angeben (z. B. &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dieser Datentyp wird zum Erfassen und Beschreiben der anfänglichen Bedingungen verschiedener Player-Status verwendet.

![Ein Diagramm [!UICONTROL Liste der Statusstarts] Datentyp.](../images/data-types/list-of-states-start-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |

{style="table-layout:auto"}
