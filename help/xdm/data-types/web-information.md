---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Webseitendetails;Datentyp;Datentyp;WebPage
solution: Experience Platform
title: Datentyp Web-Informationen
description: Erfahren Sie mehr über den Datentyp Web-Informationen für Experience-Datenmodelle (XDM).
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL Web-Informationen] Datentyp

[!UICONTROL Web-Informationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen beschreibt, die über ein Erlebnisereignis aufgezeichnet wurden, das für den World Wide Web-Kanal spezifisch ist, einschließlich Web-Seite, Referrer und/oder Link im Zusammenhang mit der Interaktion auf der Seite.

![](../images/data-types/web-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web-Interaktion]](./web-interaction.md) | Beschreibt die Details zum Weblink oder zur URL, die der Interaktion entspricht. |
| `webPageDetails` | [[!UICONTROL Web-Seitendetails]](./webpage-details.md) | Beschreibt die Details der Web-Seite, auf der die Web-Interaktion stattgefunden hat. |
| `webReferrer` | [!UICONTROL Objekt] | Beschreibt den Referrer einer Web-Interaktion, also die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. Enthält die folgenden Untereigenschaften: <ul><li>`URL`: Die Referrer-URL.</li><li>`type`: Der Referrer-Typ.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
