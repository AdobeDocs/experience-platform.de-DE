---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Abonnieren von Privacy Service-Ereignissen
description: Erfahren Sie, wie Sie Privacy Service-Ereignisse mit einem vorkonfigurierten Webhook abonnieren.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 15%

---

# Abonnieren Sie [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sind Nachrichten, die von Adobe Experience Platform bereitgestellt werden [!DNL Privacy Service], die Adobe I/O-Ereignisse nutzen, die an einen konfigurierten Webhook gesendet werden, um eine effiziente Automatisierung von Auftragsanfragen zu ermöglichen. Sie verringern oder eliminieren die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen oder eine bestimmte Etappe in einem Workflow erreicht wurde.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | Alle [!DNL Experience Cloud] -Anwendungen wurden zurückgemeldet und der allgemeine oder globale Status des Auftrags wurde als abgeschlossen markiert. |
| Auftragsfehler | Eine oder mehrere Anwendungen haben bei der Verarbeitung der Anfrage einen Fehler gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verknüpften Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete bei der Verarbeitung der Anfrage einen Fehler. |

Dieses Dokument enthält Schritte zum Einrichten einer Ereignisregistrierung für [!DNL Privacy Service] Benachrichtigungen und wie Benachrichtigungs-Payloads interpretiert werden.

## Erste Schritte

Lesen Sie die folgende Privacy Service-Dokumentation, bevor Sie mit diesem Tutorial beginnen:

* [Übersicht über Privacy Service](./home.md)
* [Handbuch zur Privacy Service-API](./api/overview.md)

## Registrieren Sie einen Webhook für [!DNL Privacy Service Events]

Um [!DNL Privacy Service Events]müssen Sie die Adobe Developer Console verwenden, um einen Webhook für Ihre [!DNL Privacy Service] Integration.

Folgen Sie dem Tutorial zu [Abonnieren von [!DNL I/O Event]-Benachrichtigungen](../observability/alerts/subscribe.md) für detaillierte Schritte, wie Sie dies erreichen können. Stellen Sie sicher, dass Sie **[!UICONTROL Privacy Service-Ereignisse]** als Ereignisanbieter, um auf die oben aufgeführten Ereignisse zuzugreifen.

## Empfangen [!DNL Privacy Service Event] Benachrichtigungen

Nachdem Sie Ihren Webhook erfolgreich registriert und Datenschutzaufträge ausgeführt haben, können Sie mit dem Empfang von Ereignisbenachrichtigungen beginnen. Diese Ereignisse können über den Webhook selbst oder durch Auswahl der **[!UICONTROL Debug-Verfolgung]** in der Übersicht über die Ereignisregistrierung in der Adobe Developer Console Ihres Projekts.

![](images/privacy-events/debug-tracing.png)

Die folgende JSON-Datei ist ein Beispiel für eine [!DNL Privacy Service Event] Benachrichtigungs-Payload, die an Ihren Webhook gesendet wird, wenn eine der mit einem Datenschutzauftrag verknüpften Anwendungen ihre Arbeit abgeschlossen hat:

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
| `type` | Die Art der zu sendenden Benachrichtigung unter Angabe des Kontexts für die unter `data`. Mögliche Werte sind: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel, der angibt, wann das Ereignis aufgetreten ist. |
| `data.value` | Enthält zusätzliche Informationen darüber, was die Benachrichtigung ausgelöst hat: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Meldung zum spezifischen Status des Auftrags. Für `productcomplete` oder `producterror` Benachrichtigungen enthält, wird in diesem Feld die betreffende Experience Cloud-Anwendung angegeben.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Privacy Service-Ereignisse für einen konfigurierten Webhook registriert werden und wie Benachrichtigungs-Payloads interpretiert werden. Informationen zum Tracking von Datenschutzaufträgen über die Benutzeroberfläche finden Sie in der [Benutzerhandbuch für Privacy Service](./ui/user-guide.md).
