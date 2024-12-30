---
title: Edge-Profile
description: Erfahren Sie mehr über Edge-Profile sowie die zugehörige Terminologie, verfügbare Regionen für Edge-Profile sowie verfügbare Services für Edge-Profile.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Edge-Profile

In Adobe Experience Platform ist das Echtzeit-Kundenprofil die zentrale Datenquelle für Entitätsdaten. Diese Profildaten befinden sich in einem zentralen Hub und unterstützen Anwendungsfälle, die auf der Vollständigkeit und Vollständigkeit Ihrer Daten basieren. In Echtzeit-Anwendungsfällen, in denen die Zeitempfindlichkeit wichtiger ist, sind jedoch Edge-Profile die bevorzugte Option. Edge-Profile sind einfache Profile, die sich an den Rändern befinden und bei Anwendungsfällen der Echtzeit-Personalisierung hilfreich sind.

Beispielsweise verwenden Adobe-Programme wie Adobe Target, Custom Personalization Destination und Adobe Campaign -Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden durch eine Projektion an einen Edge weitergeleitet, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden.

## Terminologie {#terminology}

Beim Arbeiten mit Kanten müssen Sie die folgenden Konzepte verstehen:

- **Edge**: Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht.
- **Edge-Projektion**: Eine Kantenprojektion ist die Systemprojektionsansicht eines Profils an einer bestimmten Kante, um Profildaten mit einer eindeutigen ID darzustellen, die einem bestimmten Schema für einen bestimmten Kunden entspricht. Beispiel: eine Entität, die das Profilschema mit der ID &quot;`CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`&quot; respektiert, Besucher der Luma-Website, das im VA6-Rechenzentrum repliziert wurde und die Felder &quot;`age = 35`&quot; und &quot;`gender = male`&quot; enthält.

Anders ausgedrückt werden die Daten durch eine Projektion an eine Kante weitergeleitet, wobei das **Projektionsziel** definiert, **an welche** Kante die Daten gesendet werden.

## Verfügbare Regionen {#regions}

Die folgenden Regionen stehen für die Verwendung mit Edge zur Verfügung:

- VA6
- ODER2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Alle diese Regionen sind gültige Optionen für Profile, in denen gelandet werden soll.

## Verfügbare Services {#services}

Die folgenden Services sind für die Profilsuche in Edge aktiviert:

- [Projektionsmitarbeiter-Service](#mepw)
- [Express-Profildienst](#xps)

### Projektionsmitarbeiter-Service {#mepw}

Der Projection Worker Service (MEPW) überwacht Änderungen, die am Hub in Profilen vorgenommen werden. Nach Prüfung der Konfigurationsänderungen bereitet dieser Service die Projektionen vor und sendet sie an die zuvor festgelegten Randbereiche. Darüber hinaus verarbeitet dieser Service die Aktualisierungsanfragen der Entität und sendet die erforderlichen Projektionen an die erforderlichen Regionen. Entitätsaktualisierungen werden verwendet, um sicherzustellen, dass der Zugriff auf die Entität mit hoher Verfügbarkeit möglich ist.

### Express-Profildienst {#xps}

Der Express-Profildienst (XPS) ruft die Profile an den verschiedenen Kanten ab. Dieser Service empfängt Anfragen von nachgelagerten Lösungen wie Adobe Target oder benutzerdefinierten Personalization-Zielen, sucht die Profile in den Datenbanken am Edge und sendet das angeforderte Profil an die anfragende Lösung. Wenn das Profil nicht gefunden wird, wird eine Aktualisierungsanfrage an den zugehörigen Hub gesendet.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs sollten Sie über ein grundlegendes Verständnis von Edge-Profilen verfügen, einschließlich Informationen zu den verfügbaren Regionen und Services für Edge-Profile. Weitere Informationen zum Adobe von Experience Edge finden Sie in der [Edge Network-Übersicht](../web-sdk/home.md#edge-network).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu Edge-Profilen:

### In welchen Regionen können Edge-Profile landen?

Edge-Profile können je nach Situation in verschiedenen Regionen landen.

Darüber hinaus verfügt jedes Edge-Profil über ein Schemaattribut namens „Benutzeraktivitätsregion (UAR)“. In diesem Profilattribut sind alle Kanten aufgeführt, die dieses Profil in den letzten 14 Tagen besucht hat. Wenn dieses Attribut in einem Profil vorhanden ist, werden daher alle Änderungen am Profil auch an alle in der UAR aufgeführten Regionen gesendet.

### Wie funktioniert das Ablaufen von Daten mit Edge-Profilen?

Bei Edge-Profilen bestimmt der Datenablauf, wie lange das Profil im Edge verbleibt, bevor es entfernt wird. Datenablauf ist **rollierend** d. h., bei jedem Zugriff auf das Profil im Randbereich wird die Datenablaufzeit zurückgesetzt. Standardmäßig beträgt der Ablauf der Daten 14 Tage.

### Welche Daten werden im Edge-Profil gespeichert?

Edge Profile speichert die Profilattribute, Profil-IDs sowie qualifizierte Zielgruppen-IDs. Standardmäßig beträgt der Ablauf der Daten 14 Tage.
