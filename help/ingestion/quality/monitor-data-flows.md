---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Überwachen der Datenerfassung
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Überwachen der Datenerfassung

Durch die Datenerfassung können Sie Ihre Daten in Adobe Experience Platform erfassen. Sie können entweder die Stapelverarbeitung verwenden, mit der Sie Ihre Daten mit verschiedenen Dateitypen (z. B. CSVs) einfügen können, oder Streaming, mit dem Sie Ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit an die Platform erfassen können.

In diesem Benutzerhandbuch wird beschrieben, wie Sie Ihre Daten in der Benutzeroberfläche der Adobe Experience Platform überwachen. Für dieses Handbuch benötigen Sie eine Adobe ID und Zugriff auf die Adobe Experience Platform.

## Überwachen der End-to-End-Datenerfassung

Klicken Sie in der Benutzeroberfläche [der](https://platform.adobe.com)Experience Platform im linken Navigationsmenü auf **Überwachung** und dann auf **Streaming von Ende zu Ende**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Die Seite zur *Streaming-End-to-End* -Überwachung wird angezeigt. Dieser Arbeitsbereich bietet ein Diagramm, das die Rate der Streaming-Ereignis anzeigt, die bei der Platform empfangen werden. Es zeigt die Rate der Streaming-Ereignis an, die erfolgreich vom [Echtzeit-Kundendienst](../../profile/home.md)verarbeitet wurden, sowie eine detaillierte Liste der eingehenden Daten.

![](../images/quality/monitor-data-flows/list-streams.png)

Standardmäßig zeigt das obere Diagramm die Rate der Aufnahme in den letzten sieben Tagen an. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Das untere Diagramm zeigt die Rate der erfolgreich verarbeiteten Streaming-Ereignis nach Profil in den letzten sieben Tagen. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

>[!NOTE]
>
>Damit Daten in diesem Diagramm angezeigt werden, müssen sie zum Profil **explizit** aktiviert werden. Informationen zum Aktivieren von Streaming-Daten für Profil finden Sie im Benutzerhandbuch zu [Datensätzen](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Unter den Diagrammen befindet sich eine Liste aller Streaming-Erfassungsdatensätze, die dem oben angezeigten Datumsbereich entsprechen. Jeder aufgelistete Stapel zeigt die ID, den Namen des Datensatzes, bei der letzten Aktualisierung die Anzahl der Datensätze im Stapel sowie die Anzahl der Fehler (sofern vorhanden) an. Sie können auf einen der Datensätze klicken, um detaillierte Informationen zu diesem Datensatz zu erhalten.

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