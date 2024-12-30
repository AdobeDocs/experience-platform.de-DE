---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service-Ereignisse abonnieren
description: Erfahren Sie, wie Sie Privacy Service-Ereignisse mit einem vorkonfigurierten Webhook abonnieren.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 8%

---

# [!DNL Privacy Service Events] abonnieren

[!DNL Privacy Service Events] sind Nachrichten, die von Adobe Experience Platform [!DNL Privacy Service] bereitgestellt werden und Adobe I/O-Ereignisse nutzen, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | Alle [!DNL Experience Cloud] Bewerbungen wurden zurückgemeldet und der Gesamt- oder globale Status des Auftrags wurde als abgeschlossen markiert. |
| Auftragsfehler | Mindestens eine Anwendung hat bei der Verarbeitung der Anfrage einen Fehler gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verknüpften Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete einen Fehler bei der Verarbeitung der Anfrage. |

In diesem Dokument werden die Schritte zum Einrichten einer Ereignisregistrierung für [!DNL Privacy Service]-Benachrichtigungen und zum Interpretieren von Benachrichtigungs-Payloads beschrieben.

## Erste Schritte

Lesen Sie die folgende Privacy Service-Dokumentation, bevor Sie mit diesem Tutorial beginnen:

* [Übersicht über Privacy Service](./home.md)
* [Privacy Service-API-Handbuch](./api/overview.md)

## Registrieren eines Webhooks für [!DNL Privacy Service Events]

Um [!DNL Privacy Service Events] zu erhalten, müssen Sie Adobe Developer Console verwenden, um einen Webhook zu Ihrer [!DNL Privacy Service]-Integration zu registrieren.

Im Tutorial zum [ von [!DNL I/O Event]-Benachrichtigungen ](../observability/alerts/subscribe.md) Sie ausführliche Schritte, wie Sie dies tun können. Stellen Sie sicher, dass Sie **[!UICONTROL Ereignisereignisse]** als Ereignisanbieter auswählen, um auf die oben aufgeführten Privacy Services zuzugreifen.

## [!DNL Privacy Service Event] Benachrichtigungen empfangen

Nachdem Sie Ihren Webhook erfolgreich registriert und Datenschutzaufträge ausgeführt haben, können Sie beginnen, Ereignisbenachrichtigungen zu erhalten. Diese Ereignisse können mit dem Webhook selbst oder durch Auswahl der Registerkarte **[!UICONTROL Debug-]**&quot; in der Übersicht über die Ereignisregistrierung Ihres Projekts in Adobe Developer Console angezeigt werden.

![](images/privacy-events/debug-tracing.png)

Die folgende JSON-Datei ist ein Beispiel für eine [!DNL Privacy Service Event] Benachrichtigungs-Payload, die an Ihren Webhook gesendet wird, wenn eine der mit einem Datenschutzauftrag verknüpften Anwendungen seine Arbeit abgeschlossen hat:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Eine eindeutige, systemgenerierte ID für die Benachrichtigung. |
| `type` | Die Art der gesendeten Benachrichtigung, wobei der Kontext der unter `data` bereitgestellten Informationen angegeben wird. Zu den möglichen Werten gehören: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel, der angibt, wann das Ereignis aufgetreten ist. |
| `data.value` | Enthält zusätzliche Informationen darüber, wodurch die Benachrichtigung ausgelöst wurde: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Nachricht zum spezifischen Status des Auftrags. Bei `productcomplete`- oder `producterror`-Benachrichtigungen gibt dieses Feld die betreffende Experience Cloud-Anwendung an.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie Privacy Service-Ereignisse in einem konfigurierten Webhook registrieren und Benachrichtigungs-Payloads interpretieren. Informationen zum Nachverfolgen von Datenschutzaufträgen mithilfe der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](./ui/user-guide.md).
