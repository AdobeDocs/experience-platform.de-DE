---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Webseitendetails; Datentyp; Datentyp; Datentyp; Datentyp; Webseite
solution: Experience Platform
title: Datentyp "Web Page Details"
description: Dieses Dokument bietet einen Überblick über die Webseitendetails zum Experience-Datenmodell (XDM)-Datentyp.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 13%

---

# [!UICONTROL Webseitendetails] Datentyp

[!UICONTROL Webseitendetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu einer Web-Seite beschreibt, die gerade geladen und angezeigt wurde und von einem ExperienceEvent aufgezeichnet wurde.

Der Datentyp ist für vollständige Seitendetails und das erstmalige Laden von Einzelseiten-Webanwendungen (SPA) vorgesehen. Informationen zu Interaktionen, die auf einer geladenen Seite stattfinden und bei denen kein neuer Seitenladevorgang Trigger wird, finden Sie im Abschnitt [Web-Interaktion](./web-interaction.md) Datentyp.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Maßnahme]](./measure.md) | Die Anzahl der Ansichten auf einer Webseite. |
| `URL` | Zeichenfolge | Die normative oder übliche URL der Webseite. Dies kann die tatsächliche URL sein, die zum Erreichen der Seite verwendet wird. Um die URL aufzuzeichnen, mit der die Seite erreicht wird, verwenden Sie `webLink`. Das URI-Format sollte dem [RFC 3986](https://tools.ietf.org/html/rfc3986) Standard. |
| `isErrorPage` | Boolesch | Diese Eigenschaft verwendet eine Markierung, um anzugeben, ob es sich bei der Seite um eine Fehlerseite handelt oder nicht. Diese Markierung wird verwendet, um Webinteraktionen grob zu kategorisieren. Der Fehler wird von der Anwendung definiert und kann einer Seite entsprechen, die mit einem HTTP-Fehlercode versorgt wird. |
| `isHomePage` | Boolesch | Diese Eigenschaft verwendet eine Markierung, um anzugeben, ob es sich bei der Seite um eine Homepage handelt oder nicht. Diese Markierung wird verwendet, um Webinteraktionen grob zu kategorisieren. Die Definition der Homepage wird von der Anwendung bestimmt. |
| `name` | Zeichenfolge | Der normative Name der Webseite. Dieser Name ist nicht notwendigerweise der Seitentitel oder direkt mit dem Seiteninhalt verknüpft, sondern dient zum Organisieren der Seiten einer Site zu Klassifizierungszwecken. |
| `server` | Zeichenfolge | Der normative oder normale Server, auf dem die Webseite gehostet wird. Dies kann der Host oder Server sein, der die Seiteninteraktion tatsächlich durchgeführt hat. |
| `siteSection` | Zeichenfolge | Der normative Name des Website-Bereichs, in dem sich diese Webseite befindet. Damit können Sie die Interaktion klassifizieren oder kategorisieren. |
| `viewName` | Zeichenfolge | Der Name der Ansicht innerhalb einer Seite. Diese Eigenschaft wird häufig bei Einzelseitenanwendungen oder Seiten mit Registerkarten oder Steuerelementen verwendet, die einen Großteil des Seitenlayouts ändern. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
