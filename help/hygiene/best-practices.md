---
title: Best Practices für die erweiterte Verwaltung des Datenlebenszyklus
description: Erfahren Sie, wie Sie Datenhygiene-Anfragen in Adobe Experience Platform mithilfe der erweiterten Benutzeroberfläche für die Verwaltung von Datenlebenszyklen und der Datenhygiene-API effizient verwalten können. In diesem Handbuch werden Best Practices behandelt, wie die Maximierung von Identitäten pro Anfrage, die Angabe einzelner Datensätze und die Berücksichtigung von API-Drosselungen zur Vermeidung von Verzögerungen. Das Dokument enthält Richtlinien für die Einrichtung der automatischen Datensatzbereinigung, für die Überwachung des Arbeitsauftragsstatus und für detaillierte Methoden zum Abrufen von Antworten. Befolgen Sie diese Best Practices, um die Verarbeitung Ihrer Anfragen zu optimieren und die Antwortzeiten zu optimieren.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Best Practices für das erweiterte Data Lifecycle Management

Verwenden Sie die erweiterte Data Lifecycle Management-Benutzeroberfläche und die Data Hygiene API, um Bereinigungsanfragen effizient zu verwalten und Daten aus Adobe Experience Platform-Services zu entfernen. Befolgen Sie diese Best Practices, um die Verarbeitung Ihrer Anfragen zu optimieren und die Antwortzeiten zu optimieren.

## Voraussetzungen {#prerequisites}

Dieses Handbuch setzt ein Verständnis des Datenlebenszyklus-Arbeitsbereichs und der [Datenhygiene-API](./api/overview.md) voraus. Bevor Sie mit diesem Dokument fortfahren, machen Sie sich mit den Handbüchern [Erweitertes Daten-](./home.md)-Management“ und [Erstellen von Anfragen zum Löschen von Datensätzen](./ui/record-delete.md) oder [Datensatzgültigkeiten in der Benutzeroberfläche](./ui/dataset-expiration.md) oder über die API vertraut.

## Richtlinien zur Erstellung von Arbeitsaufträgen {#work-order-creation-guidelines}

