---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fehlerbehebung bei der Streaming-Erfassung
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Handbuch zur Fehlerbehebung bei der Streaming-Erfassung

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zum Streaming in Adobe Experience Platform. Fragen und Fehlerbehebung zu anderen Plattformdiensten, einschließlich solcher, die in allen Plattform-APIs auftreten, finden Sie im Handbuch zur Fehlerbehebung für [Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform Data Ingestion stellt REST-fähige APIs bereit, mit denen Sie Daten in Experience Platform erfassen können. Die erfassten Daten werden verwendet, um individuelle Kundenerlebnisse in Echtzeit zu aktualisieren, sodass Sie personalisierte, relevante Profil über mehrere Kanal hinweg bereitstellen können. Weitere Informationen zum Dienst und zu den verschiedenen Erfassungsmethoden finden Sie in der Übersicht über die [Dateneinbettung](../home.md) . Anweisungen zur Verwendung von Streaming-Inhalten-APIs finden Sie in der [Streaming-Erfassungsübersicht](../streaming-ingestion/overview.md).

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zur Streaming-Erfassung.

### Woher weiß ich, dass die Nutzlast, die ich verschicke, korrekt formatiert ist?

Data Ingestion nutzt Experience Data Model-(XDM-)Schema zur Validierung des Formats eingehender Daten. Das Senden von Daten, die nicht der Struktur eines vordefinierten XDM-Schemas entsprechen, führt zu einem Fehler bei der Erfassung. Weitere Informationen zu XDM und seiner Verwendung in Experience Platform finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

Die Streaming-Erfassung unterstützt zwei Überprüfungsmodi: synchron und asynchron. Bei jeder Überprüfungsmethode werden fehlerhafte Daten unterschiedlich behandelt.

**Während des Entwicklungsprozesses sollte eine synchrone Validierung** verwendet werden. Datensätze, bei denen die Überprüfung fehlschlägt, werden entfernt und eine Fehlermeldung ausgegeben, warum sie fehlgeschlagen sind (z. B.: &quot;Ungültiges XDM-Nachrichtenformat&quot;).

**Bei der Produktion sollte eine asynchrone Validierung** verwendet werden. Fehlerhafte Daten, die keine Validierung weitergeben, werden als Batchdatei an den Data Lake gesendet, wo sie später zur weiteren Analyse abgerufen werden können.

Weitere Informationen zur synchronen und asynchronen Validierung finden Sie in der Übersicht zur [Streaming-Validierung](../quality/streaming-validation.md). Anweisungen zur Ansicht von Stapeln mit Fehler bei der Überprüfung finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md).

### Kann ich eine Anfrage-Nutzlast überprüfen, bevor ich sie an die Plattform schicke?

Nutzdatenanforderungen können nur ausgewertet werden, nachdem sie an die Plattform gesendet wurden. Bei der Durchführung der synchronen Überprüfung geben gültige Nutzdaten ausgefüllte JSON-Objekte zurück, während ungültige Nutzdaten Fehlermeldungen zurückgeben. Während der asynchronen Validierung erkennt und sendet der Dienst fehlerhafte Daten an den Data Lake, wo sie später zur Analyse abgerufen werden können. See the [streaming validation overview](../quality/streaming-validation.md) for more information.

### Was passiert, wenn eine synchrone Validierung an einer Kante angefordert wird, die diese nicht unterstützt?

Wenn die synchrone Validierung für den angeforderten Speicherort nicht unterstützt wird, wird eine 501-Fehlerantwort zurückgegeben. Weitere Informationen zur synchronen Validierung finden Sie in der Übersicht über die [Streaming-Validierung](../quality/streaming-validation.md) .

### Wie authentifiziert ich gesendete Daten?

Experience Platform unterstützt die sichere Datenerfassung. Wenn die authentifizierte Datenerfassung aktiviert ist, müssen Clients ein JSON-WebToken (JWT) und ihre IMS-Organisations-ID als Anforderungsheader senden. Weitere Informationen zum Senden authentifizierter Daten an die Plattform finden Sie im Handbuch zur [authentifizierten Datenerfassung](../tutorials/create-authenticated-streaming-connection.md).

### Wie lange dauert das Streaming von Daten an das Echtzeit-Profil?

Streaming-Ereignis werden in der Regel in weniger als 60 Sekunden im Echtzeit-Profil des Kunden angezeigt. Die tatsächlichen Latenzen können sich aufgrund des Datenvolumens, der Nachrichtengröße und der Bandbreiteneinschränkungen unterscheiden.

### Kann ich mehrere Nachrichten in dieselbe API-Anforderung einbeziehen?

