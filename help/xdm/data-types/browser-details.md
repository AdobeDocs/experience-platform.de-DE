---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Browser;Browser-Details;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der Browser-Details
description: Erfahren Sie mehr über den XDM-Datentyp „Browser-Details“.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 27%

---

# [!UICONTROL Browserdetails] Datentyp

[!UICONTROL Browser-Details] ist ein standardmäßiger XDM-Datentyp, der Details zu einem Browser oder einer Anwendung beschreibt.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acceptLanguage` | Zeichenfolge | Ein IETF-Sprach-Tag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolesch | Gibt an, ob die Benutzereinstellungen das Schreiben von Cookies zulassen. |
| `javaEnabled` | Boolesch | Gibt an, ob Java auf dem Gerät aktiviert wurde, von dem aus die Beobachtung durchgeführt wurde. |
| `javaScriptEnabled` | Boolesch | Gibt an, ob JavaScript auf dem Gerät aktiviert wurde, von dem aus die Beobachtung durchgeführt wurde. |
| `javaScriptVersion` | String | Die während der Beobachtung unterstützte JavaScript-Version. |
| `javaVersion` | String | Die während der Beobachtung unterstützte Java-Version. |
| `name` | String | Der Anwendungs- oder Browsername. |
| `quicktimeVersion` | String | Die während der Beobachtung unterstützte Apple Quicktime-Version. |
| `thirdPartyCookiesEnabled` | Boolesch | Gibt an, ob Drittanbieter-Cookies auf dem Gerät aktiviert wurden, von dem aus die Beobachtung durchgeführt wurde. |
| `userAgent` | String | Die HTTP-Benutzeragenten-Zeichenfolge aus der Client-Anfrage. |
| `vendor` | String | Der Anwendungs- oder Browser-Anbieter. |
| `version` | String | Die Anwendungs- oder Browser-Version. |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixeln des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Web-Ansichtsereignis ist dies die Höhe des Browser-Ansichtsfensters. |
| `viewportWidth` | Ganzzahl | Die horizontale Größe in Pixeln des Fensters, in dem das Ereignis angezeigt wurde. Bei einem Web-Ansichtsereignis ist dies die Breite des Browser-Ansichtsfensters. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
