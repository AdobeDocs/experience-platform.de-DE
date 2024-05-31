---
title: Bestellung von Kundenzeitstempeln
description: Erfahren Sie, wie Sie Ihren Datensätzen eine Sortierung nach Kundenzeitstempeln hinzufügen, um Konsistenz in Ihren Profildaten sicherzustellen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Bestellung von Kundenzeitstempeln

In Adobe Experience Platform ist die Datenreihenfolge bei der Aufnahme von Daten durch Streaming-Erfassung in den Profilspeicher nicht standardmäßig garantiert. Bei der Sortierung von Kundenzeitstempeln können Sie sicherstellen, dass die neueste Nachricht gemäß dem bereitgestellten Kundenzeitstempel im Profilspeicher beibehalten wird. Alle veralteten Nachrichten werden dann abgelegt und **not** für die Verwendung in nachgelagerten Diensten verfügbar sein, die Profildaten wie Segmentierung und Ziele verwenden. Dadurch können Ihre Profildaten konsistent sein und Ihre Profildaten mit Ihren Quellsystemen synchronisieren.

Um die Sortierung von Kundenzeitstempeln zu aktivieren, verwenden Sie die `extSourceSystemAudit.lastUpdatedDate` -Feld innerhalb der [Datentyp &quot;Externe Quell-System-Auditattribute&quot;](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) und wenden Sie sich mit Ihren Sandbox- und Datensatzinformationen an Ihren Adobe Technical Account Manager oder an die Adobe-Kundenunterstützung.

## Begrenzungen

In dieser privaten Beta-Version gelten bei der Verwendung der Sortierung von Kundenzeitstempeln die folgenden Einschränkungen:

- Sie können die Reihenfolge der Kundenzeitstempel nur mit **Profilattribute** erfasst mit **Streaming-Erfassung** im Profilspeicher.
   - Es gibt **no** Bestellgarantien für Daten im Data Lake oder Identity Service.
- Sie können die Reihenfolge der Kundenzeitstempel nur in **Nicht-Produktion** Sandboxes.
- Sie können die Reihenfolge der Kundenzeitstempel nur auf **5** Datensätze pro Sandbox.
- You **cannot** Verwenden Sie Streaming-Aufrufe, um partielle Zeilenaktualisierungen in einem Datensatz zu senden, für den die Sortierung von Kundenzeitstempeln aktiviert ist.
- Die `extSourceSystemAudit.lastUpdatedDate` field **must** im [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) Format. Bei Verwendung des ISO 8601-Formats **must** als vollständiger Datum/Uhrzeit im Format `yyyy-MM-ddTHH:mm:ss.sssZ` (zum Beispiel: `2028-11-13T15:06:49.001Z`).
- Alle Zeilen der aufgenommenen Daten **must** enthält `extSourceSystemAudit.lastUpdatedDate` als Feldergruppe der obersten Ebene. Das bedeutet, dass dieses Feld **must** nicht innerhalb des XDM-Schemas verschachtelt sein. Wenn dieses Feld fehlt oder ein falsches Format aufweist, wird der fehlerhafte Datensatz **not** erfasst und eine entsprechende Fehlermeldung gesendet.
- Jeder Datensatz, der für die Sortierung von Kundenzeitstempeln aktiviert wurde **must** ein neuer Datensatz ohne zuvor erfasste Daten sein.
- Für ein bestimmtes Profilfragment nur Zeilen mit einer neueren `extSourceSystemAudit.lastUpdatedDate` wird erfasst. Zeilen, die eine `extSourceSystemAudit.lastUpdatedDate` werden verworfen, die älter oder das gleiche Alter sind.

## Empfehlungen

Beachten Sie bei der Implementierung der Sortierung von Kundenzeitstempeln die folgenden Aspekte:

- Sie sind für die Synchronisierung der Uhren auf allen internen Systemen verantwortlich, die Daten an den Profilspeicher senden.
- In Zeitstempeln im ISO 8061-Format sollten Sie eine Genauigkeit von Millisekunden haben.
