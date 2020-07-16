---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutorials zur Datenerfassung
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 40%

---


# Ingest data into [!DNL Experience Platform]

Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketern ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe [!DNL Experience Platform Data Ingestion] represents the multiple methods by which [!DNL Platform] ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream [!DNL Platform services]. [!DNL Data Ingestion] umfasst die Stapelverarbeitung, Streaming-Erfassung und -Erfassung mithilfe von Quell-Connectors. Weiterführende Informationen finden Sie in der [Übersicht zur Datenerfassung](../ingestion/home.md) oder direkt in der [Quellendokumentation](../sources/home.md).

## Quell-Connector in der Benutzeroberfläche und der API erstellen

Source connectors allow you to ingest data from multiple sources, where it can then be labeled, structured, and enhanced using [!DNL Platform services]. Informationen zum Erstellen eines Quell-Connectors finden Sie in der [Quellenübersicht](../sources/home.md).

## Batch-Daten erfassen

Adobe Experience Platform allows you to easily import data into [!DNL Platform] as batch files. Examples of data to be ingested may include profile data from a flat file in a CRM system (such as a parquet file) or data that conforms to a known [!DNL Experience Data Model] (XDM) schema in the Schema Registry. Konsultieren Sie zunächst das Tutorial [Datenerfassung in Platform](../ingestion/tutorials/ingest-batch-data.md).

## CSV-Datei einem XDM-Schema zuordnen

In order to ingest CSV data into Adobe Experience Platform, the data must be mapped to an [!DNL Experience Data Model] (XDM) schema. For steps showing how to map a CSV file to an XDM schema using the [!DNL Experience Platform] user interface, follow the [map a CSV file to an XDM schema tutorial](../ingestion/tutorials/map-a-csv-file.md).

## Streaming-Verbindung erstellen

Um Streaming-Daten an [!DNL Experience Platform]Beginn, müssen Sie zunächst einen HTTP-Endpunkt anfordern. Sie haben die Möglichkeit, diesen Endpunkt zu konfigurieren, um authentifiziertes Verhalten zu erzwingen. This can be done using the [!DNL Platform] user interface or [!DNL Experience Platform] APIs. Weiterführende Informationen finden Sie in den Tutorials zum [Erstellen einer Streaming-Verbindung mithilfe der Benutzeroberfläche](../ingestion/tutorials/create-streaming-connection-ui.md) oder [Erstellen einer Streaming-Verbindung mithilfe von APIs](../ingestion/tutorials/create-streaming-connection.md).

## Authentifizierte Streaming-Verbindung erstellen

Authenticated Data Collection allows Adobe Experience Platform services, such as [!DNL Real-time Customer Profile] and [!DNL Identity], to differentiate between records coming from trusted sources and untrusted sources. Folgen Sie zunächst dem Tutorial zum [Erstellen einer authentifizierten Streaming-Verbindung](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Datensatz- und Zeitreihendaten streamen

With a dataset and steaming connections in place, you can stream record or time series data into [!DNL Platform]. Um mit dem Streaming von Datensatzdaten zu beginnen, folgen Sie dem Tutorial [Streamen von Datensatzdaten nach Platform](../ingestion/tutorials/streaming-record-data.md). Um mit dem Streaming von Zeitreihendaten zu beginnen, folgen Sie dem Tutorial [Streamen von Zeitreihendaten nach Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Mehrere Nachrichten in einer einzelnen HTTP-Anfrage streamen

Beim Streaming von Daten an Adobe Experience Platform kann das Ausführen zahlreicher HTTP-Aufrufe teuer werden. Anstatt beispielsweise 200 HTTP-Anfragen mit 1-KB-Payloads zu erstellen, ist es deutlich effizienter, eine HTTP-Anfrage mit 200 jeweils 1 KB großen Nachrichten und einer einzelnen Payload von 200 KB anzulegen. When used correctly, grouping multiple messages within a single request is an excellent way to optimize data being sent to [!DNL Experience Platform]. To learn how to send multiple messages to [!DNL Experience Platform] within a single HTTP request using streaming ingestion, follow the [sending multiple messages tutorial](../ingestion/tutorials/streaming-multiple-messages.md).