Sie können mehrere Nachrichten innerhalb einer einzigen Anforderungsnutzlast gruppieren und an die Plattform streamen. Bei korrekter Verwendung ist die Gruppierung mehrerer Nachrichten in einer einzigen Anforderung eine hervorragende Möglichkeit, Ihre Datenvorgänge zu optimieren. Bitte lesen Sie das Tutorial zum [Senden mehrerer Nachrichten in einer Anfrage](../tutorials/streaming-multiple-messages.md) für weitere Informationen.

### Woher weiß ich, ob die von mir gesendeten Daten empfangen werden?

Alle Daten, die (erfolgreich oder anderweitig) an die Plattform gesendet werden, werden als Stapeldateien gespeichert, bevor sie in Datensätzen beibehalten werden. Der Verarbeitungsstatus von Stapeln erscheint im Datensatz, an den sie gesendet wurden.

Sie können überprüfen, ob die Daten erfolgreich erfasst wurden, indem Sie die Aktivität des Datensatzes über die [Experience Platform-Benutzeroberfläche](https://platform.adobe.com)überprüfen. Klicken Sie im linken Navigationsbereich auf **Datensätze** , um eine Liste der Datensätze anzuzeigen. Wählen Sie aus der angezeigten Liste den Datensatz, zu dem Sie streamen, aus, um die zugehörige Seite &quot; *Datenbestand-Aktivität* &quot;zu öffnen und alle Stapel anzuzeigen, die während eines bestimmten Zeitraums gesendet wurden. Weitere Informationen zur Verwendung von Experience Platform zur Überwachung von Datenströmen finden Sie im Handbuch zur [Überwachung von Streaming-Datenströmen](../quality/monitor-data-flows.md).

Wenn Ihre Daten nicht erfasst werden konnten und Sie sie von der Plattform wiederherstellen möchten, können Sie die fehlgeschlagenen Stapel abrufen, indem Sie ihre IDs an die [Datenzugriff-API][Data Access Service API]senden. Weitere Informationen finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md) .

### Warum sind meine Streaming-Daten nicht im Data Lake verfügbar?

Es gibt verschiedene Gründe, warum die Stapelverarbeitung möglicherweise nicht zum Data Lake gelangt, z. B. eine ungültige Formatierung, fehlende Daten oder Systemfehler. Um festzustellen, warum der Stapel fehlgeschlagen ist, müssen Sie den Stapel mit der [Data Ingestion Service API][Data Ingestion Service] abrufen und die zugehörigen Details Ansicht geben. Ausführliche Anweisungen zum Abrufen eines fehlgeschlagenen Stapels finden Sie im Handbuch zum [Abrufen fehlgeschlagener Stapel](../quality/retrieve-failed-batches.md).

### Wie parse ich die für die API-Anforderung zurückgegebene Antwort?

Sie können eine Antwort analysieren, indem Sie zunächst den Server-Antwortcode überprüfen, um festzustellen, ob Ihre Anforderung akzeptiert wurde. Wenn ein erfolgreicher Antwortcode zurückgegeben wird, können Sie das `responses` Array-Objekt überprüfen, um den Status der Erfassungsmethode zu bestimmen.

Eine erfolgreiche API-Anfrage mit einer einzelnen Meldung gibt den Statuscode 200 zurück. Eine erfolgreiche (oder teilweise erfolgreiche) Batch-Nachrichten-API-Anforderung gibt den Statuscode 207 zurück.

Die folgende JSON-Datei ist ein Beispielantwortobjekt für eine API-Anforderung mit zwei Meldungen: einer erfolgreich und einer fehlgeschlagen. Meldungen, die erfolgreich streamen, geben eine `xactionId` Eigenschaft zurück. Meldungen, die nicht streamen, geben eine `statusCode` Eigenschaft und eine Antwort `message` mit weiteren Informationen zurück.

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

### Warum werden meine gesendeten Nachrichten nicht vom Echtzeit-Kundenservice-Profil empfangen?

Wenn das Kundenkonto eine Meldung in Echtzeit ablehnt, ist dies höchstwahrscheinlich auf falsche Identitätsinformationen zurückzuführen. Dies kann darauf zurückzuführen sein, dass ein ungültiger Wert oder Namensraum für eine Identität angegeben wurde.

Es gibt zwei Arten von Identitäts-Namensräumen: Standard und benutzerdefiniert. Wenn Sie benutzerdefinierte Namensraum verwenden, stellen Sie sicher, dass der Namensraum im Identitätsdienst registriert wurde. Weitere Informationen zur Verwendung von Standard- und benutzerdefinierten Namensräumen finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/namespaces.md) .

Sie können die [Experience Platform-Benutzeroberfläche](https://platform.adobe.com) verwenden, um weitere Informationen darüber anzuzeigen, warum eine Nachricht nicht erfasst werden konnte. Klicken Sie im linken Navigationsbereich auf **Überwachung** und dann auf die Registerkarte _Streaming (Ende-zu-Ende_ -Registerkarte), um die während eines bestimmten Zeitraums gestreamen Meldungsstapel anzuzeigen.