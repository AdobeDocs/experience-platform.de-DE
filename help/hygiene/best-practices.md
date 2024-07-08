---
title: Best Practices für erweitertes Data Lifecycle Management
description: Erfahren Sie, wie Sie mit der erweiterten Benutzeroberfläche für Data Lifecycle Management und der Data Hygiene-API Datenanforderungen in Adobe Experience Platform effizient verwalten können. In diesem Handbuch werden Best Practices beschrieben, wie das Maximieren von Identitäten pro Anfrage, das Festlegen einzelner Datensätze und die Berücksichtigung von API-Einschränkungen zur Vermeidung von Verlangsamungen. Das Dokument enthält Richtlinien zum Einrichten der automatischen Datensatzbereinigung, zum Überwachen des Status der Arbeitsaufträge und detaillierte Methoden zum Abrufen von Antworten. Befolgen Sie diese Verfahren, um die Anforderungsverarbeitung zu optimieren und die Antwortzeiten zu optimieren.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Best Practices für die erweiterte Lebenszyklusverwaltung

Verwenden Sie die Advanced Data Lifecycle Management-Benutzeroberfläche und die Data Hygiene-API, um Bereinigungsanfragen effizient zu verwalten und Daten aus Adobe Experience Platform-Diensten zu entfernen. Befolgen Sie diese Best Practices, um Ihre Anforderungsverarbeitung zu optimieren und die Antwortzeiten für die Fertigstellung zu optimieren.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des Arbeitsbereichs &quot;Datenlebenszyklus&quot;und der [Data Hygiene API](./api/overview.md). Machen Sie sich mit den Handbüchern vertraut, bevor Sie mit diesem Dokument fortfahren [Advanced Data Lifecycle Management](./home.md) und [Erstellen von Löschanfragen für Datensätze](./ui/record-delete.md) oder [Datensatzabläufe in der Benutzeroberfläche](./ui/dataset-expiration.md)oder über die API.

## Richtlinien zur Erstellung von Arbeitsbestellungen {#work-order-creation-guidelines}

Sie können die `/workorder` -Endpunkt in der Data Hygiene-API zur programmatischen Verwaltung von Löschanfragen von Datensätzen in Experience Platform. Mit diesem Endpunkt können Sie eine Löschanfrage erstellen, ihren Status überprüfen oder eine vorhandene Anforderung aktualisieren. Siehe [Arbeitserstellungsendpunkt-Dokument](./api/workorder.md) , um zu erfahren, wie Sie diese Aktionen mit der API durchführen.

>[!TIP]
>
>Ein Arbeitsauftrag ist eine strukturierte Anforderung, die spezifische Datenverwaltungsvorgänge wie Datenbereinigung oder -umwandlung durchführt, um eine effiziente und systematische Verarbeitung zu gewährleisten.

Befolgen Sie diese Richtlinien, um Ihre Datenbereinigungsanforderungen zu optimieren:

1. **Identitäten pro Anforderung maximieren:** Binden Sie bis zu 100.000 Identitäten pro Bereinigungsanfrage ein, um die Effizienz zu steigern. Wenn Sie mehrere Identitäten in eine einzige Anfrage stapeln, können Sie die Häufigkeit von API-Aufrufen reduzieren und das Risiko von Leistungsproblemen aufgrund übermäßiger Einzelidentitätsanfragen minimieren. Senden Sie Anfragen mit maximalen Identitätszahlen, um eine schnellere Verarbeitung zu erzielen, da Arbeitsaufträge aus Effizienzgründen stapelt werden.
2. **Festlegen einzelner Datensätze:** Geben Sie für maximale Effizienz den zu verarbeitenden Datensatz an.
3. **Überlegungen zur API-Drosselung:** Achten Sie auf API-Einschränkungen, um langsame Downloads zu verhindern. Kleinere Anforderungen (&lt; 100 IDs) mit höheren Frequenzen können zu 429 Antworten führen und erfordern eine erneute Übermittlung zu akzeptablen Raten.

### 429-Fehler verwalten {#manage-429-errors}

Wenn der Fehler 429 angezeigt wird, bedeutet dies, dass Sie die zulässige Anzahl von Anfragen innerhalb eines bestimmten Zeitraums überschritten haben. Befolgen Sie diese Best Practices, um 429-Fehler effektiv zu verwalten:

