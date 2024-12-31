---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Gerät;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Gerätedatentyp
description: Erfahren Sie mehr über den Geräte-XDM-Datentyp.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 19%

---

# [!UICONTROL Gerät] Datentyp

[!UICONTROL Device] ist ein standardmäßiger XDM-Datentyp, der ein identifiziertes Gerät beschreibt. Ein Gerät ist eine Anwendungs- oder Browser-Instanz, die sitzungsübergreifend verfolgt werden kann, normalerweise durch Cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `colorDepth` | Ganzzahl | Die Anzahl der Farben, die die Anzeige darstellen kann. |
| `manufacturer` | String | Der Name der Organisation, der das Design und die Erstellung des Geräts gehört. |
| `model` | String | Der Name des Modells für das Gerät. Dies ist der gängige, für Menschen lesbare oder Marketing-Name des Geräts. So ist beispielsweise das &quot;iPhone 6S“ ein besonderes Handymodell. |
| `modelNumber` | String | Die eindeutige Modellnummer, die vom Hersteller für dieses Gerät zugewiesen wurde. Modellnummern sind keine Versionen, sondern eindeutige Kennungen, die eine bestimmte Modellkonfiguration identifizieren. |
| `screenHeight` | Ganzzahl | Die Anzahl der vertikalen Pixel des aktiven Displays des Geräts in der Standardausrichtung. |
| `screenOrientation` | String | Die aktuelle Bildschirmausrichtung. Zu den akzeptierten Werten gehören `portrait` und `landscape`. |
| `screenWidth` | String | Die Anzahl der horizontalen Pixel des aktiven Displays des Geräts in der Standardausrichtung. |
| `type` | String | Der Typ des zu verfolgenden Geräts. Zu den akzeptierten Werten gehören: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | String | Eine Kennung für das Gerät. Dies kann eine Kennung aus DeviceAtlas oder einem anderen Service sein, der die verwendete Hardware identifiziert. |
| `typeIDService` | String | Der Namespace des Services, der zur Identifizierung des Gerätetyps verwendet wird. Siehe [Anhang](#typeIDService) für Details zu den akzeptierten Werten. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Gerät].

## Akzeptierte Werte für typeIDService {#typeIDService}

In der folgenden Tabelle sind die akzeptierten Werte für `typeIDService` und ihre zugehörigen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Das Gerät wurde mit DeviceAtlas identifiziert. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Das Gerät wurde mit Adobe Campaign identifiziert. |
