---
title: Kundenzeitstempel-Sortierung
description: Erfahren Sie, wie Sie Ihren Datensätzen eine Zeitstempelreihenfolge von Kunden hinzufügen, um Konsistenz in Ihren Profildaten sicherzustellen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Kunden-Zeitstempel sortieren

In Adobe Experience Platform ist die Datenreihenfolge bei der Aufnahme von Daten über die Streaming-Aufnahme in den Profilspeicher nicht standardmäßig gewährleistet. Bei der Sortierung von Kundenzeitstempeln können Sie garantieren, dass die neueste Nachricht gemäß dem bereitgestellten Kundenzeitstempel im Profilspeicher beibehalten wird. Alle veralteten Nachrichten werden dann gelöscht und stehen **nicht** für nachgelagerte Services zur Verfügung, die Profildaten wie Segmentierung und Ziele verwenden. Auf diese Weise bleiben Ihre Profildaten konsistent und Ihre Profildaten mit Ihren Quellsystemen synchronisiert.

Um die Sortierung von Zeitstempeln durch Kunden zu aktivieren, verwenden Sie das Feld `extSourceSystemAudit.lastUpdatedDate` in der Feldergruppe [Externe Source-Systemüberwachungsattribute](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) und wenden Sie sich mit Ihrer Sandbox und Ihren Datensatzinformationen an Ihren technischen Adobe-Kundenbetreuer oder die Adobe-Kundenunterstützung.

## Begrenzungen

In dieser privaten Beta-Version gelten die folgenden Einschränkungen bei der Verwendung der Zeitstempelreihenfolge für Kunden:

- Sie können die Kundenzeitstempelreihenfolge nur mit **Profilattributen** verwenden, die mit **Streaming-Aufnahme** im Profilspeicher aufgenommen werden.
   - Für **Daten im Data Lake** Identity Service werden keine Bestellgarantien bereitgestellt.
- Sie können die Kundenzeitstempelreihenfolge nur für (produktionsfremde **Sandboxes**.
- Sie können die Kundenzeitstempelreihenfolge nur auf **5** Datensätze pro Sandbox anwenden.
- Sie **nicht** Streaming-Upserts verwenden, um partielle Zeilenaktualisierungen in einem Datensatz zu senden, in dem die Kundenzeitstempelreihenfolge aktiviert ist.
- Das `extSourceSystemAudit.lastUpdatedDate` Feld **muss** im Format [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) vorliegen. Bei Verwendung des ISO 8601 **Formats muss** im Format `yyyy-MM-ddTHH:mm:ss.sssZ` (z. B. `2028-11-13T15:06:49.001Z`) als vollständiger Datums-/Uhrzeitwert angegeben werden.
- Alle aufgenommenen Datenzeilen **müssen** das `extSourceSystemAudit.lastUpdatedDate` Feld als Feldergruppe der obersten Ebene enthalten. Dies bedeutet, dass dieses **(**) nicht im XDM-Schema verschachtelt sein darf. Wenn dieses Feld fehlt oder in einem falschen Format vorliegt, wird der falsch formatierte Datensatz **nicht** aufgenommen und eine entsprechende Fehlermeldung wird gesendet.
- Jeder Datensatz, der für die Kundenzeitstempelreihenfolge aktiviert **muss** ein neuer Datensatz ohne zuvor aufgenommene Daten sein.
- Für ein bestimmtes Profilfragment werden nur Zeilen aufgenommen, die eine neuere `extSourceSystemAudit.lastUpdatedDate` enthalten. Zeilen, die eine `extSourceSystemAudit.lastUpdatedDate` enthalten, die entweder älter oder gleich alt ist, werden verworfen.

## Empfehlungen

Beachten Sie bei der Implementierung der Kundenzeitstempelreihenfolge die folgenden Überlegungen:

- Sie sind für die Synchronisierung der Uhren auf allen internen Systemen verantwortlich, die Daten an den Profilspeicher senden.
- Sie sollten in Ihren ISO 8061-formatierten Zeitstempeln eine Präzision auf Millisekundenebene haben.