- **Lesen Sie die Kopfzeile &quot;Retry-After&quot;.**: Wenn ein 429-Fehler zurückgegeben wird, überprüfen Sie die Antwortheader &quot;Retry-After&quot;. Dieser Header gibt die Wartezeit vor einem erneuten Versuch der Anfrage an.
- **Implementieren der Wiederholungslogik**: Verwenden Sie den Wert &quot;Retry-After&quot;, um die Wiederholungslogik in Ihre Anwendung zu implementieren und sicherzustellen, dass nach der angegebenen Zeit versucht wird, weitere Versuche durchzuführen, um nachfolgende 429 Fehler zu vermeiden.
- **Batch von Anforderungen**: Vermeiden Sie das schnelle Senden zahlreicher kleiner Anfragen. Stapeln Sie stattdessen mehrere Identitäten in einer einzelnen Anfrage, um die Häufigkeit von Aufrufen zu reduzieren und das Risiko zu minimieren, dass Quotenbeschränkungen erreicht werden.

## Ablaufdatum des Datensatzes {#dataset-expiration}

Richten Sie die automatische Bereinigung von Datensätzen für kurzlebige Daten ein. Verwenden Sie die `/ttl` -Endpunkt der Data Hygiene-API verwenden, um Ablaufdaten für Datensätze zu planen, die basierend auf einem bestimmten Zeitpunkt oder Datum für die Bereinigung verwendet werden sollen. Weitere Informationen finden Sie im Handbuch zum Ablauf von Datensätzen . [Erstellen eines Datensatzablaufs](./api/dataset-expiration.md) und [akzeptierte Abfrageparameter](./api/dataset-expiration.md#query-params).

## Überwachen der Arbeitsreihenfolge und des Datensatzablaufstatus {#monitor}

Sie können den Fortschritt Ihrer Datenlebenszyklusverwaltung effizient überwachen, indem Sie **E/A-Ereignisse**. Ein I/O-Ereignis ist ein Mechanismus zum Empfang von Echtzeit-Benachrichtigungen über Änderungen oder Aktualisierungen in verschiedenen Diensten innerhalb von Platform.

E/A-Ereignis-Warnungen können an einen konfigurierten Webhook gesendet werden, um die Automatisierung der Aktivitätsüberwachung zu ermöglichen. Um Warnhinweise über Webhook zu erhalten, müssen Sie Ihren Webhook für Platform-Warnhinweise in der Adobe Developer Console registrieren. Siehe Handbuch unter [Abonnieren von Adobe I/O-Ereignisbenachrichtigungen](../observability/alerts/subscribe.md) für die detaillierten Anweisungen.

Verwenden Sie die folgenden Lebenszyklusmethoden und -richtlinien, um den Auftragsstatus effektiv abzurufen und zu überwachen:

### I/O-Ereignisse {#io-events}

Um den Fortschritt Ihrer Datenlebenszyklusaufgaben effizient zu überwachen, richten Sie I/O-Ereignisse ein und verwenden Sie sie, indem Sie die folgenden Schritte ausführen:

- Richten Sie Webhooks ein, um Push-Benachrichtigungen für Statusänderungen zu erhalten.
- Verwenden Sie Benachrichtigungen, um den Fortschritt zu überwachen und nach Abschluss Aktualisierungen zu erhalten.
- Vermeiden Sie die Implementierung von Abrufmechanismen zur Minimierung des API-Traffics.

### Abrufen detaillierter Antworten für eine einzelne Arbeitsreihenfolge {#retrieve-detailed-work-order-response}

Ausführliche Informationen zu einzelnen Arbeitsaufträgen erhalten Sie bei folgendem Ansatz:

- Stellen Sie eine GET-Anfrage an die `/workorder/{work_order_id}` Endpunkt für detaillierte Antwortdaten.
- Abrufen produktspezifischer Antworten und Erfolgsmeldungen.
- Vermeiden Sie die Verwendung dieser Methode für reguläre Abruftätigkeiten.

Durch Einhaltung dieser Best Practices können Sie im Rahmen des erweiterten Data Lifecycle Managements effektiv Bereinigungsanfragen verwalten und die Reaktionszeiten optimieren.
