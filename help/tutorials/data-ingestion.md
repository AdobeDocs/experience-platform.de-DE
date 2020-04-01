---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Lernprogramme zur Datenüberlastung
topic: tutorial
translation-type: tm+mt
source-git-commit: eef56cfc20eb8e4ac131bee20c5c3afbf82971d2

---


# Daten in die Experience Platform integrieren

Die Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketingexperten ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen Plattform Daten aus diesen Quellen zusammenfasst, sowie die Art und Weise, wie diese Daten im Data Lake für die Verwendung durch nachgelagerte Plattformdienste beibehalten werden. Die Dateningestion umfasst die Stapelverarbeitung, Streaming-Erfassung und Erfassung mithilfe von Quellschnittstellen. Weitere Informationen finden Sie in der Übersicht über die [Dateneinbettung](../ingestion/home.md) und in der Übersicht über die [Quellen](../source-connectors/home.md).

## Stapeldaten aufnehmen

Mit Adobe Experience Platform können Sie Daten ganz einfach als Batch-Dateien in die Plattform importieren. Zu den zu erfassenden Daten zählen beispielsweise Profil-Daten aus einer reduzierten Datei in einem CRM-System (z. B. eine Parkettdatei) oder Daten, die einem bekannten XDM-Schema (Experience Data Model) in der Schema-Registrierung entsprechen. Besuchen Sie zunächst die [Erfassungsdaten im Plattform-Tutorial](../ingestion/tutorials/ingest-batch-data.md).

## Zuordnen einer CSV-Datei zu einem XDM-Schema

Um CSV-Daten in Adobe Experience Platform zu erfassen, müssen die Daten einem XDM-Schema (Experience Data Model) zugeordnet werden. Anweisungen zum Zuordnen einer CSV-Datei zu einem XDM-Schema mithilfe der Experience Platform-Benutzeroberfläche finden Sie in der [Zuordnung einer CSV-Datei zu einem XDM-Schema-Lernprogramm](../ingestion/tutorials/map-a-csv-file.md).

## Erstellen einer Streaming-Verbindung

Um Streaming-Daten an Experience Platform Beginn, müssen Sie zunächst eine Streaming-HTTP-Verbindung erstellen. Beim Erstellen einer Streaming-Verbindung müssen Sie wichtige Details wie die Quelle der Streaming-Daten angeben und angeben, ob Daten von einer vertrauenswürdigen (authentifizierten) oder einer nicht vertrauenswürdigen (nicht authentifizierten) Quelle gesendet werden sollen. Dies kann über die Plattform- oder Experience Platform-APIs erfolgen. Weitere Informationen finden Sie in den Übungen zum [Erstellen einer Streaming-Verbindung mit der Benutzeroberfläche](../ingestion/tutorials/create-streaming-connection-ui.md) oder zum [Erstellen einer Streaming-Verbindung mit APIs](../ingestion/tutorials/create-streaming-connection.md).

## Authentifizierte Streaming-Verbindung erstellen

Die authentifizierte Datenerfassung ermöglicht es Adobe Experience Platform-Diensten wie dem Echtzeit-Profil von Kunden und Identitäten, zwischen Datensätzen aus vertrauenswürdigen Quellen und nicht vertrauenswürdigen Quellen zu unterscheiden. Beginnen Sie mit dem Lernprogramm zum [Erstellen einer authentifizierten Streaming-Verbindung](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Stream-Datensatz- und Zeitreihendaten

Mit einem Dataset und einer Streaming-Verbindung können Sie Daten aus Datensatz- oder Zeitreihen in Plattform streamen. Um mit dem Streaming von Datensatzdaten zu beginnen, folgen Sie den [Stream-Datensatzdaten in das Plattform-Lernprogramm](../ingestion/tutorials/streaming-record-data.md). Um mit dem Streaming von Zeitreihendaten zu beginnen, folgen Sie den Daten der [Stream-Zeitreihen in Plattform](../ingestion/tutorials/streaming-time-series-data.md).

## Streamen mehrerer Nachrichten in einer einzelnen HTTP-Anforderung

Beim Streaming von Daten an Adobe Experience Platform können zahlreiche HTTP-Aufrufe teuer sein. Anstatt beispielsweise 200 HTTP-Anforderungen mit 1 KB Nutzlasten zu erstellen, ist es viel effizienter, 1 HTTP-Anforderung mit 200 Nachrichten mit jeweils 1 KB und einer Nutzlast von 200 KB zu erstellen. Bei korrekter Verwendung ist die Gruppierung mehrerer Nachrichten in einer einzigen Anforderung eine hervorragende Möglichkeit, Daten zu optimieren, die an Experience Platform gesendet werden. Um zu erfahren, wie mehrere Nachrichten über eine einzelne HTTP-Anforderung an Experience Platform mit Streaming gesendet werden, befolgen Sie das Lernprogramm zum [Senden mehrerer Nachrichten](../ingestion/tutorials/streaming-multiple-messages.md).

## Erstellen eines Quell-Connectors in der Benutzeroberfläche und der API

Mithilfe von Source Connectors können Sie Daten aus mehreren Quellen erfassen und dann mit Plattformdiensten beschriftet, strukturiert und erweitert werden. Um mit der Erstellung eines Connectors über die Benutzeroberfläche zu beginnen, besuchen Sie bitte die Seite zum [Erstellen eines Quell-Connectors in der UI-Übersicht](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md). Um Quellschnittstellen mithilfe der API zu erstellen, [erstellen Sie mithilfe der Übersicht](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)zur Flussdienst-API einen Quellanschluss.

