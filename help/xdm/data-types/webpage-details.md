---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Webseitendetails;Datentyp;Datentyp;WebPage
solution: Experience Platform
title: Datentyp „Web-Seitendetails“
description: Erfahren Sie mehr über die Web-Seitendetails zum Datentyp Experience-Datenmodell (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 11%

---

# [!UICONTROL Webseitendetails] Datentyp

[!UICONTROL Web-Seitendetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu einer Web-Seite beschreibt, die gerade geladen und angezeigt wurde und von einem ExperienceEvent aufgezeichnet wurde.

Der Datentyp ist für vollständige Seitendetails und anfängliches Laden von Einzelseiten-Web-Anwendungen (SPA) vorgesehen. Informationen zu Interaktionen, die auf einer geladenen Seite stattfinden und keinen neuen Seitenladevorgang im Trigger haben, finden Sie unter [Web-Interaktion](./web-interaction.md) Datentyp .

![Web-Seitendetails](../images/data-types/web-page-details.PNG){width="500"}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Maßnahme]](./measure.md) | Die Anzahl der Ansichten auf einer Web-Seite. |
| `URL` | String | Die normative oder übliche URL der Webseite. Dies kann, muss aber nicht die tatsächliche URL sein, die zum Aufrufen der Seite verwendet wird. Verwenden Sie `webLink`, um die URL aufzuzeichnen, über die die Seite erreicht wird. Das URI-Format muss dem Standard [RFC 3986](https://tools.ietf.org/html/rfc3986) entsprechen. |
| `isErrorPage` | Boolesch | Diese Eigenschaft verwendet eine Markierung, um anzugeben, ob die Seite eine Fehlerseite ist oder nicht. Dieses Flag wird verwendet, um Web-Interaktionen grob zu kategorisieren. Der Fehler wird von der Anwendung definiert und kann einer Seite entsprechen, die mit einem HTTP-Fehler-Code bereitgestellt wird. |
| `isHomePage` | Boolesch | Diese Eigenschaft verwendet eine Markierung, um anzugeben, ob die Seite eine Startseite ist oder nicht. Dieses Flag wird verwendet, um Web-Interaktionen grob zu kategorisieren. Die Definition der Startseite wird von der Anwendung bestimmt. |
| `name` | String | Der normative Name der Web-Seite. Dieser Name ist nicht notwendigerweise der Seitentitel oder direkt mit dem Seiteninhalt verknüpft, sondern wird verwendet, um die Seiten einer Site zu Klassifizierungszwecken zu organisieren. |
| `server` | String | Der normative oder übliche Server, der die Web-Seite hostet. Dies kann, muss aber nicht der Host oder Server sein, der tatsächlich die Seiteninteraktion durchgeführt hat. |
| `siteSection` | String | Der normative Name des Site-Bereichs, in dem sich diese Web-Seite befindet. Dies kann verwendet werden, um die Interaktion zu klassifizieren oder zu kategorisieren. |
| `viewName` | String | Der Name der Ansicht innerhalb einer Seite. Diese Eigenschaft wird häufig bei Einzelseitenanwendungen oder Seiten mit Registerkarten oder Steuerelementen verwendet, die einen Großteil des Seitenlayouts ändern. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
