---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Umgebung;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp der Umgebung
topic-legacy: overview
description: Dieses Dokument gibt einen Überblick über den XDM-Datentyp der Umgebung.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 14%

---

# [!UICONTROL Typ ] Environmentdata

[!UICONTROL Die ] Umgebung ist ein Standard-XDM-Datentyp, der die umliegende Umgebung eines beobachteten Ereignisses beschreibt und dabei insbesondere vorübergehende Informationen wie Netzwerk- und Softwareversionen beschreibt.

>[!IMPORTANT]
>
>Alle Werte sollten mit der [DeviceAtlas](https://deviceatlas.com)-Datenbank, lizenziert von der Adobe, übereinstimmen.

<img src="../images/data-types/environment.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc` | Objekt | Ein Objekt, das ein einzelnes Feld mit der Bezeichnung `language` enthält, das die Sprache der Umgebung angibt, in der die sprachlichen, geografischen oder kulturellen Präferenzen des Benutzers für die Datendarstellung dargestellt werden sollen. Die Sprache wird im Sprachcode angegeben, wie in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) definiert. |
| `browserDetails` | [Browserdetails](./browser-details.md) | Beschreibt die browserspezifischen Details der Umgebung, z. B. Browsername, Version, JavaScript-Version, Benutzeragenten-Zeichenfolge und Annahmesprache. |
| `ISP` | Zeichenfolge | Der Name des Internet-Dienstleisters des Benutzers. |
| `carrier` | Zeichenfolge | Der Name des Mobilfunknetzbetreibers oder der Mobilfunknetzbetreiber (auch als Wireless-Dienstleister, Wireless-Netzbetreiber, Mobilnetzbetreiber oder Mobilnetzbetreiber bezeichnet), der Kommunikationsdienste verkauft und für den Nutzer bereitstellt. |
| `colorDepth` | Ganzzahl | Die Anzahl der Bit, die für jede Farbkomponente eines einzelnen Pixels verwendet werden. |
| `connectionType` | Zeichenfolge | Der Typ der Internetverbindung. Zu den zulässigen Werten gehören: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Zeichenfolge | Die Domäne des ISP des Benutzers. |
| `ipV4` | Zeichenfolge | Die numerische Beschriftung, die einem Gerät zugewiesen ist, das an einem Computernetzwerk teilnimmt, das das Internetprotokoll für die Kommunikation verwendet (32-Bit). |
| `ipV6` | Zeichenfolge | Die numerische Beschriftung, die einem Gerät zugewiesen wird, das an einem Computernetzwerk teilnimmt, das das Internet-Protokoll für die Kommunikation verwendet (128 Bit). |
| `operatingSystem` | Zeichenfolge | Der Name des Betriebssystems, das bei der Beobachtung verwendet wurde. Das Attribut sollte keine Versionsinformationen wie `10.5.3` enthalten, sondern stattdessen &quot;Edition&quot;-Bezeichnungen wie `Ultimate` oder `Professional` enthalten. |
| `operatingSystemVendor` | Zeichenfolge | Der Name des Betriebssystemanbieters, das bei der Beobachtung verwendet wurde. |
| `operatingSystemVersion` | Zeichenfolge | Die Vollversionskennung des Betriebssystems, das bei der Beobachtung verwendet wurde. Versionen werden in der Regel numerisch zusammengestellt, können jedoch in einem vom Anbieter definierten Format vorliegen. |
| `type` | Zeichenfolge | Der Typ der Anwendungs-Umgebung. Die zulässigen Werte finden Sie im Anhang [a1/>.](#type) |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixeln des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Web-Ansicht-Ereignis ist dies die Browser-Viewport-Höhe. |
| `viewPortWidth` | Ganzzahl | Die horizontale Größe in Pixeln des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Web-Ansicht-Ereignis ist dies die Browser-Viewport-Breite. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Datentyp [!UICONTROL Gerät].

## Akzeptierte Werte für den Typ {#type}

In der folgenden Tabelle sind die für `type` zulässigen Werte und die damit verbundenen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `browser` | Browser |
| `application` | Anwendung |
| `iot` | Internet der Dinge |
| `external` | Externes System |
| `widget` | Anwendungserweiterung |
