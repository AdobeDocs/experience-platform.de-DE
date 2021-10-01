---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming; Streaming-Erfassung; Fehlerbehebung; Fehlerbehebung bei Streaming-Erfassung; Fehlerbehebung bei Streaming-Erfassung; FAQ bei Streaming-Erfassung; FAQ;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei der Streaming-Erfassung
topic-legacy: troubleshooting
description: In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zur Streaming-Erfassung in Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 64%

---

# Handbuch zur Fehlerbehebung bei der Streaming-Erfassung

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zur Streaming-Erfassung in Adobe Experience Platform. Fragen und Antworten zur Fehlerbehebung bei anderen [!DNL Platform]-Diensten, einschließlich solcher, die für alle [!DNL Platform]-APIs verfügbar sind, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platformen](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] stellt RESTful-APIs bereit, mit denen Sie Daten in [!DNL Experience Platform] erfassen können. Die erfassten Daten dienen zur nahezu echtzeitbasierten Aktualisierung einzelner Kundenprofile, sodass Sie kanalübergreifend für personalisierte, relevante Erlebnisse sorgen können. Weiterführende Informationen zu dem Dienst und zu den verschiedenen Erfassungsmethoden finden Sie in der [Datenerfassung – Übersicht](../home.md). Anweisungen zur Verwendung von Streaming-Erfassungs-APIs finden Sie in der [Streaming-Erfassung – Übersicht](../streaming-ingestion/overview.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zur Streaming-Erfassung.

### Wie weiß ich, ob die Payload, die ich versenden möchte, richtig formatiert ist?

[!DNL Data Ingestion] nutzt ( [!DNL Experience Data Model] XDM)-Schemas zur Validierung des Formats eingehender Daten. Das Senden von Daten, die nicht mit der Struktur eines vordefinierten XDM-Schemas übereinstimmen, führt dazu, dass die Erfassung fehlschlägt. Weitere Informationen zu XDM und seiner Verwendung in [!DNL Experience Platform] finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

Die Streaming-Erfassung unterstützt zwei Validierungsmodi: synchron und asynchron. Bei jeder Validierungsmethode werden fehlerhafte Daten anders behandelt.

**Synchrone Validierung** sollte während der Entwicklung genutzt werden. Datensätze, bei denen die Validierung fehlschlägt, werden entfernt; außerdem wird eine Fehlermeldung mit Informationen dazu ausgegeben, warum sie fehlgeschlagen sind (z. B. „Ungültiges XDM-Nachrichtenformat“).

**Asynchrone Validierung** sollte in der Produktion verwendet werden. Falsch formatierte Daten, die die Validierung nicht bestehen, werden als fehlgeschlagene Batch-Datei an [!DNL Data Lake] gesendet, wo sie später zur weiteren Analyse abgerufen werden können.

Weiterführende Informationen zur synchronen und asynchronen Validierung finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md). Anweisungen zum Anzeigen von Batches, die die Validierung nicht bestehen, finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Kann ich eine Anfrage-Payload validieren, bevor ich sie an [!DNL Platform] schicke?

Anfrage-Payloads können erst ausgewertet werden, nachdem sie an [!DNL Platform] gesendet wurden. Bei Nutzung der synchronen Validierung geben gültige Payloads ausgefüllte JSON-Objekte zurück, während ungültige Payloads Fehlermeldungen zurückgeben. Während der asynchronen Validierung erkennt und sendet der Dienst fehlerhafte Daten an [!DNL Data Lake], wo sie später zur Analyse abgerufen werden können. Weiterführende Informationen dazu finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md).

### Was geschieht, wenn eine synchrone Validierung an einem Edgeserver angefordert wird, der sie nicht unterstützt?

Wenn synchrone Validierung am angeforderten Ort nicht unterstützt wird, wird eine Fehlerantwort vom Typ 501 zurückgegeben. Weiterführende Informationen zur synchronen Validierung finden Sie in der [Übersicht zur Streaming-Validierung](../quality/streaming-validation.md).

### Wie stelle ich sicher, dass Daten nur aus vertrauenswürdigen Quellen erfasst werden?

[!DNL Experience Platform] unterstützt die sichere Datenerfassung. Wenn authentifizierte Datenerfassung aktiviert ist, müssen Clients ein JSON Web Token (JWT) und ihre IMS-Organisations-Kennung als Anfragekopfzeilen senden. Weitere Informationen zum Senden authentifizierter Daten an [!DNL Platform] finden Sie im Handbuch zu [authentifizierter Datenerfassung](../tutorials/create-authenticated-streaming-connection.md).

