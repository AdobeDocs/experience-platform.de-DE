---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Webseitendetails; Datentyp; Datentyp; Datentyp; Datentyp; Webseite
solution: Experience Platform
title: Datentyp für Webinformationen
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Webinformationen-Datentyp Experience-Datenmodell (XDM) .
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---

# [!UICONTROL Datentyp ] &quot;Web information&quot;

[!UICONTROL Web-] Informationen sind ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Informationen beschreibt, die über ein Erlebnisereignis aufgezeichnet wurden, das für den World Wide Web-Kanal spezifisch ist, einschließlich der Web-Seite, des Referrers und/oder des Links im Zusammenhang mit der On-Page-Interaktion.

![](../images/data-types/web-information.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Webinteraktion]](./web-interaction.md) | Beschreibt die Details des Weblinks oder der URL, die der Interaktion entspricht. |
| `webPageDetails` | [[!UICONTROL Webseitendetails]](./webpage-details.md) | Beschreibt die Details der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `webReferrer` | [!UICONTROL Objekt] | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. Enthält die folgenden Untereigenschaften: <ul><li>`URL`: Die Referrer-URL.</li><li>`type`: Der Typ der verweisenden Stelle.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
