---
title: Liste der Status Ende der Sammlungsdatentyp
description: Erfahren Sie mehr über den Datentyp "List of States End Collection Data Type Experience Data Model (XDM)".
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Liste der Statusenddaten ]

Der Datentyp Liste der Daten vom Typ &quot;State End Collection&quot;ist ein Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Endstatus verschiedener Player-Attribute darstellt. Sie enthält die Eigenschaften [!UICONTROL Player-Statusname] , die den jeweiligen Attributstatus angeben (z. B. &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dieser Datentyp wird zum Erfassen und Beschreiben der anfänglichen Bedingungen verschiedener Player-Status verwendet.

![Ein Diagramm des Datentyps Liste der Status Ende der Sammlung.](../images/data-types/list-of-states-end-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |

{style="table-layout:auto"}
