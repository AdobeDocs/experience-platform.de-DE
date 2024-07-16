---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Gerät; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Device Data Type
description: Erfahren Sie mehr über den Geräte-XDM-Datentyp.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 19%

---

# [!UICONTROL Device]-Datentyp

[!UICONTROL Gerät] ist ein standardmäßiger XDM-Datentyp, der ein identifiziertes Gerät beschreibt. Ein Gerät ist eine Anwendung oder Browser-Instanz, die sitzungsübergreifend verfolgt werden kann, normalerweise durch Cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `colorDepth` | Ganzzahl | Die Anzahl der Farben, die die Anzeige darstellen kann. |
| `manufacturer` | Zeichenfolge | Der Name der Organisation, der das Design und die Erstellung des Geräts gehören. |
| `model` | Zeichenfolge | Der Name des Modells für das Gerät. Dies ist der gebräuchliche, für Menschen lesbare oder Marketing-Name des Geräts. Beispielsweise ist &quot;iPhone 6S&quot;ein bestimmtes Mobiltelefonmodell. |
| `modelNumber` | Zeichenfolge | Die eindeutige Modellnummer, die der Hersteller diesem Gerät zugewiesen hat. Modellnummern sind keine Versionen, sondern eindeutige Kennungen, die eine bestimmte Modellkonfiguration identifizieren. |
| `screenHeight` | Ganzzahl | Die Anzahl der vertikalen Pixel des aktiven Displays des Geräts in der Standardausrichtung. |
| `screenOrientation` | Zeichenfolge | Die aktuelle Bildschirmausrichtung. Zulässige Werte sind `portrait` und `landscape`. |
| `screenWidth` | Zeichenfolge | Die Anzahl der horizontalen Pixel des aktiven Displays des Geräts in der Standardausrichtung. |
| `type` | Zeichenfolge | Der Typ des zu verfolgenden Geräts. Zu den zulässigen Werten gehören: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Zeichenfolge | Eine Kennung für das Gerät. Dies kann eine Kennung von DeviceAtlas oder einem anderen Dienst sein, der die verwendete Hardware identifiziert. |
| `typeIDService` | Zeichenfolge | Der Namespace des Dienstes, der zur Identifizierung des Gerätetyps verwendet wird. Weitere Informationen zu akzeptierten Werten finden Sie im [Anhang](#typeIDService) . |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Gerät] .

## Akzeptierte Werte für typeIDService {#typeIDService}

In der folgenden Tabelle sind die zulässigen Werte für `typeIDService` und die zugehörige Bedeutung aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Das Gerät wurde mithilfe von DeviceAtlas identifiziert. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Das Gerät wurde mit Adobe Campaign identifiziert. |
