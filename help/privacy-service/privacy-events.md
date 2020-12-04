---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service-Ereignis abonnieren
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 7%

---


# Abonnieren [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sind Nachrichten von Adobe Experience Platform [!DNL Privacy Service], die Adobe I/O-Ereignis nutzen, die an einen konfigurierten Webhaken gesendet werden, um eine effiziente Auftragsabwicklungsautomatisierung zu ermöglichen. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | All [!DNL Experience Cloud] applications have reported back and the overall or global status of the job has been marked as complete. |
| Auftragsfehler | Eine oder mehrere Anwendungen haben während der Verarbeitung der Anforderung einen Fehler gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verknüpften Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete einen Fehler bei der Verarbeitung der Anforderung. |

In diesem Dokument wird beschrieben, wie Sie eine Ereignis-Registrierung für [!DNL Privacy Service] Benachrichtigungen einrichten und wie Sie Benachrichtigungs-Nutzdaten interpretieren.

## Erste Schritte

Lesen Sie die folgende Dokumentation zum Privacy Service, bevor Sie dieses Lernprogramm starten:

* [Übersicht über den Privacy Service](./home.md)
* [Entwicklerhandbuch für die Privacy Service-API](./api/getting-started.md)

## Registrieren Sie einen Webshaken, um [!DNL Privacy Service Events]

Für den Empfang müssen Sie Adobe Developer Console verwenden, um einen Webshaken für Ihre [!DNL Privacy Service Events][!DNL Privacy Service] Integration zu registrieren.

Folgen Sie dem Tutorial zum [Abonnieren von [!DNL I/O Event] Tonbenachrichtigungen](../observability/notifications/subscribe.md) , um detaillierte Schritte dazu zu erhalten. Stellen Sie sicher, dass Sie **[!UICONTROL Privacy Service-Ereignis]** als Ereignis-Provider auswählen, um auf die oben aufgeführten Ereignis zuzugreifen.

## Benachrichtigungen [!DNL Privacy Service Event] empfangen

Nachdem Sie Ihren Webshaken erfolgreich registriert und Datenschutzaufträge ausgeführt haben, können Sie Beginn mit Ereignis-Benachrichtigungen aufrufen. Diese Ereignisse können mit dem Webshaken selbst oder über die Registerkarte &quot; **[!UICONTROL Debug-Ablaufverfolgung]** &quot;in der Projektregistrierung in der Adobe Developer Console angezeigt werden.

![](images/privacy-events/debug-tracing.png)

Die folgende JSON-Datei ist ein Beispiel für eine [!DNL Privacy Service Event] Benachrichtigungs-Payload, die an Ihren WebHook gesendet wird, wenn eine der Anwendungen, die mit einem Datenschutzauftrag verknüpft sind, ihre Arbeit abgeschlossen hat:

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
| `id` | Eine eindeutige, systemgenerierte ID für die Benachrichtigung. |
| `type` | Die Art der zu sendenden Benachrichtigung unter Angabe des Kontextes zu den unter `data`. Mögliche Werte sind: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel, der angibt, wann das Ereignis aufgetreten ist. |
| `data.value` | Enthält zusätzliche Informationen zum Auslöser der Benachrichtigung: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Meldung zum spezifischen Status des Auftrags. Für `productcomplete` oder `producterror` Benachrichtigungen gibt dieses Feld die betreffende Experience Cloud-Anwendung an.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Privacy Service-Ereignis für einen konfigurierten Webhook registriert werden und wie Benachrichtigungs-Nutzdaten interpretiert werden. Informationen zum Verfolgen von Datenschutzaufträgen über die Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](./ui/user-guide.md).