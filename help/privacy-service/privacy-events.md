---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Privacy Service-Ereignis abonnieren
topic-legacy: privacy events
description: Erfahren Sie, wie Sie Privacy Service-Ereignisse mit einem vorkonfigurierten Webhaken abonnieren.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 15%

---

# Abonnieren [!DNL Privacy Service Events]

[!DNL Privacy Service Events] von Adobe Experience Platform bereitgestellte Nachrichten [!DNL Privacy Service], die Adobe I/O-Ereignis, die an einen konfigurierten Webhaken gesendet werden, nutzen, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | Alle [!DNL Experience Cloud] -Anwendungen wurden zurückgemeldet und der Gesamtstatus des Auftrags oder der Gesamtstatus des Auftrags wurde als vollständig markiert. |
| Auftragsfehler | Eine oder mehrere Anwendungen haben einen Fehler bei der Verarbeitung der Anforderung gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verbundenen Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete einen Fehler bei der Verarbeitung der Anforderung. |

Dieses Dokument enthält Schritte zum Einrichten einer Ereignis-Registrierung für [!DNL Privacy Service] Benachrichtigungen und die Interpretation von Benachrichtigungs-Payloads.

## Erste Schritte

Bitte lesen Sie die folgende Dokumentation zum Privacy Service, bevor Sie dieses Tutorial starten:

* [Übersicht über Privacy Service](./home.md)
* [Privacy Service-API-Handbuch](./api/overview.md)

## Webhook registrieren für [!DNL Privacy Service Events]

Um [!DNL Privacy Service Events]verwenden, müssen Sie die Adobe Developer Console verwenden, um einen Webhaken bei Ihrem [!DNL Privacy Service] Integration.

Folgen Sie dem Tutorial auf [abonnieren von [!DNL I/O Event] Benachrichtigungen](../observability/alerts/subscribe.md) für detaillierte Schritte, wie Sie dies erreichen können. Stellen Sie sicher, dass Sie **[!UICONTROL Privacy Service-Ereignis]** als Ihr Ereignis-Provider, um auf die oben aufgeführten Ereignis zuzugreifen.

## empfangen [!DNL Privacy Service Event] Benachrichtigungen

Wenn Sie Ihren Webhaken erfolgreich registriert haben und Datenschutzaufträge ausgeführt wurden, können Sie Beginn werden, der Ereignis-Benachrichtigungen erhält. Diese Ereignisse können mit dem Webhook selbst oder durch Auswahl der **[!UICONTROL Debugging-Ablaufverfolgung]** in der Übersicht über die Registrierung von Ereignissen in der Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Das folgende JSON ist ein Beispiel für [!DNL Privacy Service Event] Benachrichtigungs-Payload, die an Ihren WebHook gesendet wird, wenn eine der Anwendungen, die einem Datenschutzauftrag zugeordnet sind, seine Arbeit abgeschlossen hat:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Eine eindeutige, vom System generierte ID für die Benachrichtigung. |
| `type` | Art der zu sendenden Benachrichtigung unter Angabe des Kontextes zu den unter `data`. Mögliche Werte sind: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel zum Auftreten des Ereignisses. |
| `data.value` | Enthält zusätzliche Informationen über den Auslöser der Benachrichtigung: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Nachricht zum spezifischen Status des Auftrags. für `productcomplete` oder `producterror` -Benachrichtigungen, zeigt dieses Feld die betreffende Experience Cloud-Anwendung an.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Privacy Service-Ereignis in einen konfigurierten Webhaken registriert werden und wie Benachrichtigungs-Payloads interpretiert werden. Informationen zur Verfolgung von Datenschutzaufträgen über die Benutzeroberfläche finden Sie in der [Privacy Service-Benutzerhandbuch](./ui/user-guide.md).