Sie können den `/workorder`-Endpunkt in der Data Hygiene API verwenden, um Anfragen zum Löschen von Datensätzen in Experience Platform programmgesteuert zu verwalten. Mit diesem Endpunkt können Sie eine Löschanfrage erstellen, ihren Status überprüfen oder eine vorhandene Anfrage aktualisieren. Informationen zum Ausführen dieser Aktionen mithilfe [&#x200B; API finden &#x200B;](./api/workorder.md) im Dokument zum Arbeitsauftrags-Endpunkt .

>[!TIP]
>
>Ein Arbeitsauftrag ist eine strukturierte Anfrage, die bestimmte Datenverwaltungsvorgänge wie Datenbereinigung oder -umwandlung durchführt, um eine effiziente und systematische Verarbeitung zu gewährleisten.

Befolgen Sie die folgenden Richtlinien, um die Übermittlung Ihrer Bereinigungsanfrage zu optimieren:

1. **Maximieren von Identitäten pro Anfrage:** Schließen Sie bis zu 100.000 Identitäten pro Bereinigungsanfrage ein, um die Effizienz zu steigern. Wenn Sie mehrere Identitäten in einer einzigen Anfrage stapeln, reduzieren Sie die Häufigkeit von API-Aufrufen und minimieren das Risiko von Leistungsproblemen aufgrund von übermäßigen Single-Identity-Anfragen. Senden Sie Anfragen mit maximaler Identitätsanzahl, um eine schnellere Verarbeitung zu erzielen, da Arbeitsaufträge im Batch verarbeitet werden, um die Effizienz zu steigern.
2. **Spezifizieren einzelner Datensätze:** Geben Sie zur maximalen Effizienz den zu verarbeitenden einzelnen Datensatz an.
3. **Überlegungen zur API-Drosselung** Achten Sie auf API-Drosselungen, um Langsamkeiten zu verhindern. Kleinere Anfragen (&lt; 100 IDs) mit höherer Häufigkeit können zu 429 Antworten führen und erfordern eine erneute Einreichung mit akzeptablen Raten.

### 429-Fehler verwalten {#manage-429-errors}

Wenn Sie einen 429-Fehler erhalten, bedeutet dies, dass Sie die zulässige Anzahl von Anfragen innerhalb eines bestimmten Zeitraums überschritten haben. Befolgen Sie die folgenden Best Practices, um 429 Fehler effektiv zu verwalten:

- **Header „Wiederholen nach“ lesen**: Wenn ein 429-Fehler zurückgegeben wird, überprüfen Sie die Antwort-Header „Wiederholen nach“. Diese Kopfzeile gibt die Wartezeit an, bevor die Anfrage erneut versucht wird.
- **Wiederholungslogik implementieren**: Verwenden Sie den Wert „Wiederholen nach“, um Wiederholungslogik in Ihrer Anwendung zu implementieren und sicherzustellen, dass Wiederholungsversuche nach der angegebenen Zeit unternommen werden, um nachfolgende 429-Fehler zu vermeiden.
- **Batch Ihrer Anfragen**: Senden Sie nicht schnell hintereinander zahlreiche kleine Anfragen. Stattdessen sollten Sie mehrere Identitäten in einer einzigen Anfrage zusammenfassen, um die Anruffrequenz zu reduzieren und das Risiko zu minimieren, dass die Ratenbeschränkungen erreicht werden.

## Ablaufdatum des Datensatzes {#dataset-expiration}

Richten Sie die automatische Datensatzbereinigung für kurzlebige Daten ein. Verwenden Sie den `/ttl`-Endpunkt in der Datenhygiene-API, um Ablaufdaten für Datensätze zur Bereinigung basierend auf einer bestimmten Zeit oder einem bestimmten Datum zu planen. Informationen zum Erstellen einer Datensatzgültigkeit und [akzeptierten Abfrageparametern](./api/dataset-expiration.md) finden Sie [&#x200B; Handbuch zum Datensatzgültigkeits-Endpunkt &#x200B;](./api/dataset-expiration.md#query-params).

## Überwachen des Arbeitsauftrags und des Datensatzgültigkeitsstatus {#monitor}

Sie können den Fortschritt des Daten-Lifecycle-Managements effizient mithilfe von **I/O Events** überwachen. Ein I/O-Ereignis ist ein Mechanismus zum Empfang von Echtzeitbenachrichtigungen über Änderungen oder Aktualisierungen in verschiedenen Services in Experience Platform.

E/A-Ereignis-Warnhinweise können an einen konfigurierten Webhook gesendet werden, um die Automatisierung der Aktivitätsüberwachung zu ermöglichen. Um Warnhinweise über einen Webhook zu erhalten, müssen Sie Ihren Webhook für Experience Platform-Warnhinweise in Adobe Developer Console registrieren. Detaillierte Anweisungen finden Sie [&#x200B; Handbuch unter „Abonnieren von Adobe I/O](../observability/alerts/subscribe.md)Ereignisbenachrichtigungen“.

Verwenden Sie die folgenden Methoden und Richtlinien für den Datenlebenszyklus, um Auftragsstatus effektiv abzurufen und zu überwachen:

### I/O-Ereignisse {#io-events}

Um den Fortschritt Ihrer Datenlebenszyklusaufgaben effizient zu überwachen, richten Sie I/O-Ereignisse ein und verwenden Sie sie, indem Sie die folgenden Schritte ausführen:

- Webhooks für den Empfang von Push-Benachrichtigungen bei Statusänderungen einrichten.
- Verwenden Sie Benachrichtigungen, um den Fortschritt zu überwachen und nach Abschluss Aktualisierungen zu erhalten.
- Vermeiden Sie die Implementierung von Abrufmechanismen, um den API-Traffic zu minimieren.

### Abrufen detaillierter Antworten für einen einzelnen Arbeitsauftrag {#retrieve-detailed-work-order-response}

Detaillierte Informationen zu einzelnen Arbeitsaufträgen erhalten Sie nach folgendem Ansatz:

- Stellen Sie eine GET-Anfrage an den `/workorder/{work_order_id}`-Endpunkt, um detaillierte Antwortdaten zu erhalten.
- Rufen Sie produktspezifische Antworten und Erfolgsmeldungen ab.
- Vermeiden Sie diese Methode für regelmäßige Abrufaktionen.

Durch Befolgung dieser Best Practices können Sie Bereinigungsanfragen effektiv verwalten und die Antwortzeiten im erweiterten Data Lifecycle Management optimieren.
