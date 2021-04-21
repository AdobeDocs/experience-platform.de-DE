---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Webseitendetails;Datentyp;Datentyp;Datentyp;Webseite
solution: Experience Platform
title: Datentyp "Webseitendetails"
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Erlebnisdatenmodells (XDM) für Webseitendetails.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 10%

---

# [!UICONTROL Datentyp ] der Webseite

[!UICONTROL Eine Webseite ] enthält einen standardmäßigen XDM-Datentyp (Experience Data Model), der Details zu einer Webseite beschreibt, die gerade geladen und angezeigt wurde, wie von einem ExperienceEvent aufgezeichnet.

Der Datentyp ist für vollständige Seitendetails und das Laden der ersten Seite von einseitigen Webanwendungen (SPA) vorgesehen. Informationen zu Interaktionen, die auf einer geladenen Seite stattfinden und nicht zum Trigger eines neuen Seitenladevorgangs führen, finden Sie im Datentyp [Webinteraktion](./web-interactions.md).

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Maßnahme]](./measure.md) | Die Anzahl der Ansichten auf einer Webseite. |
| `URL` | Zeichenfolge | Die normative oder übliche URL der Webseite. Dies kann die eigentliche URL sein, die zum Erreichen der Seite verwendet wird. Um die URL aufzuzeichnen, die zum Erreichen der Seite verwendet wird, verwenden Sie `webLink`. Das URI-Format sollte dem Standard [RFC 3986](https://tools.ietf.org/html/rfc3986) entsprechen. |
| `isErrorPage` | Boolesch | Diese Eigenschaft verwendet ein Flag, um anzugeben, ob es sich bei der Seite um eine Fehlerseite handelt oder nicht. Diese Markierung wird verwendet, um Webinteraktionen grob zu kategorisieren. Der Fehler wird von der Anwendung definiert und kann einer Seite entsprechen, die mit einem HTTP-Fehlercode versorgt wird. |
| `isHomePage` | Boolesch | Diese Eigenschaft verwendet ein Flag, um anzugeben, ob es sich bei der Seite um eine Startseite handelt oder nicht. Diese Markierung wird verwendet, um Webinteraktionen grob zu kategorisieren. Die Begriffsbestimmung für Startseite wird durch den Antrag festgelegt. |
| `name` | Zeichenfolge | Der normative Name der Webseite. Dieser Name ist nicht notwendigerweise der Seitentitel oder steht in direktem Zusammenhang mit dem Seiteninhalt, er wird aber zur Klassifizierung der Seiten einer Site verwendet. |
| `server` | Zeichenfolge | Der normative oder normale Server, auf dem die Webseite gehostet wird. Dies kann der Host oder der Server sein, der bzw. der die Seiteninteraktion tatsächlich durchgeführt hat. |
| `siteSection` | Zeichenfolge | Der normative Name des Sitebereichs, in dem sich diese Webseite befindet. Auf diese Weise können Sie die Interaktion klassifizieren oder kategorisieren. |
| `viewName` | Zeichenfolge | Der Name der Ansicht innerhalb einer Seite. Diese Eigenschaft wird häufig bei Einzelseitenanwendungen oder Seiten mit Registerkarten oder Steuerelementen verwendet, die einen Großteil des Seitenlayouts ändern. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
