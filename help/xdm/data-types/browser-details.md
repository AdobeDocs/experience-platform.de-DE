---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Browser;Browserdetails;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp "Browserdetails"
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp von Browserdetails.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 19%

---

# [!UICONTROL Browser-] DetailsDatentyp

[!UICONTROL Browser-] Details enthalten einen Standard-XDM-Datentyp, der Details zu einem Browser oder einer Anwendung beschreibt.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acceptLanguage` | Zeichenfolge | Ein IETF-Sprach-Tag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
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
