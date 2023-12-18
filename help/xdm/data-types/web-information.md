---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Webseitendetails; Datentyp; Datentyp; Datentyp; Datentyp; Webseite
solution: Experience Platform
title: Datentyp für Webinformationen
description: Erfahren Sie mehr über den Webinformationen-Datentyp Experience-Datenmodell (XDM) .
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL Webinformationen] Datentyp

[!UICONTROL Webinformationen] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen beschreibt, die über ein Erlebnisereignis aufgezeichnet wurden, das für den World Wide Web-Kanal spezifisch ist, einschließlich der Webseite, des Referrers und/oder des Links im Zusammenhang mit der On-Page-Interaktion.

![](../images/data-types/web-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Webinteraktion]](./web-interaction.md) | Beschreibt die Details des Weblinks oder der URL, die der Interaktion entspricht. |
| `webPageDetails` | [[!UICONTROL Webseitendetails]](./webpage-details.md) | Beschreibt die Details der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `webReferrer` | [!UICONTROL Objekt] | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. Enthält die folgenden Untereigenschaften: <ul><li>`URL`: Die Referrer-URL.</li><li>`type`: Der Typ der verweisenden Stelle.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
