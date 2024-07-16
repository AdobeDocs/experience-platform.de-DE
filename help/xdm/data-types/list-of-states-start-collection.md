---
title: Liste der Status Beginn der Datenerfassung
description: Erfahren Sie mehr über den Datentyp "List of States Start Data Type Experience Data Model (XDM)".
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Liste der Statusstartdatentypen ]

Der Datentyp [!UICONTROL Liste der Statusstarts] ist ein Experience-Datenmodell (XDM)-Datentyp, der dazu bestimmt ist, Informationen zum Startstatus verschiedener Player-Attribute darzustellen. Sie enthält die Eigenschaften [!UICONTROL Player-Statusname] , die den jeweiligen Attributstatus angeben (z. B. &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Dieser Datentyp wird zum Erfassen und Beschreiben der anfänglichen Bedingungen verschiedener Player-Status verwendet.

![Ein Diagramm des Datentyps [!UICONTROL Liste der Statusstarts].](../images/data-types/list-of-states-start-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player-Statusname] | `name` | Zeichenfolge | Nein | Der Name des Player-Status. Aufzählung: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; mit der jeweiligen Bedeutung. |

{style="table-layout:auto"}