### Wie hoch ist die Latenz für Streaming-Daten auf [!DNL Real-time Customer Profile]?

Streaming-Ereignisse werden im Allgemeinen in [!DNL Real-time Customer Profile] in weniger als 60 Sekunden angezeigt. Reale Latenzwerte können aber je nach Datenvolumen, Nachrichtengröße und Bandbreiteneinschränkungen davon abweichen.

### Kann ich in eine API-Anfrage mehrere Nachrichten einschließen?

Sie können mehrere Nachrichten in einer einzelnen Anfrage-Payload gruppieren und an [!DNL Platform] streamen. Bei richtiger Verwendung stellt das Gruppieren mehrerer Nachrichten in einer Anfrage eine hervorragende Möglichkeit zur Optimierung Ihrer Datenvorgänge dar. Lesen Sie das Tutorial zum [Senden mehrerer Nachrichten in einer Anfrage](../tutorials/streaming-multiple-messages.md), um mehr zu erfahren.

### Wie weiß ich, ob meine gesendeten Daten empfangen werden?

Alle Daten, die (erfolgreich oder anderweitig) an [!DNL Platform] gesendet werden, werden als Batch-Dateien gespeichert, bevor sie in Datensätzen persistiert werden. Der Verarbeitungsstatus von Batches erscheint in dem Datensatz, an den sie gesendet wurden.

Sie können überprüfen, ob Daten erfolgreich erfasst wurden, indem Sie die Datensatzaktivität mit der [Benutzeroberfläche von Experience Platform](https://platform.adobe.com) überprüfen. Klicken Sie dazu im linken Navigationsbereich auf **[!UICONTROL Datensätze]**, um eine Liste der Datensätze anzuzeigen. Wählen Sie in der angezeigten Liste den Datensatz aus, an den Sie streamen, um die zugehörige Seite **[!UICONTROL Datensatzaktivität]** zu öffnen und alle Batches anzuzeigen, die in einem bestimmten Zeitraum gesendet wurden. Weitere Informationen zur Verwendung von [!DNL Experience Platform] zur Überwachung von Datenströmen finden Sie im Handbuch zum [Überwachen von Streaming-Datenflüssen](../quality/monitor-data-ingestion.md).

Wenn Ihre Daten nicht erfasst werden konnten und Sie sie von [!DNL Platform] wiederherstellen möchten, können Sie die fehlgeschlagenen Batches abrufen, indem Sie ihre IDs an [!DNL Data Access API] senden. Weiterführende Informationen finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Warum sind meine Streaming-Daten im Data Lake nicht verfügbar?

Es gibt verschiedene Gründe, warum die Batch-Erfassung die [!DNL Data Lake]-Variable möglicherweise nicht erreicht, z. B. ungültige Formatierung, fehlende Daten oder Systemfehler. Um festzustellen, warum Ihr Batch fehlgeschlagen ist, müssen Sie den Batch mit [!DNL Data Ingestion Service API] abrufen und seine Details anzeigen. Ausführliche Anweisungen zum Abrufen eines fehlgeschlagenen Batches finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

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

### Warum werden meine gesendeten Nachrichten nicht von [!DNL Real-time Customer Profile] empfangen?

Wenn [!DNL Real-time Customer Profile] eine Nachricht ablehnt, ist dies höchstwahrscheinlich auf falsche Identitätsinformationen zurückzuführen. Der Grund dafür kann sein, dass für eine Identität ein ungültiger Wert oder Namespace angegeben wurde.

Es gibt zwei Arten von Identitäts-Namespaces: standardmäßige und benutzerdefinierte. Wenn Sie benutzerdefinierte Namespaces verwenden, stellen Sie sicher, dass der Namespace in [!DNL Identity Service] registriert wurde. Weiterführende Informationen zur Verwendung von standardmäßigen und benutzerdefinierten Namespaces finden Sie in der [Übersicht zu Identitäts-Namespaces](../../identity-service/namespaces.md).

Sie können [[!DNL Experience Platform UI]](https://platform.adobe.com) verwenden, um weitere Informationen dazu anzuzeigen, warum eine Nachricht bei der Erfassung fehlgeschlagen ist. Klicken Sie im linken Navigationsbereich auf **[!UICONTROL Monitoring]** und dann auf den Tab **[!UICONTROL Streaming End-to-End]**, um die in einem bestimmten Zeitraum gestreamten Nachrichten-Batches anzuzeigen.
