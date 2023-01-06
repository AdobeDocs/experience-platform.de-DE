---
keywords: Experience Platform; Startseite; beliebte Themen; Datenerfassungsbenachrichtigungen; Benachrichtigungen; Abonnement-Ereignisse; Datenerfassungsstatus-Ereignisse; Statusereignisse; Abonnement; Statusbenachrichtigungen;
solution: Experience Platform
title: Datenerfassungsbenachrichtigungen
description: Um die Überwachung des Aufnahmevorgangs zu unterstützen, ermöglicht es Adobe Experience Platform, eine Reihe von Ereignissen zu abonnieren, die von jedem Prozessschritt veröffentlicht werden. Dadurch werden Sie über den Status der aufgenommenen Daten und mögliche Fehler informiert.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 28%

---

# Benachrichtigungen zur Datenerfassung

Der Prozess der Datenaufnahme in Adobe Experience Platform besteht aus mehreren Schritten. Sobald Sie Datendateien identifiziert haben, die in aufgenommen werden müssen [!DNL Platform], beginnt der Aufnahmevorgang und jeder Schritt erfolgt nacheinander, bis die Daten erfolgreich erfasst wurden oder fehlschlagen. Der Erfassungsvorgang kann mit der [Adobe Data Ingestion-API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) oder über die Experience Platform-Benutzeroberfläche eingeleitet werden.[!DNL Experience Platform]

In geladene Daten [!DNL Platform] muss mehrere Schritte durchlaufen, um sein Ziel zu erreichen. [!DNL Data Lake] oder [!DNL Real-Time Customer Profile] Datenspeicher. Jeder Schritt umfasst die Verarbeitung der Daten, die Validierung der Daten und dann die Speicherung der Daten, bevor sie an den nächsten Schritt weitergeleitet werden. Je nachdem, wie viele Daten aufgenommen werden, kann dies ein zeitaufwendiger Prozess sein und es besteht immer die Möglichkeit, dass der Prozess aufgrund von Validierungs-, Semantik- oder Verarbeitungsfehlern fehlschlägt. Im Fall eines Fehlers müssen die Datenprobleme behoben werden und dann der gesamte Aufnahmevorgang mit den korrigierten Datendateien neu gestartet werden.

Unterstützung bei der Überwachung des Aufnahmevorgangs, [!DNL Experience Platform] ermöglicht es, eine Reihe von Ereignissen zu abonnieren, die von jedem Schritt des Prozesses veröffentlicht werden, und Sie über den Status der aufgenommenen Daten und mögliche Fehler zu informieren.

## Webhook für Benachrichtigungen zur Datenerfassung registrieren

Um Benachrichtigungen zur Datenerfassung zu erhalten, müssen Sie [Adobe Developer-Konsole](https://www.adobe.com/go/devs_console_ui) , um einen Webhook für Ihre Experience Platform-Integration zu registrieren.

Folgen Sie dem Tutorial zu [abonnieren von [!DNL Adobe I/O Event] Benachrichtigungen](../../observability/alerts/subscribe.md) für detaillierte Schritte, wie Sie dies erreichen können.

>[!IMPORTANT]
>
>Stellen Sie während des Abonnementprozesses sicher, dass Sie **[!UICONTROL Plattformbenachrichtigungen]** als Ereignisanbieter fungieren, und wählen Sie die **[!UICONTROL Benachrichtigung zur Datenerfassung]** Ereignisabonnement bei Aufforderung.

## Benachrichtigungen zur Datenerfassung empfangen

Nachdem Sie Ihren Webhook erfolgreich registriert und neue Daten erfasst haben, können Sie mit dem Empfang von Ereignisbenachrichtigungen beginnen. Diese Ereignisse können über den Webhook selbst oder durch Auswahl der **[!UICONTROL Debug-Verfolgung]** in der Übersicht über die Ereignisregistrierung in der Adobe Developer Console Ihres Projekts.

Die folgende JSON-Datei ist ein Beispiel für eine Benachrichtigungs-Payload, die bei einem fehlgeschlagenen Batch-Erfassungsereignis an Ihren Webhook gesendet wird:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
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
| `event.xdm:datasetId` | Die ID des Datensatzes, für den das Aufnahmeereignis gilt. |
| `event.xdm:eventCode` | Ein Statuscode, der den Typ des Ereignisses angibt, das für den Datensatz ausgelöst wurde. Siehe [Anhang](#event-codes) für bestimmte Werte und deren Definitionen. |

Das vollständige Schema für Ereignisbenachrichtigungen finden Sie im Abschnitt [öffentliches GitHub-Repository](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Nächste Schritte

Sobald Sie sich registriert haben [!DNL Platform] Benachrichtigungen an Ihr Projekt können Sie die empfangenen Ereignisse aus dem [!UICONTROL Projektübersicht]. Weitere Informationen finden Sie im Handbuch [Tracking-Adobe I/O-Ereignisse](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) für detaillierte Anweisungen zur Verfolgung Ihrer Ereignisse.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Interpretation der Payloads von Datenerfassungsbenachrichtigungen.

### Verfügbare Statusbenachrichtigungs-Ereignisse {#event-codes}

In der folgenden Tabelle sind die verfügbaren Statusbenachrichtigungen zur Datenerfassung aufgeführt, die Sie abonnieren können.

| Ereignis-Code | Platform Service | Status | Ereignisbeschreibung |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | Erfolgreich | Ein Batch wurde erfolgreich in einen Datensatz innerhalb der [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | Fehlgeschlagen | Ein Batch konnte nicht in einen Datensatz innerhalb der [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | Erfolgreich | Ein Batch wurde erfolgreich in die [!DNL Profile] Datenspeicher. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | Fehlgeschlagen | Ein Batch konnte nicht in die [!DNL Profile] Datenspeicher. |
| `ig_load_success` | [!DNL Identity Service] | Erfolgreich | Daten wurden erfolgreich in das Identitätsdiagramm geladen. |
| `ig_load_failure` | [!DNL Identity Service] | Fehlgeschlagen | Daten konnten nicht in das Identitätsdiagramm geladen werden. |

>[!NOTE]
>
> Es wird nur ein Ereignisthema für alle Benachrichtigungen zur Datenerfassung bereitgestellt. Zur Unterscheidung zwischen verschiedenen Status kann der Ereignis-Code verwendet werden.
