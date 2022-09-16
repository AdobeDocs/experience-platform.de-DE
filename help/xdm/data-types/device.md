---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Gerät; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Device Data Type
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Geräte-XDM-Datentyp.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 18%

---

# [!UICONTROL Gerät] Datentyp

[!UICONTROL Gerät] ist ein standardmäßiger XDM-Datentyp, der ein identifiziertes Gerät beschreibt. Ein Gerät ist eine Anwendung oder Browser-Instanz, die sitzungsübergreifend verfolgt werden kann, normalerweise durch Cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `colorDepth` | Ganzzahl | Die Anzahl der Farben, die die Anzeige darstellen kann. |
| `manufacturer` | Zeichenfolge | Der Name der Organisation, der das Design und die Erstellung des Geräts gehören. |
| `model` | Zeichenfolge | Der Name des Modells für das Gerät. Dies ist der gebräuchliche, für Menschen lesbare oder Marketing-Name des Geräts. Beispielsweise ist &quot;iPhone 6S&quot;ein bestimmtes Mobiltelefonmodell. |
| `modelNumber` | Zeichenfolge | Die eindeutige Modellnummer, die der Hersteller diesem Gerät zugewiesen hat. Modellnummern sind keine Versionen, sondern eindeutige Bezeichner, die eine bestimmte Modellkonfiguration identifizieren. |
| `screenHeight` | Ganzzahl | Die Anzahl der vertikalen Pixel der aktiven Anzeige des Geräts in der Standardausrichtung. |
| `screenOrientation` | Zeichenfolge | Die aktuelle Bildschirmausrichtung. Zu den zulässigen Werten gehören `portrait` und `landscape`. |
| `screenWidth` | Zeichenfolge | Die Anzahl der horizontalen Pixel der aktiven Anzeige des Geräts in der Standardausrichtung. |
| `type` | Zeichenfolge | Der Typ des zu verfolgenden Geräts. Zu den zulässigen Werten gehören: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Zeichenfolge | Eine Kennung für das Gerät. Dies kann eine Kennung von DeviceAtlas oder einem anderen Dienst sein, der die verwendete Hardware identifiziert. |
| `typeIDService` | Zeichenfolge | Der Namespace des Diensts, mit dem der Gerätetyp identifiziert wird. Siehe [Anhang](#typeIDService) für Details zu akzeptierten Werten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum [!UICONTROL Gerät] Datentyp.

## Akzeptierte Werte für typeIDService {#typeIDService}

In der folgenden Tabelle sind die für `typeIDService` und ihre zugehörige Bedeutung:

| Wert | Beschreibung |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Das Gerät wurde mit DeviceAtlas identifiziert. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Das Gerät wurde mit Adobe Campaign identifiziert. |
