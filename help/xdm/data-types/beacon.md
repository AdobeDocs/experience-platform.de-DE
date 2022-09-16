---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Beacon; Interaktionsdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Beacon-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Klasse "XDM Individual Profile".
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 12%

---

# [!UICONTROL Beacon] Datentyp

[!UICONTROL Beacon] ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weitergibt, wenn mobile Geräte in Reichweite sind.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconMajor` | Double | Wichtige Werte identifizieren und unterscheiden eine Gruppe und vorzeichenlose ganzzahlige Werte zwischen 1 und 65.535. |
| `beaconMinor` | Double | Geringfügige Werte kennzeichnen und unterscheiden einzelne und nicht vorzeichenbehaftete ganzzahlige Werte zwischen 1 und 65.535. |
| `proximity` | Zeichenfolge | Geschätzte Entfernung vom Beacon. Siehe [Anhang](#proximity) für akzeptierte Werte und Definitionen. |
| `proximityUUID` | Zeichenfolge | Eine Näherungs-UUID (Universally Unique Identifier) ist ein spezieller Kennungstyp, mit dem Beacons in Ihrem Netzwerk von allen anderen Beacons in Netzwerken außerhalb Ihrer Kontrolle unterschieden werden. Die Näherungs-UUID wird in ein Beacon konfiguriert, das an Mobilgeräte im Bereich der Identifizierung der Beacons eines Unternehmens übertragen wird. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum [!UICONTROL Beacon] Datentyp.

## Zulässige Werte für räumliche Nähe {#proximity}

In der folgenden Tabelle sind die für `proximity` und ihre zugehörige Bedeutung:

| Wert | Beschreibung |
| --- | --- |
| `immediate` | Innerhalb weniger Zentimeter. |
| `near` | Weniger als 10 Meter entfernt. |
| `far` | Mehr als 10 Meter entfernt. |
| `unknown` | Die Entfernung konnte nicht ermittelt werden, wahrscheinlich aufgrund eines schwachen Signals. |
