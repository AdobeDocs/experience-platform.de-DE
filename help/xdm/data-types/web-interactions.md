---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Web-Interaktion; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Web Interaction-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Datentyp des Experience-Datenmodells (XDM) für Webinteraktionen.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---

# [!UICONTROL Web ] InteractionData type

[!UICONTROL Web-] Interaktion ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Informationen über Interaktionen beschreibt, die auf einer Webseite nach dem ersten Laden der Seite aufgetreten sind. Sie ist zur Aufzeichnung von Interaktionen in Rich-Web-Anwendungen gedacht, die keinen neuen Seitenladevorgang wie Single-Page-Webanwendungen (SPA) Trigger haben.

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Messung, die den Klick auf einen Weblink verfolgt. |
| `URL` | Zeichenfolge | Der tatsächliche Link oder die URL, der bzw. die für diese Web-Interaktion verwendet wird. |
| `name` | Zeichenfolge | Der normative Name, der für diesen Web-Link verwendet wird. Dies wird zu Classification-Zwecken verwendet. |
| `type` | Zeichenfolge | Der Linktyp. Diese Eigenschaft muss einem der folgenden Enum-Werte entsprechen: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
