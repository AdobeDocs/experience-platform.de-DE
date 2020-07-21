---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fehlerbehebung bei der Streaming-Erfassung
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 65%

---


# Handbuch zur Fehlerbehebung bei der Streaming-Erfassung

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zur Streaming-Erfassung in Adobe Experience Platform. For questions and troubleshooting related to other [!DNL Platform] services, including those that are encountered across all [!DNL Platform] APIs, please refer to the [Experience Platform troubleshooting guide](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] provides RESTful APIs that you can use to ingest data into [!DNL Experience Platform]. Die erfassten Daten dienen zur nahezu echtzeitbasierten Aktualisierung einzelner Kundenprofile, sodass Sie kanalübergreifend für personalisierte, relevante Erlebnisse sorgen können. Weiterführende Informationen zu dem Dienst und zu den verschiedenen Erfassungsmethoden finden Sie in der [Übersicht zur Datenerfassung](../home.md). Anweisungen zur Verwendung von Streaming-Erfassungs-APIs finden Sie in der [Übersicht zur Streaming-Erfassung](../streaming-ingestion/overview.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zur Streaming-Erfassung.

### Wie weiß ich, ob die Payload, die ich versenden möchte, richtig formatiert ist?

[!DNL Data Ingestion] nutzt [!DNL Experience Data Model] (XDM-)Schema zur Validierung des Formats eingehender Daten. Das Senden von Daten, die nicht mit der Struktur eines vordefinierten XDM-Schemas übereinstimmen, führt dazu, dass die Erfassung fehlschlägt. For more information on XDM and its use in [!DNL Experience Platform], see the [XDM System overview](../../xdm/home.md).

Die Streaming-Erfassung unterstützt zwei Validierungsmodi: synchron und asynchron. Bei jeder Validierungsmethode werden fehlerhafte Daten anders behandelt.

**Synchrone Validierung** sollte während der Entwicklung genutzt werden. Datensätze, bei denen die Validierung fehlschlägt, werden entfernt; außerdem wird eine Fehlermeldung mit Informationen dazu ausgegeben, warum sie fehlgeschlagen sind (z. B. „Ungültiges XDM-Nachrichtenformat“).

**Asynchrone Validierung** sollte in der Produktion verwendet werden. Any malformed data that does not pass validation is sent to the [!DNL Data Lake] as a failed batch file, where it can be retrieved later for further analysis.

Weiterführende Informationen zur synchronen und asynchronen Validierung finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md). Anweisungen zum Anzeigen von Batches, die die Validierung nicht bestehen, finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Can I validate a request payload before sending it to [!DNL Platform]?

Request payloads can only be evaluated after they have been sent to [!DNL Platform]. Bei Nutzung der synchronen Validierung geben gültige Payloads ausgefüllte JSON-Objekte zurück, während ungültige Payloads Fehlermeldungen zurückgeben. During asynchronous validation, the service detects and sends any malformed data to the [!DNL Data Lake] where it can later be retrieved for analysis. Weiterführende Informationen dazu finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md).

### Was geschieht, wenn eine synchrone Validierung an einem Edgeserver angefordert wird, der sie nicht unterstützt?

Wenn synchrone Validierung am angeforderten Ort nicht unterstützt wird, wird eine Fehlerantwort vom Typ 501 zurückgegeben. Weiterführende Informationen zur synchronen Validierung finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md).

### Wie stelle ich sicher, dass Daten nur aus vertrauenswürdigen Quellen erfasst werden?

[!DNL Experience Platform] unterstützt die sichere Datenerfassung. Wenn authentifizierte Datenerfassung aktiviert ist, müssen Clients ein JSON Web Token (JWT) und ihre IMS-Organisations-Kennung als Anfragekopfzeilen senden. For more information on how to send authenticated data to [!DNL Platform], please see the guide on [authenticated data collection](../tutorials/create-authenticated-streaming-connection.md).

### Wie lange dauert das Streaming von Daten [!DNL Real-time Customer Profile]?

Streamed events are generally reflected in [!DNL Real-time Customer Profile] in under 60 seconds. Reale Latenzwerte können aber je nach Datenvolumen, Nachrichtengröße und Bandbreiteneinschränkungen davon abweichen.

### Kann ich in eine API-Anfrage mehrere Nachrichten einschließen?

