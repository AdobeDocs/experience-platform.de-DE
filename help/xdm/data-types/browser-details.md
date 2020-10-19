---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Datentyp "Browserdetails"
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp von Browserdetails.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 21%

---


# [!UICONTROL Datentyp der] Browserdetails

[!UICONTROL Browserdetails] sind ein standardmäßiger XDM-Datentyp, der Details zu einem Browser oder einer Anwendung beschreibt.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acceptLanguage` | Zeichenfolge | An IETF language tag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolesch | Gibt an, ob die Benutzereinstellungen das Schreiben von Cookies zulassen. |
| `javaEnabled` | Boolesch | Gibt an, ob Java auf dem Gerät, von dem die Beobachtung ausgeführt wurde, aktiviert wurde. |
| `javaScriptEnabled` | Boolesch | Gibt an, ob JavaScript auf dem Gerät, von dem die Beobachtung durchgeführt wurde, aktiviert wurde. |
| `javaScriptVersion` | Zeichenfolge | Die während der Beobachtung unterstützte JavaScript-Version. |
| `javaVersion` | Zeichenfolge | Die während der Beobachtung unterstützte Java-Version. |
| `name` | Zeichenfolge | Der Anwendungs- oder Browsername. |
| `quicktimeVersion` | Zeichenfolge | Die während der Beobachtung unterstützte Apple Quicktime-Version. |
| `thirdPartyCookiesEnabled` | Boolesch | Gibt an, ob Drittanbieter-Cookies im Gerät, aus dem die Beobachtung stammt, aktiviert wurden. |
| `userAgent` | Zeichenfolge | Die HTTP-Benutzeragent-Zeichenfolge aus der Clientanforderung. |
| `vendor` | Zeichenfolge | Der Anwendungs- oder Browser-Anbieter. |
| `version` | Zeichenfolge | Die Anwendungs- oder Browserversion. |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixeln des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Web-Ansicht-Ereignis ist dies die Browser-Viewport-Höhe. |
| `viewportWidth` | Ganzzahl | Die horizontale Größe in Pixeln des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Web-Ansicht-Ereignis ist dies die Browser-Viewport-Breite. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)