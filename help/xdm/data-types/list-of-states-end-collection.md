---
title: Liste der Status Ende der Sammlungsdatentyp
description: Erfahren Sie mehr über den Datentyp "List of States End Collection Data Type Experience Data Model (XDM)".
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Liste der Statusenden] Datentyp

Der Datentyp Liste der Daten vom Typ &quot;State End Collection&quot;ist ein Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Endstatus verschiedener Player-Attribute darstellt. Er enthält die [!UICONTROL Player-Statusname] -Eigenschaften, die den jeweiligen Attributstatus angeben (z. B. &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dieser Datentyp wird zum Erfassen und Beschreiben der anfänglichen Bedingungen verschiedener Player-Status verwendet.

![Ein Diagramm des Datentyps Liste der Status Ende-Sammlung .](../images/data-types/list-of-states-end-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |

{style="table-layout:auto"}
