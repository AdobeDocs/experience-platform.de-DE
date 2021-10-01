---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Abonnieren von Privacy Service-Ereignissen
topic-legacy: privacy events
description: Erfahren Sie, wie Sie Privacy Service-Ereignisse mit einem vorkonfigurierten Webhook abonnieren.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: a455134a45137b171636d6525ce9124bc95f4335
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 15%

---

# Abonnieren Sie [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sind von Adobe Experience Platform bereitgestellte Nachrichten,  [!DNL Privacy Service]die Adobe I/O-Ereignisse nutzen, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Automatisierung von Auftragsanfragen zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | Alle [!DNL Experience Cloud] -Anwendungen haben einen Bericht erstellt und der Gesamtstatus bzw. der globale Status des Auftrags wurde als abgeschlossen markiert. |
| Auftragsfehler | Eine oder mehrere Anwendungen haben bei der Verarbeitung der Anfrage einen Fehler gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verknüpften Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete bei der Verarbeitung der Anfrage einen Fehler. |

In diesem Dokument werden Schritte zum Einrichten einer Ereignisregistrierung für [!DNL Privacy Service]-Benachrichtigungen und zum Interpretieren der Benachrichtigungs-Payloads beschrieben.

## Erste Schritte

Lesen Sie die folgende Privacy Service-Dokumentation, bevor Sie mit diesem Tutorial beginnen:

* [Übersicht über Privacy Service](./home.md)
* [Entwicklerhandbuch für die Privacy Service-API](./api/getting-started.md)

## Registrieren Sie einen Webhook bei [!DNL Privacy Service Events].

Um [!DNL Privacy Service Events] zu erhalten, müssen Sie die Adobe Developer Console verwenden, um einen Webhook für Ihre [!DNL Privacy Service] -Integration zu registrieren.

Folgen Sie dem Tutorial zu [Abonnieren von [!DNL I/O Event] Benachrichtigungen](../observability/alerts/subscribe.md) , um detaillierte Anweisungen dazu zu erhalten. Stellen Sie sicher, dass Sie **[!UICONTROL Privacy Service Events]** als Ereignisanbieter auswählen, um auf die oben aufgeführten Ereignisse zuzugreifen.

## [!DNL Privacy Service Event]-Benachrichtigungen empfangen

Nachdem Sie Ihren Webhook erfolgreich registriert und Datenschutzaufträge ausgeführt haben, können Sie mit dem Empfang von Ereignisbenachrichtigungen beginnen. Diese Ereignisse können über den Webhook selbst oder durch Auswahl der Registerkarte **[!UICONTROL Debug Tracing]** in der Übersicht zur Ereignisregistrierung Ihres Projekts in der Adobe Developer Console angezeigt werden.

![](images/privacy-events/debug-tracing.png)

Die folgende JSON-Datei ist ein Beispiel für eine [!DNL Privacy Service Event]-Benachrichtigungs-Payload, die an Ihren Webhook gesendet wird, wenn eine der Anwendungen, die mit einem Datenschutzauftrag verknüpft sind, ihre Arbeit abgeschlossen hat:

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
| `type` | Die Art der zu sendenden Benachrichtigung unter Angabe des Kontexts für die unter `data` bereitgestellten Informationen. Mögliche Werte sind: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel, der angibt, wann das Ereignis aufgetreten ist. |
| `data.value` | Enthält zusätzliche Informationen darüber, was die Benachrichtigung ausgelöst hat: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Meldung zum spezifischen Status des Auftrags. Bei `productcomplete` - oder `producterror` -Benachrichtigungen gibt dieses Feld die betreffende Experience Cloud-Anwendung an.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Privacy Service-Ereignisse für einen konfigurierten Webhook registriert werden und wie Benachrichtigungs-Payloads interpretiert werden. Informationen zum Tracking von Datenschutzaufträgen über die Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](./ui/user-guide.md).
