---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Tutorials zur Datenerfassung
topic-legacy: tutorial
type: Tutorial
description: Datenerfassung beinhaltet die Batch-Erfassung, Streaming-Erfassung und Erfassung mithilfe von Quell-Connectoren.
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 40%

---

# Daten in [!DNL Experience Platform] einbeziehen

Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketern ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Die Adobe [!DNL Experience Platform Data Ingestion] stellt die verschiedenen Methoden dar, mit denen [!DNL Platform] Daten aus diesen Quellen erfasst und wie diese Daten im Data Lake zur Verwendung durch nachgelagerte [!DNL Platform services] beibehalten werden. [!DNL Data Ingestion] umfasst die Stapelverarbeitung, Streaming-Erfassung und -Erfassung mithilfe von Quell-Connectors. Weiterführende Informationen finden Sie in der [Datenerfassung – Übersicht](../ingestion/home.md) oder direkt in der [Quellendokumentation](../sources/home.md).

## Erstellen einer Quellverbindung in der Benutzeroberfläche und der API

Mithilfe von Source Connectors können Sie Daten aus mehreren Quellen erfassen und dann mit [!DNL Platform services] beschriftet, strukturiert und erweitert werden. Informationen zum Erstellen eines Quell-Connectors finden Sie unter [Quellübersicht](../sources/home.md).

## Batch-Daten erfassen

Mit Adobe Experience Platform können Sie Daten einfach als Stapeldateien in [!DNL Platform] importieren. Zu den zu erfassenden Daten zählen beispielsweise Profil-Daten aus einer einfachen Datei in einem CRM-System (z. B. eine Parquet-Datei) oder Daten, die einem bekannten [!DNL Experience Data Model] (XDM)-Schema in der Schema-Registrierung entsprechen. Konsultieren Sie zunächst das [Tutorial Datenerfassung in Platform](../ingestion/tutorials/ingest-batch-data.md).

## CSV-Datei einem XDM-Schema zuordnen

Um CSV-Daten in Adobe Experience Platform zu erfassen, müssen die Daten einem [!DNL Experience Data Model] (XDM)-Schema zugeordnet werden. Anweisungen zum Zuordnen einer CSV-Datei zu einem XDM-Schema mithilfe der [!DNL Experience Platform]-Benutzeroberfläche finden Sie unter [Zuordnen einer CSV-Datei zu einem XDM-Schema-Lernprogramm](../ingestion/tutorials/map-a-csv-file.md).

## Aufbauen einer Streaming-Verbindung

Um Streaming-Daten auf [!DNL Experience Platform] Beginn, müssen Sie zunächst einen HTTP-Endpunkt anfordern. Sie haben die Möglichkeit, diesen Endpunkt zu konfigurieren, um authentifiziertes Verhalten zu erzwingen. Dies kann über die [!DNL Platform]-Benutzeroberfläche oder [!DNL Experience Platform]-APIs erfolgen. Weiterführende Informationen finden Sie in den Tutorials zum [Erstellen einer Streaming-Verbindung mithilfe der Benutzeroberfläche](../ingestion/tutorials/create-streaming-connection-ui.md) oder [Erstellen einer Streaming-Verbindung mithilfe von APIs](../ingestion/tutorials/create-streaming-connection.md).

## Erstellen einer authentifizierten Streaming-Verbindung

Die authentifizierte Datenerfassung ermöglicht es Adobe Experience Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Identity], zwischen Datensätzen aus vertrauenswürdigen Quellen und nicht vertrauenswürdigen Quellen zu unterscheiden. Folgen Sie zunächst dem Tutorial zum [Erstellen einer authentifizierten Streaming-Verbindung](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Datensatz- und Zeitreihendaten streamen

Wenn ein Dataset und Dampfverbindungen vorhanden sind, können Sie Daten aus Datensatz- oder Zeitreihen in [!DNL Platform] streamen. Um mit dem Streaming von Datensatzdaten zu beginnen, folgen Sie dem Tutorial [Streamen von Datensatzdaten nach Platform](../ingestion/tutorials/streaming-record-data.md). Um mit dem Streaming von Zeitreihendaten zu beginnen, folgen Sie dem Tutorial [Streamen von Zeitreihendaten nach Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Mehrere Nachrichten in einer einzelnen HTTP-Anfrage streamen

Beim Streaming von Daten an Adobe Experience Platform kann das Ausführen zahlreicher HTTP-Aufrufe teuer werden. Anstatt beispielsweise 200 HTTP-Anfragen mit Payloads von 1 KB zu erstellen, ist es viel effizienter, 1 HTTP-Anfrage mit 200 Nachrichten mit jeweils 1 KB und einer Payload von 200 KB zu erstellen. Bei korrekter Verwendung ist die Gruppierung mehrerer Nachrichten in einer einzigen Anforderung eine hervorragende Möglichkeit, Daten zu optimieren, die an [!DNL Experience Platform] gesendet werden. Um zu erfahren, wie Sie mit der Streaming-Erfassung mehrere Nachrichten an [!DNL Experience Platform] innerhalb einer einzelnen HTTP-Anforderung senden, folgen Sie dem Tutorial [Senden mehrerer Nachrichten](../ingestion/tutorials/streaming-multiple-messages.md).
