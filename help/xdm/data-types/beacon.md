---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Beacon;Interaktionsdetails;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Beacon-Datentyp
description: Erfahren Sie mehr über die Klasse „XDM Individual Profile“.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# [!UICONTROL Beacon]-Datentyp

[!UICONTROL Beacon] ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen übermittelt, wenn mobile Geräte in Reichweite kommen.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconMajor` | Double | Hauptwerte identifizieren und eine Gruppe unterscheiden und vorzeichenlose Ganzzahlwerte zwischen 1 und 65.535. |
| `beaconMinor` | Double | Nebenwerte identifizieren und unterscheiden eine Person und vorzeichenlose Ganzzahlwerte zwischen 1 und 65.535. |
| `proximity` | String | Geschätzte Entfernung vom Beacon. Siehe [Anhang](#proximity) für akzeptierte Werte und Definitionen. |
| `proximityUUID` | String | Eine Proximity UUID (Universally Unique Identifier) ist eine spezielle Art von Kennung, mit der Beacons in Ihrem Netzwerk von allen anderen Beacons in Netzwerken außerhalb Ihrer Kontrolle unterschieden werden. Die Proximity UUID wird zu einem Beacon konfiguriert, das an Mobilgeräte in Reichweite übertragen wird, um die Beacons einer Organisation zu identifizieren. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen [!UICONTROL  Datentyp ]Beacon“.

## Akzeptierte Werte für die Nähe {#proximity}

In der folgenden Tabelle sind die akzeptierten Werte für `proximity` und ihre zugehörigen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `immediate` | Innerhalb weniger Zentimeter. |
| `near` | Weniger als 10 Meter entfernt. |
| `far` | Mehr als 10 Meter entfernt. |
| `unknown` | Der Abstand konnte nicht ermittelt werden, wahrscheinlich aufgrund eines schwachen Signals. |
