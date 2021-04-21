---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service-Ereignis abonnieren
topic-legacy: privacy events
description: Erfahren Sie, wie Sie Privacy Service-Ereignis mit einem vorkonfigurierten Webshaken abonnieren.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 7%

---

# Abonnieren von [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sind Meldungen von Adobe Experience Platform  [!DNL Privacy Service], die Adoben I/O-Ereignis nutzen, die an einen konfigurierten Webhaken gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. Sie verringern oder beseitigen die Notwendigkeit, die [!DNL Privacy Service]-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen ist oder ein bestimmter Meilenstein in einem Workflow erreicht wurde.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
| --- | --- |
| Auftrag abgeschlossen | Alle [!DNL Experience Cloud]-Anwendungen wurden zurückgemeldet und der Gesamtstatus des Auftrags bzw. der globale Status wurde als abgeschlossen markiert. |
| Auftragsfehler | Eine oder mehrere Anwendungen haben während der Verarbeitung der Anforderung einen Fehler gemeldet. |
| Produkt abgeschlossen | Eine der mit diesem Auftrag verknüpften Anwendungen hat ihre Arbeit abgeschlossen. |
| Produktfehler | Eine der Anwendungen meldete einen Fehler bei der Verarbeitung der Anforderung. |

In diesem Dokument wird beschrieben, wie Sie eine Ereignis-Registrierung für [!DNL Privacy Service]-Benachrichtigungen einrichten und wie Sie Benachrichtigungs-Nutzdaten interpretieren.

## Erste Schritte

Lesen Sie die folgende Dokumentation zum Privacy Service, bevor Sie dieses Lernprogramm starten:

* [Übersicht über den Privacy Service](./home.md)
* [Entwicklerhandbuch für die Privacy Service-API](./api/getting-started.md)

## Registrieren eines Webhosts für [!DNL Privacy Service Events]

Um [!DNL Privacy Service Events] zu erhalten, müssen Sie Adobe Developer Console verwenden, um einen Webshaken bei Ihrer [!DNL Privacy Service]-Integration zu registrieren.

Folgen Sie dem Tutorial [Abonnieren von [!DNL I/O Event] Benachrichtigungen](../observability/notifications/subscribe.md), um detaillierte Schritte dazu zu erhalten. Stellen Sie sicher, dass Sie **[!UICONTROL Privacy Service-Ereignis]** als Ereignis-Provider auswählen, um auf die oben aufgeführten Ereignis zuzugreifen.

## [!DNL Privacy Service Event]-Benachrichtigungen empfangen

Nachdem Sie Ihren Webshaken erfolgreich registriert und Datenschutzaufträge ausgeführt haben, können Sie Beginn mit Ereignis-Benachrichtigungen aufrufen. Diese Ereignisse können mit dem Webhook selbst oder durch Auswahl der Registerkarte **[!UICONTROL Debugging-Verfolgung]** in der Projektregistrierung in der Adobe Developer Console angezeigt werden.

![](images/privacy-events/debug-tracing.png)

Die folgende JSON-Datei ist ein Beispiel für eine [!DNL Privacy Service Event]-Benachrichtigungs-Payload, die an Ihren WebHook gesendet wird, wenn eine der Anwendungen, die mit einem Datenschutzauftrag verknüpft sind, ihre Arbeit abgeschlossen hat:

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
| `type` | Die Art der gesendeten Benachrichtigung, die den Kontext zu den unter `data` bereitgestellten Informationen enthält. Mögliche Werte sind: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Ein Zeitstempel, der angibt, wann das Ereignis aufgetreten ist. |
| `data.value` | Enthält zusätzliche Informationen zum Auslöser der Benachrichtigung: <ul><li>`jobId`: Die ID des Datenschutzauftrags, der die Benachrichtigung ausgelöst hat.</li><li>`message`: Eine Meldung zum spezifischen Status des Auftrags. Für `productcomplete`- oder `producterror`-Benachrichtigungen gibt dieses Feld die betreffende Experience Cloud-Anwendung an.</li></ul> |

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Privacy Service-Ereignis für einen konfigurierten Webhook registriert werden und wie Benachrichtigungs-Nutzdaten interpretiert werden. Informationen zum Verfolgen von Datenschutzaufträgen über die Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](./ui/user-guide.md).
