---
title: Edge-Profile
description: Erfahren Sie mehr über Edge-Profile sowie die zugehörige Terminologie, verfügbare Regionen für Edge-Profile sowie verfügbare Dienste für Edge-Profile.
source-git-commit: 3c6f885f3962caff5f10980b8811f42e02b64f85
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 5%

---


# Edge-Profile

In Adobe Experience Platform ist das Echtzeit-Kundenprofil die einzige &quot;Source of Truth&quot; für Entitätsdaten. Diese Profildaten befinden sich in einem zentralen Hub und ermöglichen die Verwendung von Fällen, die auf die Vollständigkeit und Vollständigkeit Ihrer Daten angewiesen sind. In Echtzeit-Anwendungsfällen, bei denen die Zeitempfindlichkeit wichtiger ist, sind jedoch Kantenprofile die bevorzugte Option. Edge-Profile sind einfache Profile, die an Edges sitzen und bei der Echtzeit-Personalisierung helfen.

Adobe-Anwendungen wie Adobe Target, Custom Personalization Destination und Adobe Campaign verwenden beispielsweise Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden.

## Terminologie {#terminology}

Achten Sie beim Arbeiten mit Kanten darauf, die folgenden Konzepte zu verstehen:

- **Edge**: Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht.
- **Projektkonfiguration**: Eine Projektionskonfiguration beschreibt, wie eine bestimmte Entität für einen bestimmten Kunden an den Edges repliziert werden soll und unter welchen Bedingungen. Beispiel: Bei Luma (einem Beispielkunden) sollten sich nur die Felder age und gender aus dem Datensatz, der dem Profilschema folgt, an die Edges ausdehnen.
- **Edge-Projektion**: Eine Edge-Projektion ist die Anwendung einer Projektionskonfiguration an einem bestimmten Edge auf ein Datenelement mit einer eindeutigen ID, die einem bestimmten Schema für einen bestimmten Kunden entspricht. Beispiel: eine Entität, die das Profilschema mit ID berücksichtigt `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, Besucher der Luma-Website, repliziert in das VA6-Rechenzentrum, mit den Feldern `age = 35` und `gender = male`.

Anders ausgedrückt: Daten werden durch eine Projektion an eine Kante weitergeleitet, wobei die **Projektionsziel** Definieren **,** Edge, an den die Daten gesendet werden, und die **Projektionskonfiguration** Definieren **what** -Daten werden an den angegebenen Edge gesendet.

## Verfügbare Regionen {#regions}

Die folgenden Regionen können mit Edge verwendet werden:

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Alle diese Regionen sind gültige Optionen, in denen Profile landen können.

## Verfügbare Dienste {#services}

Die folgenden Dienste sind für die Profilsuche an der Edge aktiviert:

- [Edge Profile Configuration Service](#edge-profile-configuration-service)
- [Projektor Worker-Dienst](#mepw)
- [Express Profile Service](#xps)

### Edge Profile Configuration Service {#edge-profile-configuration-service}

Der Edge Profile Configuration Service stellt APIs für nachgelagerte Lösungen und Anwendungen zur Erstellung von Projektionskonfigurationen bereit. Sie können diese APIs verwenden, um die Attribute und Zielgruppen eines Profils anzugeben, das an die Edges gesendet werden soll, sowie die Edge-Regionen, an die die Projektion gesendet werden soll. Zu diesem Zeitpunkt können Sie **any** der Randbereiche für Projektionen.

### Projektor Worker-Dienst {#mepw}

Der Projection Worker Service (MEPW) überwacht Änderungen, die am Hub in Profilen stattfinden. Nach Prüfung der Änderungen in den Konfigurationen bereitet dieser Dienst die Projektionen vor und sendet sie an die zuvor angegebenen Edge-Regionen. Darüber hinaus verarbeitet dieser Dienst die Anforderungen zur Entitätsaktualisierung und sendet die erforderlichen Projektionen an die erforderlichen Regionen. Entitätsaktualisierungen werden verwendet, um sicherzustellen, dass auf die Entität mit hoher Verfügbarkeit zugegriffen werden kann.

### Express Profile Service {#xps}

Der Express Profile Service (XPS) ruft die Profile an den verschiedenen Edges ab. Dieser Dienst empfängt Anforderungen von nachgelagerten Lösungen wie Adobe Target- oder Custom Personalization-Zielen, sucht die Profile aus den Datenbanken an den Edges und sendet das angeforderte Profil an die anfragende Lösung. Wenn das Profil nicht gefunden wird, wird eine Aktualisierungsanforderung an den zugehörigen Hub gesendet.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs sollten Sie über grundlegende Kenntnisse zu Kantenprofilen verfügen, einschließlich Informationen zu den verfügbaren Regionen und Diensten für Kantenprofile. Weitere Informationen zu Edge-Projektionen finden Sie im [Endpunktleitfaden für Edge-Projektionen](./api/edge-projections.md). Weitere Informationen zum Adobe Experience Edge finden Sie im Abschnitt [Edge-Übersicht](../edge/home.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zu Edge-Profilen:

### In welchen Regionen können Kantenprofile landen?

Edge-Profile können je nach Situation in verschiedenen Regionen landen.

Bei Projektionskonfigurationen werden alle Änderungen am Profil auf alle Regionen übertragen, die in der Profilkonfiguration erwähnt werden.

Darüber hinaus verfügt jedes Kantenprofil über ein Schemaattribut namens User Activity Region (UAR). Alle Edges, die dieses Profil in den letzten 14 Tagen besucht hat, sind in diesem Profilattribut aufgeführt. Wenn dieses Attribut in einem Profil vorhanden ist, werden daher auch alle Änderungen am Profil an alle in der UAR-Datei aufgelisteten Regionen gesendet.

### Wie funktionieren Datenabläufe mit Kantenprofilen?

Bei Kantenprofilen bestimmt der Datenablauf, wie lange das Profil auf der Kante bleibt, bevor es entfernt wird. Datengültigkeit **rollierend**: Jedes Mal, wenn auf das Profil an der Kante zugegriffen wird, wird die Datenablaufzeit zurückgesetzt.

Sie können Ihren Kantenprofilen einen Datenablauf hinzufügen, indem Sie ihn zum [Kantenprojektion](./api/edge-projections.md). Standardmäßig läuft die Datengültigkeit 14 Tage an, kann jedoch auf eine Mindestdauer von 1 Stunde und eine Höchstdauer von 90 Tagen eingestellt werden.
