---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Webinteraktion;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Webinteraktionsdatentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Experience Data Model (XDM) für Webinteraktion.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 4%

---

# [!UICONTROL Web-] Interaktionsdatentyp

[!UICONTROL Web-] Interaktion ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der Informationen zu Interaktionen beschreibt, die auf einer Webseite nach dem ersten Laden der Seite aufgetreten sind. Es ist für die Aufzeichnung von Interaktionen in Rich-Web-Anwendungen vorgesehen, bei denen kein neuer Seitenladevorgang wie einseitige Web-Apps (SPA) Trigger wird.

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Messung, die den Klick auf einen Weblink verfolgt. |
| `URL` | Zeichenfolge | Der eigentliche Link oder die URL, der bzw. die für diese Webinteraktion verwendet wird. |
| `name` | Zeichenfolge | Der normative Name, der für diesen Weblink verwendet wird. Dies wird zu Classification-Zwecken verwendet. |
| `type` | Zeichenfolge | Der Linktyp. Diese Eigenschaft muss einem der folgenden Enum-Werte entsprechen: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
