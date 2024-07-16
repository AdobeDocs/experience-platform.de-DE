---
title: Bestellung von Kundenzeitstempeln
description: Erfahren Sie, wie Sie Ihren Datensätzen eine Sortierung nach Kundenzeitstempeln hinzufügen, um Konsistenz in Ihren Profildaten sicherzustellen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Bestellung von Kundenzeitstempeln

In Adobe Experience Platform ist die Datenreihenfolge bei der Aufnahme von Daten durch Streaming-Erfassung in den Profilspeicher nicht standardmäßig garantiert. Bei der Sortierung von Kundenzeitstempeln können Sie sicherstellen, dass die neueste Nachricht gemäß dem bereitgestellten Kundenzeitstempel im Profilspeicher beibehalten wird. Alle veralteten Nachrichten werden dann gelöscht und **nicht** steht für die Verwendung in nachgelagerten Diensten zur Verfügung, die Profildaten wie Segmentierung und Ziele verwenden. Dadurch können Ihre Profildaten konsistent sein und Ihre Profildaten mit Ihren Quellsystemen synchronisieren.

Um die Sortierung von Kundenzeitstempeln zu aktivieren, verwenden Sie das Feld `extSourceSystemAudit.lastUpdatedDate` in der Feldergruppe [Externe Source-Systemaudit-Attribute](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) und wenden Sie sich mit Ihren Sandbox- und Datensatzinformationen an Ihren Adobe Technical Account Manager oder an die Adobe-Kundenunterstützung.

## Begrenzungen

In dieser privaten Beta-Version gelten bei der Verwendung der Sortierung von Kundenzeitstempeln die folgenden Einschränkungen:

- Sie können die Sortierung von Kundenzeitstempeln nur mit **Profilattributen** verwenden, die mit **Streaming-Erfassung** im Profilspeicher erfasst werden.
   - Es gibt **no** Bestellgarantien für Daten im Data Lake oder Identity Service.
- Sie können die Sortierung von Kundenzeitstempeln nur für **Nicht-Produktion** -Sandboxes verwenden.
- Sie können die Reihenfolge von Kundenzeitstempeln nur auf **5** Datensätze pro Sandbox anwenden.
- Sie können **nicht** Streaming-Upserts verwenden, um Teilzeilenaktualisierungen in einem Datensatz zu senden, für den die Sortierung von Kundenzeitstempeln aktiviert ist.
- Das Feld `extSourceSystemAudit.lastUpdatedDate` **muss** im Format [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) aufweisen. Bei Verwendung des ISO 8601-Formats muss **1} als vollständiger Datum im Format `yyyy-MM-ddTHH:mm:ss.sssZ` sein (z. B. `2028-11-13T15:06:49.001Z`).**
- Alle Zeilen der erfassten Daten **müssen** das Feld `extSourceSystemAudit.lastUpdatedDate` als Feldergruppe der obersten Ebene enthalten. Das bedeutet, dass dieses Feld **must** nicht im XDM-Schema verschachtelt ist. Wenn dieses Feld fehlt oder ein falsches Format aufweist, wird der fehlerhafte Datensatz **nicht** erfasst und eine entsprechende Fehlermeldung wird gesendet.
- Jeder Datensatz, der für die Sortierung von Kunden-Zeitstempeln **aktiviert wurde, muss** ein neuer Datensatz ohne zuvor erfasste Daten sein.
- Für ein bestimmtes Profilfragment werden nur Zeilen erfasst, die eine aktuellere `extSourceSystemAudit.lastUpdatedDate` enthalten. Zeilen, die eine `extSourceSystemAudit.lastUpdatedDate` enthalten, die älter oder im selben Alter ist, werden verworfen.

## Empfehlungen

Beachten Sie bei der Implementierung der Sortierung von Kundenzeitstempeln die folgenden Aspekte:

- Sie sind für die Synchronisierung der Uhren auf allen internen Systemen verantwortlich, die Daten an den Profilspeicher senden.
- In Zeitstempeln im ISO 8061-Format sollten Sie eine Genauigkeit von Millisekunden haben.
