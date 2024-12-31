---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Umgebung;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Umgebungs-Datentyp
description: Informationen zum XDM-Datentyp der Umgebung.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 19%

---

# [!UICONTROL Umgebung] Datentyp

[!UICONTROL Umgebung] ist ein standardmäßiger XDM-Datentyp, der die Umgebung eines beobachteten Ereignisses beschreibt, insbesondere mit Details zu vorübergehenden Informationen wie Netzwerk- und Softwareversionen.

>[!IMPORTANT]
>
>Alle Werte sollten mit der Datenbank [DeviceAtlas](https://deviceatlas.com) abgeglichen werden, die per Adobe lizenziert wird.

<img src="../images/data-types/environment.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc` | Objekt | Ein Objekt, das ein einzelnes Feld `language` enthält, das die Sprache der Umgebung angibt, um die sprachlichen, geografischen oder kulturellen Voreinstellungen der Benutzenden für die Datendarstellung darzustellen. Sprachen werden im Sprach-Code angegeben, wie in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt) definiert. |
| `browserDetails` | [Browser-Details](./browser-details.md) | Beschreibt die browserspezifischen Details der Umgebung, z. B. Browsername, Version, JavaScript-Version, Benutzeragenten-Zeichenfolge und akzeptierte Sprache. |
| `ISP` | String | Der Name des Internet-Dienstleisters (ISP) des Benutzers. |
| `carrier` | String | Der Name des Mobilfunknetzbetreibers oder MNO (auch als Mobilfunkanbieter, Mobilfunkunternehmen, Mobilfunkunternehmen oder Mobilfunknetzbetreiber bezeichnet), der Kommunikationsdienste an den Benutzer verkauft und bereitstellt. |
| `colorDepth` | Ganzzahl | Die Anzahl der Bits, die für jede Farbkomponente eines einzelnen Pixels verwendet werden. |
| `connectionType` | String | Der Internet-Verbindungstyp. Zu den akzeptierten Werten gehören: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | String | Die Domain des ISP des Benutzers. |
| `ipV4` | String | Die numerische Beschriftung, die einem Gerät zugewiesen ist, das an einem Computernetzwerk teilnimmt, das das Internetprotokoll für die Kommunikation verwendet (32-Bit). |
| `ipV6` | String | Die numerische Beschriftung, die einem Gerät zugewiesen ist, das an einem Computernetzwerk teilnimmt, das das Internetprotokoll für die Kommunikation verwendet (128-Bit). |
| `operatingSystem` | String | Der Name des Betriebssystems, das bei der Beobachtung verwendet wurde. Das Attribut sollte keine Versionsinformationen wie `10.5.3` enthalten, sondern stattdessen „edition“-Bezeichnungen wie `Ultimate` oder `Professional`. |
| `operatingSystemVendor` | String | Der Name des Betriebssystemanbieters, das bei der Beobachtung verwendet wurde. |
| `operatingSystemVersion` | String | Die Vollversionskennung des Betriebssystems, das bei der Beobachtung verwendet wurde. Versionen werden im Allgemeinen numerisch zusammengestellt, können aber in einem vom Anbieter definierten Format vorliegen. |
| `type` | String | Der Typ der Anwendungsumgebung. Siehe [Anhang](#type) für gültige Werte. |
| `viewportHeight` | Ganzzahl | Die vertikale Größe in Pixeln des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Web-Ansichtsereignis ist dies die Höhe des Browser-Ansichtsfensters. |
| `viewPortWidth` | Ganzzahl | Die horizontale Größe in Pixeln des Fensters, in dem das Erlebnis angezeigt wurde. Bei einem Web-Ansichtsereignis ist dies die Breite des Browser-Ansichtsfensters. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Gerät].

## Akzeptierte Werte für den Typ {#type}

In der folgenden Tabelle sind die akzeptierten Werte für `type` und ihre zugehörigen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `browser` | Browser |
| `application` | Anwendung |
| `iot` | Internet der Dinge |
| `external` | Externes System |
| `widget` | Anwendungserweiterung |
