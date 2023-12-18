---
title: Datentyp "Commerce Scope"
description: Erfahren Sie mehr über den Datentyp Commerce Scope Experience Data Model (XDM) .
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Commerce-Umfang] Datentyp

[!UICONTROL Commerce-Umfang] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der IDs definiert, für die in einem Commerce-Ökosystem ein Ereignis aufgetreten ist. Sie unterscheidet Umgebungen, Websites, Stores und Store-Ansichten.

![Ein Diagramm des Datentyps Commerce Scope .](../images/data-types/commerce-scope.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Umgebungs-ID] | `environmentID` | Zeichenfolge | Die Umgebungs-ID. Eine 32-stellige alphanumerische ID. |
| [!UICONTROL Website-Code] | `websiteCode` | Zeichenfolge | Der eindeutige Website-Code in einer Umgebung. |
| [!UICONTROL Store-Code] | `storeCode` | Zeichenfolge | Der eindeutige Store-Code innerhalb einer Website. |
| [!UICONTROL Store View Code] | `storeViewCode` | Zeichenfolge | Der eindeutige Store-Ansichtscode in einem Store. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
