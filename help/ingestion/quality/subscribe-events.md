---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassungsbenachrichtigungen;Benachrichtigungen;Abonnierenereignisse;Datenerfassungsstatusereignisse;Statusereignisse;abonnieren;Statusbenachrichtigungen;
solution: Experience Platform
title: Benachrichtigungen zur Datenaufnahme
description: Um die Überwachung des Aufnahmeprozesses zu unterstützen, ermöglicht Adobe Experience Platform das Abonnieren einer Reihe von Ereignissen, die von jedem Schritt des Prozesses veröffentlicht werden und Sie über den Status der aufgenommenen Daten und mögliche Fehler informieren.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 20%

---

# Benachrichtigungen zur Datenerfassung

Der Prozess der Datenaufnahme in Adobe Experience Platform besteht aus mehreren Schritten. Sobald Sie Datendateien identifiziert haben, die in [!DNL Experience Platform] aufgenommen werden müssen, beginnt der Aufnahmeprozess und jeder Schritt findet nacheinander statt, bis die Daten entweder erfolgreich aufgenommen wurden oder fehlschlagen. Der Aufnahmevorgang kann über die [Batch-Aufnahme-API von Adobe Experience Platform &#x200B;](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) über die [!DNL Experience Platform] Benutzeroberfläche initiiert werden.

Daten, die in [!DNL Experience Platform] geladen werden, müssen mehrere Schritte durchlaufen, um ihr Ziel, den [!DNL Data Lake] oder den [!DNL Real-Time Customer Profile] Datenspeicher zu erreichen. Jeder Schritt umfasst die Verarbeitung der Daten, die Validierung der Daten und dann die Speicherung der Daten, bevor sie an den nächsten Schritt weitergeleitet werden. Je nachdem, wie viele Daten aufgenommen werden, kann dies ein zeitaufwendiger Prozess sein und es besteht immer die Möglichkeit, dass der Prozess aufgrund von Validierungs-, Semantik- oder Verarbeitungsfehlern fehlschlägt. Im Fall eines Fehlers müssen die Datenprobleme behoben werden und dann der gesamte Aufnahmevorgang mit den korrigierten Datendateien neu gestartet werden.

Um die Überwachung des Aufnahmeprozesses zu unterstützen, ermöglicht [!DNL Experience Platform] das Abonnieren einer Reihe von Ereignissen, die von jedem Schritt des Prozesses veröffentlicht werden und Sie über den Status der aufgenommenen Daten und mögliche Fehler informieren.

## Registrieren eines Webhooks für Datenerfassungsbenachrichtigungen

Um Datenaufnahmebenachrichtigungen zu erhalten, müssen Sie [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) verwenden, um einen Webhook zu Ihrer Experience Platform-Integration zu registrieren.

Im Tutorial [Abonnieren von [!DNL Adobe I/O Event] Benachrichtigungen“ &#x200B;](../../observability/alerts/subscribe.md) Sie ausführliche Schritte, wie Sie dies tun können.

>[!IMPORTANT]
>
>Stellen Sie während des Abonnementvorgangs sicher, dass Sie **[!UICONTROL Platform-Benachrichtigungen]** als Ereignisanbieter auswählen und das **[!UICONTROL Benachrichtigung zur Datenaufnahme]** Ereignisabonnement auswählen, wenn Sie dazu aufgefordert werden.

## Empfangen von Datenerfassungsbenachrichtigungen

Nachdem Sie Ihren Webhook erfolgreich registriert und neue Daten aufgenommen haben, können Sie beginnen, Ereignisbenachrichtigungen zu erhalten. Diese Ereignisse können mit dem Webhook selbst oder durch Auswahl der Registerkarte **[!UICONTROL Debug-]**&quot; in der Übersicht über die Ereignisregistrierung Ihres Projekts in Adobe Developer Console angezeigt werden.

Die folgende JSON-Datei ist ein Beispiel für eine Benachrichtigungs-Payload, die im Falle eines fehlgeschlagenen Batch-Erfassungsereignisses an Ihren Webhook gesendet wird:

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
| `event.xdm:eventCode` | Ein Status-Code, der den Typ des Ereignisses angibt, das für den Datensatz ausgelöst wurde. Siehe [Anhang](#event-codes) für bestimmte Werte und ihre Definitionen. |

Das vollständige Schema für Ereignis-Benachrichtigungen finden Sie im [öffentlichen GitHub-Repository](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Nächste Schritte

Nachdem Sie [!DNL Experience Platform]-Benachrichtigungen für Ihr Projekt registriert haben, können Sie die empfangenen Ereignisse in der [!UICONTROL Projektübersicht“ &#x200B;]. Ausführliche Anweisungen zum Nachverfolgen [&#x200B; Ereignisse finden Sie im Handbuch &#x200B;](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)Nachverfolgen von Adobe I/O Events&quot;.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Interpretation der Payloads von Datenerfassungsbenachrichtigungen.

### Verfügbare Statusbenachrichtigungs-Ereignisse {#event-codes}

In der folgenden Tabelle sind die verfügbaren Statusbenachrichtigungen zur Datenaufnahme aufgeführt, die Sie abonnieren können.

| Ereignis-Code | Experience Platform-Service | Status | Ereignisbeschreibung |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | Erfolgreich | Ein Batch wurde erfolgreich in einen Datensatz im [!DNL Data Lake] aufgenommen. |
| `ing_load_failure` | [!DNL Data Ingestion] | Fehlgeschlagen | Ein Batch konnte nicht in einen Datensatz im [!DNL Data Lake] aufgenommen werden. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | Erfolgreich | Ein Batch wurde erfolgreich in den [!DNL Profile] Datenspeicher aufgenommen. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | Fehlgeschlagen | Ein Batch konnte nicht in den [!DNL Profile]-Datenspeicher aufgenommen werden. |
| `ig_load_success` | [!DNL Identity Service] | Erfolgreich | Die Daten wurden erfolgreich in das Identitätsdiagramm geladen. |
| `ig_load_failure` | [!DNL Identity Service] | Fehlgeschlagen | Daten konnten nicht in das Identitätsdiagramm geladen werden. |

>[!NOTE]
>
>Für alle Datenerfassungsbenachrichtigungen wird nur ein Ereignisthema bereitgestellt. Zur Unterscheidung zwischen verschiedenen Status kann der Ereignis-Code verwendet werden.
