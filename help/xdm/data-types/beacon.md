---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Beacon; Interaktionsdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Beacon-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Klasse "XDM Individual Profile".
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 7%

---

#  Beacondata-Typ

 Beaconis ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen übermittelt, wenn mobile Geräte in Reichweite sind.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconMajor` | Double | Wichtige Werte identifizieren und unterscheiden eine Gruppe und vorzeichenlose ganzzahlige Werte zwischen 1 und 65.535. |
| `beaconMinor` | Double | Geringfügige Werte kennzeichnen und unterscheiden einzelne und nicht vorzeichenbehaftete ganzzahlige Werte zwischen 1 und 65.535. |
| `proximity` | Zeichenfolge | Geschätzte Entfernung vom Beacon. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#proximity) . |
| `proximityUUID` | Zeichenfolge | Eine Näherungs-UUID (Universally Unique Identifier) ist ein spezieller Kennungstyp, mit dem Beacons in Ihrem Netzwerk von allen anderen Beacons in Netzwerken außerhalb Ihrer Kontrolle unterschieden werden. Die Näherungs-UUID wird in ein Beacon konfiguriert, das an Mobilgeräte im Bereich der Identifizierung der Beacons eines Unternehmens übertragen wird. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Beacon].

## Zulässige Werte für räumliche Nähe {#proximity}

In der folgenden Tabelle sind die zulässigen Werte für `proximity` und die zugehörige Bedeutung aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `immediate` | Innerhalb weniger Zentimeter. |
| `near` | Weniger als 10 Meter entfernt. |
| `far` | Mehr als 10 Meter entfernt. |
| `unknown` | Die Entfernung konnte nicht ermittelt werden, wahrscheinlich aufgrund eines schwachen Signals. |
