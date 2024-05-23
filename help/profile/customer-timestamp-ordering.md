---
title: Bestellung von Kundenzeitstempeln
description: Erfahren Sie, wie Sie Ihren Datensätzen eine Sortierung nach Kundenzeitstempeln hinzufügen, um Konsistenz in Ihren Profildaten sicherzustellen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Bestellung von Kundenzeitstempeln

In Adobe Experience Platform ist die Datenreihenfolge beim Erfassen von Daten durch Streaming-Erfassung in den Profilspeicher nicht automatisch gewährleistet. Bei der Sortierung von Kundenzeitstempeln können Sie sicherstellen, dass die neueste Nachricht gemäß dem bereitgestellten Kundenzeitstempel im Profilspeicher beibehalten wird. Dadurch können Ihre Profildaten konsistent sein und Ihre Profildaten mit Ihren Quellsystemen synchronisieren.

Um die Sortierung von Kundenzeitstempeln zu aktivieren, müssen Sie die `lastUpdatedDate` -Feld innerhalb der [Datentyp &quot;Externe Quell-System-Auditattribute&quot;](../xdm/data-types/external-source-system-audit-attributes.md) und wenden Sie sich mit Ihren Sandbox- und Datensatzinformationen an Ihren Adobe Technical Account Manager oder an die Adobe-Kundenunterstützung.

## Begrenzungen

In dieser privaten Beta-Version gelten bei der Verwendung der Sortierung von Kundenzeitstempeln die folgenden Einschränkungen:

- Sie können die Reihenfolge der Kundenzeitstempel nur mit **Profilattribute** erfasst mit **Streaming-Erfassung**.
- Sie können die Reihenfolge der Kundenzeitstempel nur in **Nicht-Produktion** Sandboxes.
- Sie können die Reihenfolge der Kundenzeitstempel nur auf **5** Datensätze pro Sandbox.
- Die `lastUpdatedDate` -Feld muss sich im [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) Format.
- Alle Zeilen der aufgenommenen Daten **must** enthält `lastUpdatedDate` -Feld. Wenn dieses Feld fehlt oder ein falsches Format aufweist, schlägt die Aufnahme fehl.
- Jeder Datensatz, der für die Sortierung von Kundenzeitstempeln aktiviert wurde **must** ein neuer Datensatz ohne zuvor erfasste Daten sein.
- Für ein bestimmtes Profilfragment nur Zeilen mit einer neueren `lastUpdatedDate` wird erfasst. Wenn die Zeile keine neuere `lastUpdatedDate`, wird die Zeile verworfen.

## Empfehlungen

Beachten Sie bei der Implementierung der Sortierung von Kundenzeitstempeln die folgenden Aspekte:

- Sie sind für die Synchronisierung der Uhren auf allen internen Systemen verantwortlich, die Daten an den Profilspeicher senden.
- In Zeitstempeln im ISO 8061-Format sollten Sie eine Genauigkeit von Millisekunden haben.
- Die Verwendung der Datenvorbereitung in Abstimmung mit der Reihenfolge der Kundenzeitstempel ist **hoch empfohlen** erstellt eine Kopie aller aufgenommenen Zeilen zusammen mit ihren Zeitstempeln, was bei auftretenden Problemen eine bessere Fehlerbehebung ermöglicht.
