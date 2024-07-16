---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Umgebung; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Umgebungstyp
description: Erfahren Sie mehr über den Umgebungs-XDM-Datentyp.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 19%

---

# Datentyp [!UICONTROL Umgebung]

[!UICONTROL Umgebung] ist ein standardmäßiger XDM-Datentyp, der die Umgebung eines beobachteten Ereignisses beschreibt, insbesondere mit detaillierten Informationen zu vorübergehenden Informationen wie Netzwerk- und Softwareversionen.

>[!IMPORTANT]
>
>Alle Werte sollten mit der durch Adobe lizenzierten [DeviceAtlas](https://deviceatlas.com) -Datenbank übereinstimmen.

<img src="../images/data-types/environment.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc` | Objekt | Ein Objekt, das ein einzelnes Feld `language` enthält, das die Sprache der Umgebung angibt, die die sprachlichen, geografischen oder kulturellen Voreinstellungen des Benutzers für die Datendarstellung darstellen soll. Sprachen werden in Sprachcode gemäß der Definition in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) angegeben. |
| `browserDetails` | [Browserdetails](./browser-details.md) | Beschreibt die browserspezifischen Details der Umgebung, wie z. B. Browsername, Version, JavaScript-Version, Benutzeragenten-Zeichenfolge und akzeptierte Sprache. |
| `ISP` | Zeichenfolge | Der Name des Internet-Dienstleisters (ISP) des Benutzers. |
| `carrier` | Zeichenfolge | Name des Mobilfunknetzbetreibers oder der Mobilfunknetzbetreiber (auch als drahtloser Dienstleister, drahtloser Netzbetreiber, Mobilfunkunternehmen oder Mobilfunknetzbetreiber bezeichnet), der Kommunikationsdienste an den Benutzer verkauft und bereitstellt. |
| `colorDepth` | Ganzzahl | Die Anzahl der Bits, die für jede Farbkomponente eines einzelnen Pixels verwendet werden. |
| `connectionType` | Zeichenfolge | Der Typ der Internetverbindung. Zu den zulässigen Werten gehören: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Zeichenfolge | Die Domäne des ISP des Benutzers. |
| `ipV4` | Zeichenfolge | Die numerische Beschriftung, die einem Gerät zugewiesen ist, das an einem Computernetzwerk teilnimmt, das das Internet-Protokoll für die Kommunikation verwendet (32 Bit). |
| `ipV6` | Zeichenfolge | Die numerische Beschriftung, die einem Gerät zugewiesen ist, das an einem Computernetzwerk teilnimmt, das das Internet-Protokoll für die Kommunikation verwendet (128 Bit). |
| `operatingSystem` | Zeichenfolge | Der Name des Betriebssystems, das bei der Beobachtung verwendet wurde. Das Attribut sollte keine Versionsinformationen wie `10.5.3` enthalten, sondern stattdessen &quot;Bearbeitungsbezeichnungen&quot;wie `Ultimate` oder `Professional` enthalten. |
| `operatingSystemVendor` | Zeichenfolge | Der Name des Betriebssystemanbieters, das bei der Beobachtung verwendet wurde. |
| `operatingSystemVersion` | Zeichenfolge | Die Vollversionskennung des Betriebssystems, das bei der Beobachtung verwendet wurde. Versionen sind im Allgemeinen numerisch aufgebaut, können jedoch in einem vom Anbieter definierten Format vorliegen. |
| `type` | Zeichenfolge | Der Typ der Anwendungsumgebung. Akzeptierte Werte finden Sie im [Anhang](#type) . |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixel des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Webansichtsereignis ist dies die Höhe des Browser-Ansichtsfensters. |
| `viewPortWidth` | Ganzzahl | Die horizontale Größe in Pixel des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Webansichtsereignis ist dies die Breite des Browser-Ansichtsfensters. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Gerät] .

## Akzeptierte Werte für Typ {#type}

In der folgenden Tabelle sind die zulässigen Werte für `type` und die zugehörige Bedeutung aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `browser` | Browser |
| `application` | Anwendung |
| `iot` | Internet der Dinge |
| `external` | Externes System |
| `widget` | Anwendungserweiterung |
