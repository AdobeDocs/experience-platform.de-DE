---
keywords: Experience Platform;Startseite;beliebte Themen;Überwachung;Überwachung;Datenflüsse;Überwachung der Erfassung;Datenaufnahme;Datenaufnahme;Ansicht;Ansichten-Stapel;
solution: Experience Platform
title: Überwachen der Dateneinbindung
topic-legacy: overview
description: Dieses Benutzerhandbuch enthält eine Anleitung zum Überwachen Ihrer Daten in der Benutzeroberfläche von Adobe Experience Platform. Für dieses Handbuch benötigen Sie eine Adobe ID und Zugriff auf Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
translation-type: tm+mt
source-git-commit: 6bedd5ec0865e858a337155deb80309a54e30892
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 38%

---

# Überwachen der Datenaufnahme

Mit der Datenaufnahme können Sie Ihre Daten in Adobe Experience Platform aufnehmen. Sie können entweder die Stapelverarbeitung verwenden, mit der Sie Ihre Daten mit verschiedenen Dateitypen (z. B. CSVs) einfügen können, oder Streaming, mit dem Sie Ihre Daten mit Streaming-Endpunkten in Echtzeit auf [!DNL Platform] übertragen können.

In diesem Benutzerhandbuch werden Schritte zur Überwachung Ihrer Daten in der Adobe Experience Platform-Benutzeroberfläche beschrieben. Für dieses Handbuch benötigen Sie eine Adobe ID und Zugriff auf Adobe Experience Platform.

## Überwachen der Datenaufnahme bei End-to-End-Streaming

Wählen Sie in der Benutzeroberfläche [Experience Platform](https://platform.adobe.com) im linken Navigationsmenü **[!UICONTROL Überwachung]** und anschließend **[!UICONTROL Streaming von Ende zu Ende]**.

Die Überwachungsseite **[!UICONTROL End-to-End-Streaming]** wird angezeigt. Dieser Arbeitsbereich bietet ein Diagramm, das die Rate der Streaming-Ereignis anzeigt, die von [!DNL Platform] empfangen werden. Es zeigt die Rate der Streaming-Ereignis, die erfolgreich von [[!DNL Real-time Customer Profile]](../../profile/home.md) verarbeitet wurden, sowie eine detaillierte Liste der eingehenden Daten.

![](../images/quality/monitor-data-flows/list-streams.png)

Standardmäßig zeigt das obere Diagramm die Rate der Aufnahme in den letzten sieben Tagen an. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

![](../images/quality/monitor-data-flows/events-received.png)

Das untere Diagramm zeigt die Rate der erfolgreich verarbeiteten Streaming-Ereignis von [!DNL Profile] in den letzten sieben Tagen. Dieser Datumsbereich kann angepasst werden, um verschiedene Zeiträume anzuzeigen, indem Sie auf die hervorgehobene Schaltfläche klicken.

>[!NOTE]
>
>Damit Daten in diesem Diagramm angezeigt werden, müssen die Daten für **explizit** aktiviert sein. [!DNL Profile] Informationen zum Aktivieren von Streaming-Daten für [!DNL Profile] finden Sie im [Benutzerhandbuch für Datensätze](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Unter den Diagrammen befindet sich eine Liste aller Streaming-Erfassungsdatensätze, die dem oben angezeigten Datumsbereich entsprechen. Jeder aufgelistete Batch zeigt die ID, den Namen des Datensatzes, wann dieser zuletzt aktualisiert wurde, die Anzahl der Datensätze im Batch sowie die Anzahl der Fehler (sofern vorhanden) an. Sie können einen der Datensätze auswählen, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/streams.png)

### Anzeigen von Streaming-Datensätzen

Beim Anzeigen der Details eines erfolgreich gestreamten Datensatzes werden Informationen wie die Anzahl der aufgenommenen Datensätze, die Dateigröße sowie die Beginn- und Endzeiten der Aufnahme angezeigt.

![](../images/quality/monitor-data-flows/successful-streaming.png)

Die Details eines fehlgeschlagenen Streaming-Datensatzes zeigen dieselben Informationen wie ein erfolgreicher Datensatz.

![](../images/quality/monitor-data-flows/failed-batch.png)

Darüber hinaus geben fehlerhafte Datensätze Details zu den Fehlern an, die bei der Verarbeitung des Stapels aufgetreten sind. Im Beispiel unten ist ein Parsing-Fehler aufgetreten, der beim Konvertieren oder Validieren der Daten auftrat.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Überwachen der Batch-End-to-End-Datenaufnahme

Wählen Sie im linken Navigationsmenü [[!DNL Experience Platform UI]](https://platform.adobe.com) **[!UICONTROL Monitoring]**.

Die Überwachungsseite **[!UICONTROL Batch End-to-End]** wird angezeigt und listet die zuvor aufgenommenen Batches auf. Sie können einen der Stapel auswählen, um detaillierte Informationen zu diesem Datensatz zu erhalten.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Anzeigen von Batches

Beim Anzeigen der Details eines erfolgreichen Batches werden Informationen wie die Anzahl der aufgenommenen Datensätze, die Dateigröße sowie der Beginn- und Endzeitpunkt der Aufnahme angezeigt.

![](../images/quality/monitor-data-flows/successful-batch.png)

Die Details eines fehlgeschlagenen Batches zeigen dieselben Informationen wie ein erfolgreicher Batch an, mit dem Zusatz, wie viele Datensätze fehlgeschlagen sind.

![](../images/quality/monitor-data-flows/failed-batch.png)

Darüber hinaus liefern fehlgeschlagene Stapel Details zu den Fehlern, die bei der Verarbeitung des Stapels aufgetreten sind. Im Beispiel unten ist ein Fehler beim erfassten Stapel aufgetreten, da er die maximale Anzahl von Identitäten für die Person aufweist.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
