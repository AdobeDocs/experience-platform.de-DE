---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schema;Gerät;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Gerätetyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp des Geräts.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 18%

---

# [!UICONTROL Gerätetyp ] 

[!UICONTROL Ein ] XDM-Standarddatentyp, der ein bestimmtes Gerät beschreibt. Ein Gerät ist eine Anwendung oder eine Browserinstanz, die sitzungsübergreifend verfolgt werden kann, normalerweise mit Cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `colorDepth` | Ganzzahl | Die Anzahl der Farben, die die Anzeige darstellen kann. |
| `manufacturer` | Zeichenfolge | Der Name der Organisation, der der Entwurf und die Erstellung des Geräts gehören. |
| `model` | Zeichenfolge | Der Name des Modells für das Gerät. Dies ist der übliche, für Menschen lesbare oder Marketingname für das Gerät. Das &quot;iPhone 6S&quot;ist beispielsweise ein bestimmtes Mobiltelefonmodell. |
| `modelNumber` | Zeichenfolge | Die eindeutige Modellnummer, die vom Hersteller für dieses Produkt zugewiesen wurde. Modellnummern sind keine Versionen, sondern eindeutige Bezeichner, die eine bestimmte Modellkonfiguration identifizieren. |
| `screenHeight` | Ganzzahl | Die Anzahl der vertikalen Pixel der aktiven Anzeige des Geräts in der Standardausrichtung. |
| `screenOrientation` | Zeichenfolge | Die aktuelle Bildschirmausrichtung. Zu den zulässigen Werten gehören `portrait` und `landscape`. |
| `screenWidth` | Zeichenfolge | Die Anzahl der horizontalen Pixel der aktiven Anzeige des Geräts in der Standardausrichtung. |
| `type` | Zeichenfolge | Der Typ des verfolgten Geräts. Zu den zulässigen Werten gehören: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Zeichenfolge | Eine Kennung für das Gerät. Dies kann eine Kennung von DeviceAtlas oder ein anderer Dienst sein, der die verwendete Hardware identifiziert. |
| `typeIDService` | Zeichenfolge | Der Namespace des Diensts, mit dem der Gerätetyp identifiziert wird. Einzelheiten zu den zulässigen Werten finden Sie im Anhang [Anhang](#typeIDService). |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Datentyp [!UICONTROL Gerät].

## Akzeptierte Werte für typeIDService {#typeIDService}

In der folgenden Tabelle sind die für `typeIDService` zulässigen Werte und die damit verbundenen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Das Gerät wurde mit DeviceAtlas identifiziert. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Das Gerät wurde mit Adobe Campaign identifiziert. |
