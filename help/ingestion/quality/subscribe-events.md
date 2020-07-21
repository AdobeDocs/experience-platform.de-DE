---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abonnieren von Datenaufnahme-Ereignissen
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 38%

---


# Benachrichtigungen zur Datenaufnahme

Der Prozess der Datenaufnahme in Adobe Experience Platform besteht aus mehreren Schritten. Once you identify data files that need to be ingested into [!DNL Platform], the ingestion process begins and each step occurs consecutively until the data is either successfully ingested or fails. Der Aufnahmevorgang kann mit der [Adobe Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) oder über die Experience Platform-Benutzeroberfläche eingeleitet werden.[!DNL Experience Platform]

Data loaded into [!DNL Platform] must go through multiple steps in order to reach its destination, the [!DNL Data Lake] or the [!DNL Real-time Customer Profile] data store. Jeder Schritt umfasst die Verarbeitung der Daten, die Validierung der Daten und dann die Speicherung der Daten, bevor sie an den nächsten Schritt weitergeleitet werden. Je nachdem, wie viele Daten aufgenommen werden, kann dies ein zeitaufwendiger Prozess sein und es besteht immer die Möglichkeit, dass der Prozess aufgrund von Validierungs-, Semantik- oder Verarbeitungsfehlern fehlschlägt. Im Fall eines Fehlers müssen die Datenprobleme behoben werden und dann der gesamte Aufnahmevorgang mit den korrigierten Datendateien neu gestartet werden.

To assist in monitoring the ingestion process, [!DNL Experience Platform] makes it possible to subscribe to a set of events that are published by each step of the process, notifying you to the status of the ingested data and any possible failures.

## Verfügbare Statusbenachrichtigungs-Ereignisse

Im Folgenden finden Sie eine Liste der verfügbaren Statusbenachrichtigungen zur Datenaufnahme, die Sie abonnieren können.

>[!NOTE]
>
>Es wird nur ein Ereignisthema für alle Benachrichtigungen zur Datenaufnahme bereitgestellt. Zur Unterscheidung zwischen verschiedenen Status kann der Ereignis-Code verwendet werden.

| Platform Service | Status | Ereignisbeschreibung | Ereignis-Code |
| ---------------- | ------ | ----------------- | ---------- |
| Data Landing | Erfolgreich | Aufnahme – Batch erfolgreich | ing_load_success |
| Data Landing | Fehlgeschlagen | Aufnahme – Batch fehlgeschlagen | ing_load_failure |
| Echtzeit-Kundenprofil | Erfolgreich | Profil-Dienst – Datenlade-Batch erfolgreich | ps_load_success |
| Echtzeit-Kundenprofil | Fehlgeschlagen | Profil-Dienst - Datenlade-Batch fehlgeschlagen | ps_load_failure |
| Identitätsdiagramm | Erfolgreich | Identitätsdiagramm – Datenlade-Batch erfolgreich | ig_load_success |
| Identitätsdiagramm | Fehlgeschlagen | Identitätsdiagramm – Datenlade-Batch fehlgeschlagen | ig_load_failure |

## Benachrichtigungs-Payload-Schema

The data ingestion notification event schema is an [!DNL Experience Data Model] (XDM) schema containing fields and values that provide details regarding the status of the data being ingested. Please visit the public XDM [!DNL GitHub] repo in order to view the latest [notification payload schema](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json).

## Statusbenachrichtigungen zur Datenaufnahme abonnieren

Über [Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events.html) können Sie mehrere Benachrichtigungstypen über Webhooks abonnieren. In den folgenden Abschnitten werden die Schritte zum Abonnieren von [!DNL Platform] Benachrichtigungen für Datenerfassungs-Ereignis mit der Adobe Developer Console beschrieben.

### Neues Projekt in der Adobe Developer Console erstellen

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) and sign in with your Adobe ID. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

### Hinzufügen von [!DNL Experience Platform] Ereignissen

Nachdem Sie ein neues Projekt erstellt haben, navigieren Sie zum Übersichtsbildschirm dieses Projekts. Klicken Sie von hier auf **[!UICONTROL Hinzufügen Ereignis]**.

![](../images/quality/subscribe-events/add-event-button.png)

The _[!UICONTROL Add events]_dialog appears. Klicken Sie auf**[!UICONTROL  Experience Platform ]**, um die Liste der verfügbaren Optionen zu filtern, und klicken Sie dann auf**[!UICONTROL  Plattformbenachrichtigungen ]**, bevor Sie auf**[!UICONTROL  Weiter ]**klicken.

![](../images/quality/subscribe-events/select-platform-events.png)

Im nächsten Bildschirm wird eine Liste von Ereignistypen angezeigt, die abonniert werden sollen. Wählen Sie **[!UICONTROL Datenerfassungsbenachrichtigung]** und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../images/quality/subscribe-events/choose-event-subscriptions.png)

Im nächsten Bildschirm werden Sie aufgefordert, ein JSON-WebToken (JWT) zu erstellen. Sie haben die Möglichkeit, automatisch ein Schlüsselpaar zu erstellen oder einen eigenen öffentlichen Schlüssel hochzuladen, der im Terminal generiert wurde.

Für diese Übung wird die erste Option verwendet. Markieren Sie das Optionsfeld für **[!UICONTROL Generate a key pair]** und klicken Sie dann unten rechts auf die Schaltfläche **[!UICONTROL Generate keypair]** .

![](../images/quality/subscribe-events/generate-keypair.png)

Wenn das Schlüsselpaar generiert wird, wird es automatisch vom Browser heruntergeladen. Sie müssen diese Datei selbst speichern, da sie nicht in der Developer Console beibehalten wird.

Im nächsten Bildschirm können Sie die Details des neu generierten Schlüsselpaars überprüfen. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../images/quality/subscribe-events/keypair-generated.png)

Geben Sie im nächsten Bildschirm einen Namen und eine Beschreibung für die Registrierung des Ereignisses ein. Best Practice ist, einen eindeutigen, leicht identifizierbaren Namen zu erstellen, um diese Ereignis-Registrierung von anderen im selben Projekt zu unterscheiden.

![](../images/quality/subscribe-events/registration-details.png)

Weiter unten auf dem gleichen Bildschirm können Sie optional konfigurieren, wie Ereignis empfangen werden. **[!UICONTROL Mit WebHook]** können Sie eine benutzerdefinierte Webhocker-Adresse für den Empfang von Ereignissen angeben, während die **[!UICONTROL Laufzeitaktion]** es Ihnen ermöglicht, dasselbe mit der [Adobe I/O-Laufzeit](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)zu tun.

Dieses Lernprogramm überspringt diesen optionalen Konfigurationsschritt. Nachdem Sie fertig sind, klicken Sie auf **[!UICONTROL Konfigurierte Ereignisse]** speichern, um die Ereignis-Registrierung abzuschließen.

![](../images/quality/subscribe-events/receive-events.png)

Die Detailseite für die neu erstellte Ereignis-Registrierung wird angezeigt, auf der Sie die empfangenen Ereignis überprüfen, die Debugging-Verfolgung durchführen und die Konfiguration bearbeiten können.

![](../images/quality/subscribe-events/registration-complete.png)

## Nächste Schritte

Nachdem Sie [!DNL Platform] Benachrichtigungen zu Ihrem Projekt registriert haben, können Sie Ereignisse aus dem Dashboard des Projekts Ansicht haben. Detaillierte Anweisungen zur Verfolgung Ihrer Ereignisse finden Sie in der Anleitung [Verfolgung von Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md).
