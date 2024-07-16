---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Beacon; Interaktionsdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Beacon-Datentyp
description: Erfahren Sie mehr über die Klasse XDM Individual Profile .
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# [!UICONTROL Beacon]-Datentyp

[!UICONTROL Beacon] ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weitergibt, wenn mobile Geräte in Reichweite sind.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconMajor` | Double | Hauptwerte identifizieren und eine Gruppe unterscheiden und vorzeichenlose Ganzzahlwerte zwischen 1 und 65.535. |
| `beaconMinor` | Double | Nebenwerte identifizieren und unterscheiden eine Person und vorzeichenlose Ganzzahlwerte zwischen 1 und 65.535. |
| `proximity` | Zeichenfolge | Geschätzte Entfernung vom Beacon. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#proximity) . |
| `proximityUUID` | Zeichenfolge | Eine Näherungs-UUID (Universally Unique Identifier) ist ein spezieller Kennungstyp, mit dem Beacons in Ihrem Netzwerk von allen anderen Beacons in Netzwerken außerhalb Ihrer Kontrolle unterschieden werden. Die Näherungs-UUID wird in ein Beacon konfiguriert, das an Mobilgeräte im Bereich der Identifizierung der Beacons eines Unternehmens übertragen wird. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

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
