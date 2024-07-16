---
title: Commerce Scope-Datentyp
description: Erfahren Sie mehr über den Commerce Scope Experience Data Model (XDM)-Datentyp.
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# Datentyp [!UICONTROL Commerce Scope]

[!UICONTROL Commerce Scope] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der IDs definiert, für die in einem Commerce-Ökosystem ein Ereignis aufgetreten ist. Sie unterscheidet Umgebungen, Websites, Stores und Store-Ansichten.

![Ein Diagramm des Commerce Scope-Datentyps.](../images/data-types/commerce-scope.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Umgebungs-ID] | `environmentID` | Zeichenfolge | Die Umgebungs-ID. Eine 32-stellige alphanumerische ID. |
| [!UICONTROL Website-Code] | `websiteCode` | Zeichenfolge | Der eindeutige Website-Code in einer Umgebung. |
| [!UICONTROL Speichercode] | `storeCode` | Zeichenfolge | Der eindeutige Store-Code innerhalb einer Website. |
| [!UICONTROL Code für die Store-Ansicht] | `storeViewCode` | Zeichenfolge | Der eindeutige Store-Ansichtscode in einem Store. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
