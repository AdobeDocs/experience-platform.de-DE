---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Browser; Browserdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Browser Details"
description: Erfahren Sie mehr über den XDM-Datentyp Browserdetails .
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 27%

---

# [!UICONTROL Browserdetails]-Datentyp

[!UICONTROL Browserdetails] ist ein standardmäßiger XDM-Datentyp, der Details zu einem Browser oder einer Anwendung beschreibt.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acceptLanguage` | Zeichenfolge | Ein IETF-Sprach-Tag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolesch | Gibt an, ob die Benutzereinstellungen das Schreiben von Cookies zulassen. |
| `javaEnabled` | Boolesch | Gibt an, ob Java auf dem Gerät aktiviert wurde, aus dem die Beobachtung durchgeführt wurde. |
| `javaScriptEnabled` | Boolesch | Gibt an, ob JavaScript auf dem Gerät aktiviert wurde, aus dem die Beobachtung durchgeführt wurde. |
| `javaScriptVersion` | Zeichenfolge | Die während der Beobachtung unterstützte JavaScript-Version. |
| `javaVersion` | Zeichenfolge | Die während der Beobachtung unterstützte Java-Version. |
| `name` | Zeichenfolge | Der Anwendungs- oder Browsername. |
| `quicktimeVersion` | Zeichenfolge | Die während der Beobachtung unterstützte Apple Quicktime-Version. |
| `thirdPartyCookiesEnabled` | Boolesch | Gibt an, ob Drittanbieter-Cookies auf dem Gerät aktiviert wurden, aus dem die Beobachtung durchgeführt wurde. |
| `userAgent` | Zeichenfolge | Die HTTP-Benutzeragenten-Zeichenfolge aus der Client-Anfrage. |
| `vendor` | Zeichenfolge | Der Anwendungs- oder Browser-Anbieter. |
| `version` | Zeichenfolge | Die Anwendungs- oder Browser-Version. |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixel des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Webansichtsereignis ist dies die Höhe des Browser-Ansichtsfensters. |
| `viewportWidth` | Ganzzahl | Die horizontale Größe in Pixel des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Webansichtsereignis ist dies die Breite des Browser-Ansichtsfensters. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
