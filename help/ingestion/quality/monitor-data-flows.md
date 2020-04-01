---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Überwachen der Datenerfassung
topic: overview
translation-type: tm+mt
source-git-commit: 8577d9b93098d5d6ec778d549bf5fc1e29c32d86

---


# Überwachen der Datenerfassung

Mit der Datenerfassung können Sie Ihre Daten in Adobe Experience Platform erfassen. Sie können entweder die Stapelverarbeitung verwenden, mit der Sie Ihre Daten mit verschiedenen Dateitypen (z. B. CSVs) einfügen können, oder Streaming, mit dem Sie Ihre Daten mit Streaming-Endpunkten in Echtzeit an die Plattform übertragen können.

Dieses Benutzerhandbuch enthält eine Anleitung zum Überwachen Ihrer Daten in der Benutzeroberfläche von Adobe Experience Platform. Für dieses Handbuch benötigen Sie eine Adobe-ID und Zugriff auf die Adobe Experience Platform.

## Überwachen der End-to-End-Datenerfassung

Klicken Sie in der Benutzeroberfläche [der](https://platform.adobe.com)Experience Platform im linken Navigationsmenü auf **Überwachung** und dann auf **Streaming von Ende zu Ende**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Die Seite zur *Streaming-End-to-End* -Überwachung wird angezeigt. Dieser Arbeitsbereich bietet ein Diagramm, das die Rate der gesendeten Nachrichten sowie eine detaillierte Liste der eingehenden Daten anzeigt.

![](../images/quality/monitor-data-flows/list-streams.png)

Standardmäßig zeigt das Diagramm die Rate der Aufnahme in den letzten sieben Tagen an. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

![](../images/quality/monitor-data-flows/list-streams-focus-on-graph.png)

Unter dem Diagramm befindet sich eine Liste aller Streaming-Erfassungsdatensätze, die dem oben angezeigten Datumsbereich entsprechen. Jeder aufgelistete Stapel zeigt die ID, den Namen des Datensatzes, bei der letzten Aktualisierung die Anzahl der Datensätze im Stapel sowie die Anzahl der Fehler (sofern vorhanden) an. Sie können auf einen der Datensätze klicken, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Anzeigen von Streaming-Aufzeichnungen

Beim Anzeigen der Details eines erfolgreich gestreuten Datensatzes werden Informationen wie die Anzahl der erfassten Datensätze, die Dateigröße sowie der Beginn- und Endzeit der Erfassung angezeigt.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Die Details eines fehlgeschlagenen Streaming-Datensatzes zeigen dieselben Informationen wie ein erfolgreicher Datensatz.

![](../images/quality/monitor-data-flows/failed-batch.png)

Darüber hinaus geben fehlerhafte Datensätze Details zu den Fehlern an, die während der Verarbeitung des Stapels aufgetreten sind. Im Beispiel unten ist ein Systemfehler beim Überprüfen der datasetId aus dem Katalog aufgetreten.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Überwachen der Batch-End-Datenerfassung

Klicken Sie in der Benutzeroberfläche [der](https://platform.adobe.com)Experience Platform im linken Navigationsmenü auf **Überwachung** .

![](../images/quality/monitor-data-flows/click-monitoring.png)

Die Seite &quot; **Stapelüberwachung&quot;wird mit einer Liste der zuvor erfassten Stapel angezeigt** . Sie können auf einen der Stapel klicken, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/list-batches.png)

### Stapel anzeigen

Beim Anzeigen der Details eines erfolgreichen Stapels werden Informationen wie die Anzahl der erfassten Datensätze, die Dateigröße sowie der Beginn- und Endzeitpunkt der Erfassung angezeigt.

![](../images/quality/monitor-data-flows/successful-batch.png)

Die Details eines fehlgeschlagenen Stapels zeigen dieselben Informationen wie ein erfolgreicher Stapel an, wobei die Anzahl der Datensätze fehlgeschlagen ist.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Darüber hinaus werden bei fehlgeschlagenen Stapeln Details zu den Fehlern bereitgestellt, die bei der Verarbeitung des Stapels aufgetreten sind. Im Beispiel unten ist ein Fehler mit dem erfassten Stapel aufgetreten, da er ein unbekanntes Feld von verwendet `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)