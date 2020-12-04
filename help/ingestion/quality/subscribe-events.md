---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Abonnieren von Datenerfassungsereignissen
topic: overview
description: Um den Erfassungsvorgang zu überwachen, kann Adobe Experience Platform eine Reihe von Ereignissen abonnieren, die von jedem Prozessschritt veröffentlicht werden, und Sie über den Status der erfassten Daten und eventuelle Fehler informieren.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 30%

---


# Benachrichtigungen zur Datenerfassung

Der Prozess der Datenaufnahme in Adobe Experience Platform besteht aus mehreren Schritten. Once you identify data files that need to be ingested into [!DNL Platform], the ingestion process begins and each step occurs consecutively until the data is either successfully ingested or fails. Der Erfassungsvorgang kann mit der [Adobe Data Ingestion-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) oder über die Experience Platform-Benutzeroberfläche eingeleitet werden.[!DNL Experience Platform]

Data loaded into [!DNL Platform] must go through multiple steps in order to reach its destination, the [!DNL Data Lake] or the [!DNL Real-time Customer Profile] data store. Jeder Schritt umfasst die Verarbeitung der Daten, die Validierung der Daten und dann die Speicherung der Daten, bevor sie an den nächsten Schritt weitergeleitet werden. Je nachdem, wie viele Daten aufgenommen werden, kann dies ein zeitaufwendiger Prozess sein und es besteht immer die Möglichkeit, dass der Prozess aufgrund von Validierungs-, Semantik- oder Verarbeitungsfehlern fehlschlägt. Im Fall eines Fehlers müssen die Datenprobleme behoben werden und dann der gesamte Aufnahmevorgang mit den korrigierten Datendateien neu gestartet werden.

To assist in monitoring the ingestion process, [!DNL Experience Platform] makes it possible to subscribe to a set of events that are published by each step of the process, notifying you to the status of the ingested data and any possible failures.

## Registrieren eines Webhofs für Benachrichtigungen zur Datenaufnahme

Um Benachrichtigungen zur Datenerfassung zu erhalten, müssen Sie die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_de) verwenden, um einen Webshaken für Ihre Experience Platform-Integration zu registrieren.

Folgen Sie dem Tutorial zum [Abonnieren von [!DNL Adobe I/O Event] Tonbenachrichtigungen](../../observability/notifications/subscribe.md) , um detaillierte Schritte dazu zu erhalten.

>[!IMPORTANT]
>
>Stellen Sie während des Abonnements sicher, dass Sie **[!UICONTROL Plattformbenachrichtigungen]** als Ereignis-Provider auswählen und bei Aufforderung das Ereignis für **[!UICONTROL Dateneingabebenachrichtigungen]** auswählen.

## Benachrichtigungen zur Datenerfassung erhalten

Nachdem Sie Ihren Webhook erfolgreich registriert und neue Daten erfasst haben, können Sie Beginn mit Ereignis-Benachrichtigungen aufrufen. Diese Ereignisse können mit dem Webshaken selbst oder über die Registerkarte &quot; **[!UICONTROL Debug-Ablaufverfolgung]** &quot;in der Projektregistrierung in der Adobe Developer Console angezeigt werden.

Die folgende JSON-Datei ist ein Beispiel für eine Benachrichtigungs-Nutzlast, die bei einem fehlgeschlagenen Batch-ErfassungsEreignis an Ihren Webhook gesendet wird:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `event_id` | Eine eindeutige, systemgenerierte ID für die Benachrichtigung. |
| `event` | Ein Objekt, das die Details des Ereignisses enthält, das die Benachrichtigung ausgelöst hat. |
| `event.xdm:datasetId` | Die ID des Datensatzes, auf den das Ereignis &quot;Inkraftsetzung&quot;angewendet wird. |
| `event.xdm:eventCode` | Ein Statuscode, der den Typ des Ereignisses angibt, das für den Datensatz ausgelöst wurde. Spezifische Werte und deren Definitionen finden Sie im [Anhang](#event-codes) . |

Informationen zur Ansicht des vollständigen Schemas für Ereignis-Benachrichtigungen finden Sie im [öffentlichen GitHub-Repository](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Nächste Schritte

Nachdem Sie [!DNL Platform] Benachrichtigungen zu Ihrem Projekt registriert haben, können Sie Ereignisse aus der [!UICONTROL Projektübersicht]Ansicht haben. Refer to the guide on [tracing Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) for detailed instructions on how to trace your events.

## Anhang

Der folgende Abschnitt enthält weitere Informationen zur Interpretation der Nutzdaten von Dateneingabebenachrichtigungen.

### Verfügbare Statusbenachrichtigungs-Ereignisse {#event-codes}

In der folgenden Tabelle werden die verfügbaren Statusbenachrichtigungen zur Datenaufnahme Liste, die Sie abonnieren können.

| Ereignis-Code | Platform Service | Status | Ereignisbeschreibung |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | Erfolgreich | Ein Stapel wurde erfolgreich in einen Datensatz innerhalb des [!DNL Data Lake]Stapels eingefügt. |
| `ing_load_failure` | [!DNL Data Ingestion] | Fehlgeschlagen | Ein Stapel konnte nicht in einen Datensatz innerhalb des [!DNL Data Lake]Stapels aufgenommen werden. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | Erfolgreich | Ein Stapel wurde erfolgreich in den [!DNL Profile] Datenspeicher aufgenommen. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | Fehlgeschlagen | Ein Stapel konnte nicht in den [!DNL Profile] Datenspeicher aufgenommen werden. |
| `ig_load_success` | [!DNL Identity Service] | Erfolgreich | Daten wurden erfolgreich in das Identitätsdiagramm geladen. |
| `ig_load_failure` | [!DNL Identity Service] | Fehlgeschlagen | Daten konnten nicht in das Identitätsdiagramm geladen werden. |

>[!NOTE]
>
> Es wird nur ein Ereignisthema für alle Benachrichtigungen zur Datenerfassung bereitgestellt. Zur Unterscheidung zwischen verschiedenen Status kann der Ereignis-Code verwendet werden.