---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Beacon;Interaktionsdetails;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Beacon-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 6%

---

#  Beacondata-Typ

 Beaconis ist ein standardmäßiger XDM-Datentyp, der das Wireless-Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weitergibt, wenn mobile Geräte in Reichweite kommen.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconMajor` | Double | Hauptwerte identifizieren und unterscheiden eine Gruppe und vorzeichenlose Ganzzahlwerte zwischen 1 und 65.535. |
| `beaconMinor` | Dublette | Geringfügige Werte identifizieren und unterscheiden eine einzelne und vorzeichenlose Ganzzahl zwischen 1 und 65.535. |
| `proximity` | Zeichenfolge | Geschätzte Entfernung vom Beacon. Akzeptierte Werte und Definitionen finden Sie im Anhang [a1/>.](#proximity) |
| `proximityUUID` | Zeichenfolge | Eine UUID für die Nähe (Universally Unique Identifier) ist ein spezieller Identifizierungstyp, mit dem Beacons in Ihrem Netzwerk von allen anderen Beacons in Netzwerken außerhalb Ihrer Kontrolle unterschieden werden. Die UUID für die Nähe wird zu einem Beacon konfiguriert, der auf Mobilgeräte im Bereich der Identifizierung der Beacons eines Unternehmens übertragen wird. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Datentyp [!UICONTROL Beacon].

## Akzeptierte Werte für Nähe {#proximity}

In der folgenden Tabelle sind die für `proximity` zulässigen Werte und die damit verbundenen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `immediate` | Innerhalb weniger Zentimeter. |
| `near` | Weniger als 10 Meter entfernt. |
| `far` | Über 10 Meter entfernt. |
| `unknown` | Die Entfernung konnte nicht festgestellt werden, wahrscheinlich aufgrund eines schwachen Signals. |
