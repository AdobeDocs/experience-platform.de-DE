---
title: Datentyp des Commerce-Umfangs
description: Erfahren Sie mehr über den Datentyp Commerce Scope Experience Data Model (XDM).
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# Datentyp &lbrace;0 Commerce Scope

[!UICONTROL Commerce-Umfang] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Kennungen für den Ort definiert, an dem ein Ereignis in einem Commerce-Ökosystem aufgetreten ist. Es unterscheidet Umgebungen, Websites, Stores und Store-Ansichten.

![Abbildung des Datentyps „Umfang von Commerce&quot;.](../images/data-types/commerce-scope.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Umgebungs-ID] | `environmentID` | Zeichenfolge | Die Umgebungskennung. Eine 32-stellige alphanumerische ID. |
| [!UICONTROL Website-Code] | `websiteCode` | Zeichenfolge | Der eindeutige Website-Code innerhalb einer Umgebung. |
| [!UICONTROL Code speichern] | `storeCode` | Zeichenfolge | Der eindeutige Store-Code innerhalb einer Website. |
| [!UICONTROL Code der Speicheransicht] | `storeViewCode` | Zeichenfolge | Der eindeutige Code der Store-Ansicht in einem Store. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