You can group multiple messages within a single request payload and stream them to [!DNL Platform]. Bei richtiger Verwendung stellt das Gruppieren mehrerer Nachrichten in einer Anfrage eine hervorragende Möglichkeit zur Optimierung Ihrer Datenvorgänge dar. Lesen Sie das Tutorial zum [Senden mehrerer Nachrichten in einer Anfrage](../tutorials/streaming-multiple-messages.md), um mehr zu erfahren.

### Wie weiß ich, ob meine gesendeten Daten empfangen werden?

All data that is sent to [!DNL Platform] (successfully or otherwise) is stored as batch files before being persisted in datasets. Der Verarbeitungsstatus von Batches erscheint in dem Datensatz, an den sie gesendet wurden.

Sie können überprüfen, ob Daten erfolgreich erfasst wurden, indem Sie die Datensatzaktivität mit der [Benutzeroberfläche von Experience Platform](https://platform.adobe.com) überprüfen. Klicken Sie dazu im linken Navigationsbereich auf **[!UICONTROL Datensätze]**, um eine Liste der Datensätze anzuzeigen. Wählen Sie in der angezeigten Liste den Datensatz aus, an den Sie streamen, um die zugehörige Seite *[!UICONTROL Datensatzaktivität]* zu öffnen und alle Batches anzuzeigen, die in einem bestimmten Zeitraum gesendet wurden. For more information about using [!DNL Experience Platform] to monitor data streams, see the guide on [monitoring streaming data flows](../quality/monitor-data-flows.md).

If your data failed to ingest and you want to recover it from [!DNL Platform], you can retrieve the failed batches by sending their IDs to the [!DNL Data Access API]. Weiterführende Informationen finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Warum sind meine Streaming-Daten im Data Lake nicht verfügbar?

There are a variety of reasons why batch ingestion may fail to reach the [!DNL Data Lake], such as invalid formatting, missing data, or system errors. To determine why your batch failed, you must retrieve the batch using the [!DNL Data Ingestion Service API] and view its details. Ausführliche Anweisungen zum Abrufen eines fehlgeschlagenen Batches finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Wie analysiere ich die Antwort, die für die API-Anfrage zurückgegeben wurde?

Prüfen Sie zunächst den Antwort-Code des Servers, um zu ermitteln, ob Ihre Anfrage akzeptiert wurde. Wenn ein erfolgreicher Antwort-Code zurückgegeben wurde, können Sie als Nächstes das Array-Objekt `responses` prüfen, um den Status der Erfassungsaufgabe zu ermitteln.

Eine erfolgreiche API-Anfrage mit einer Nachricht gibt den Status-Code 200 zurück. Eine erfolgreiche (oder teilweise erfolgreiche) API-Anfrage mit Batch-Nachricht gibt den Status-Code 207 zurück.

Die folgende JSON ist ein Beispielantwortobjekt für eine API-Anfrage mit zwei Nachrichten: einer erfolgreichen und einer fehlgeschlagenen. Nachrichten, die erfolgreich gestreamt werden, geben eine `xactionId`-Eigenschaft zurück. Nachrichten, die nicht gestreamt werden, geben eine `statusCode`-Eigenschaft und eine Antwort-`message` mit zusätzlichen Informationen zurück.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Warum werden meine gesendeten Nachrichten nicht bei uns empfangen [!DNL Real-time Customer Profile]?

If [!DNL Real-time Customer Profile] rejects a message, it is most likely due to incorrect identity information. Der Grund dafür kann sein, dass für eine Identität ein ungültiger Wert oder Namespace angegeben wurde.

Es gibt zwei Arten von Identitäts-Namespaces: standardmäßige und benutzerdefinierte. When using custom namespaces, make sure the namespace has been registered within [!DNL Identity Service]. Weiterführende Informationen zur Verwendung von standardmäßigen und benutzerdefinierten Namespaces finden Sie in der [Übersicht zu Identitäts-Namespaces](../../identity-service/namespaces.md).

You can use the [!DNL Experience Platform UI](https://platform.adobe.com) to see more information on why a message failed ingestion. Klicken Sie im linken Navigationsbereich auf **[!UICONTROL Monitoring]** und dann auf den Tab _[!UICONTROL Streaming End-to-End]_, um die in einem bestimmten Zeitraum gestreamten Nachrichten-Batches anzuzeigen.