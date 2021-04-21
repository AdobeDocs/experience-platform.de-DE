---
keywords: Experience Platform;Startseite;beliebte Themen;Überwachung;Überwachung;Datenflüsse;Überwachung der Erfassung;Datenaufnahme;Datenaufnahme;Ansicht;Ansichten-Stapel;
solution: Experience Platform
title: Überwachen der Dateneinbindung
topic-legacy: overview
description: Dieses Benutzerhandbuch enthält eine Anleitung zum Überwachen Ihrer Daten in der Benutzeroberfläche von Adobe Experience Platform. Für dieses Handbuch benötigen Sie eine Adobe ID und Zugriff auf Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 67%

---

# Überwachen der Datenaufnahme

Mit der Datenaufnahme können Sie Ihre Daten in Adobe Experience Platform aufnehmen. Sie können entweder die Stapelverarbeitung verwenden, mit der Sie Ihre Daten mit verschiedenen Dateitypen (z. B. CSVs) einfügen können, oder Streaming, mit dem Sie Ihre Daten mit Streaming-Endpunkten in Echtzeit auf [!DNL Platform] übertragen können.

Dieses Benutzerhandbuch enthält eine Anleitung zum Überwachen Ihrer Daten in der Benutzeroberfläche von Adobe Experience Platform. Für dieses Handbuch benötigen Sie eine Adobe ID und Zugriff auf Adobe Experience Platform.

## Überwachen der Datenaufnahme bei End-to-End-Streaming

Klicken Sie in der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) im linken Navigationsmenü auf **[!UICONTROL Überwachung]** und dann auf **[!UICONTROL End-to-End-Streaming]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

Die Überwachungsseite **[!UICONTROL End-to-End-Streaming]** wird angezeigt. Dieser Arbeitsbereich bietet ein Diagramm, das die Rate der Streaming-Ereignis anzeigt, die von [!DNL Platform] empfangen werden. Es zeigt die Rate der Streaming-Ereignis, die erfolgreich von [[!DNL Real-time Customer Profile]](../../profile/home.md) verarbeitet wurden, sowie eine detaillierte Liste der eingehenden Daten.

![](../images/quality/monitor-data-flows/list-streams.png)

Standardmäßig zeigt das obere Diagramm die Rate der Aufnahme in den letzten sieben Tagen an. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Das untere Diagramm zeigt die Rate der erfolgreich verarbeiteten Streaming-Ereignis von [!DNL Profile] in den letzten sieben Tagen. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

>[!NOTE]
>
>Damit Daten in diesem Diagramm angezeigt werden, müssen die Daten für **explizit** aktiviert sein. [!DNL Profile] Informationen zum Aktivieren von Streaming-Daten für [!DNL Profile] finden Sie im [Benutzerhandbuch für Datensätze](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Unter den Diagrammen befindet sich eine Liste aller Streaming-Erfassungsdatensätze, die dem oben angezeigten Datumsbereich entsprechen. Jeder aufgelistete Batch zeigt die ID, den Namen des Datensatzes, wann dieser zuletzt aktualisiert wurde, die Anzahl der Datensätze im Batch sowie die Anzahl der Fehler (sofern vorhanden) an. Sie können auf einen dieser Datensätze klicken, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Anzeigen von Streaming-Datensätzen

Beim Anzeigen der Details eines erfolgreich gestreamten Datensatzes werden Informationen wie die Anzahl der aufgenommenen Datensätze, die Dateigröße sowie die Beginn- und Endzeiten der Aufnahme angezeigt.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Die Details eines fehlgeschlagenen Streaming-Datensatzes zeigen dieselben Informationen wie ein erfolgreicher Datensatz.

![](../images/quality/monitor-data-flows/failed-batch.png)

Darüber hinaus geben fehlerhafte Datensätze Details zu den Fehlern an, die während der Verarbeitung des Batches aufgetreten sind. Im nachstehenden Beispiel ist ein Systemfehler beim Überprüfen der datasetId aus dem Katalog aufgetreten.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Überwachen der Batch-End-to-End-Datenaufnahme

Klicken Sie im linken Navigationsmenü unter [[!DNL Experience Platform UI]](https://platform.adobe.com) auf **[!UICONTROL Monitoring]**.

![](../images/quality/monitor-data-flows/click-monitoring.png)

Die Überwachungsseite **[!UICONTROL Batch End-to-End]** wird angezeigt und listet die zuvor aufgenommenen Batches auf. Sie können auf einen der Batches klicken, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/list-batches.png)

### Anzeigen von Batches

Beim Anzeigen der Details eines erfolgreichen Batches werden Informationen wie die Anzahl der aufgenommenen Datensätze, die Dateigröße sowie der Beginn- und Endzeitpunkt der Aufnahme angezeigt.

![](../images/quality/monitor-data-flows/successful-batch.png)

Die Details eines fehlgeschlagenen Batches zeigen dieselben Informationen wie ein erfolgreicher Batch an, mit dem Zusatz, wie viele Datensätze fehlgeschlagen sind.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Darüber hinaus werden bei fehlgeschlagenen Batches Details zu den Fehlern bereitgestellt, die bei der Verarbeitung des Batches aufgetreten sind. Im nachstehenden Beispiel ist ein Fehler mit dem aufgenommenen Batch aufgetreten, da er ein unbekanntes `_experience`-Feld verwendet hat.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)
