---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ereignisse zur Datenerfassung abonnieren
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Benachrichtigungen zur Datenaufnahme

Der Prozess der Dateneingabe in Adobe Experience Platform besteht aus mehreren Schritten. Sobald Sie Datendateien identifiziert haben, die in die Plattform aufgenommen werden müssen, beginnt der Erfassungsvorgang und jeder Schritt erfolgt nacheinander, bis die Daten erfolgreich erfasst wurden oder fehlschlagen. Der Erfassungsvorgang kann mit der [Adobe Experience Platform Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) oder über die Experience Platform-Benutzeroberfläche eingeleitet werden.

Daten, die in die Plattform geladen werden, müssen mehrere Schritte durchlaufen, um ihr Ziel, den Data Lake oder den Echtzeit-Kundendatenspeicher, zu erreichen. Jeder Schritt umfasst die Verarbeitung der Daten, die Validierung der Daten und dann die Speicherung der Daten, bevor sie an den nächsten Schritt weitergeleitet werden. Je nachdem, wie viele Daten erfasst werden, kann dies ein zeitaufwendiger Prozess werden, und es besteht immer die Möglichkeit, dass der Prozess aufgrund von Validierungs-, Semantik- oder Verarbeitungsfehlern fehlschlägt. Im Ereignis eines Fehlers müssen die Datenprobleme behoben werden, und dann muss der gesamte Erfassungsvorgang mit den korrigierten Datendateien neu gestartet werden.

Um den Erfassungsvorgang zu überwachen, können Sie mit Experience Platform eine Reihe von Ereignissen abonnieren, die von jedem Prozessschritt veröffentlicht werden, und Sie über den Status der erfassten Daten und eventuelle Fehler informieren.

## Verfügbare Statusbenachrichtigungs-Ereignisse

Im Folgenden finden Sie eine Liste der verfügbaren Statusbenachrichtigungen zur Datenerfassung, die Sie abonnieren können.

>[!NOTE] Es wird nur ein Ereignis-Thema für alle Datenerfassungsbenachrichtigungen bereitgestellt. Zur Unterscheidung zwischen verschiedenen Status kann der Ereignis-Code verwendet werden.

| Plattformdienst | Status | Ereignisbeschreibung | Ereignis-Code |
| ---------------- | ------ | ----------------- | ---------- |
| Dateneingabe | success | Aufschluss - Batch erfolgreich | ing_load_success |
| Dateneingabe | Fehler | Einbettung - Batch fehlgeschlagen | ing_load_failure |
| Echtzeit-Kundenprofil | success | Profil-Dienst - Datenladestapel erfolgreich | ps_load_success |
| Echtzeit-Kundenprofil | Fehler | Profil-Dienst - Datenladestapel fehlgeschlagen | ps_load_failure |
| Identitätsdiagramm | success | Identitätsdiagramm - Datenladestapel erfolgreich | ig_load_success |
| Identitätsdiagramm | Fehler | Identitätsdiagramm - Batch bei Datenladung fehlgeschlagen | ig_load_failure |

## Benachrichtigungsnutzlast-Schema

Das Ereignis für die Datenerfassungsbenachrichtigung ist ein XDM-Schema (Experience Data Model) mit Feldern und Werten, die Details zum Status der erfassten Daten enthalten. Bitte besuchen Sie den öffentlichen XDM GitHub-Repo, um das aktuelle [Benachrichtigungs-Nutzlast-Schema](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)Ansicht.

## Datenaufnahmenstatusbenachrichtigungen abonnieren

Über [Adobe-E/A-Ereignisse](https://www.adobe.io/apis/experienceplatform/events.html)können Sie mehrere Benachrichtigungstypen über Webhooks abonnieren. Weitere Informationen zu Webhooks und zum Abonnieren von Adobe-E/A-Ereignisse mithilfe von Webhooks finden Sie im Handbuch [Einführung zu Adobe-I/O-Ereignisse für Webhooks](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) .

### Neue Integration mit der Adobe I/O-Konsole erstellen

Melden Sie sich bei der [Adobe-E/A-Konsole](https://console.adobe.io/home) an und klicken Sie auf die Registerkarte &quot; *Integrationen* &quot;oder unter &quot;Schneller Beginn&quot;auf Integration **erstellen** . Wenn der Bildschirm &quot; *Integration* &quot;angezeigt wird, klicken Sie auf **Neue Integration** , um eine neue Integration zu erstellen.

![Neue Integration erstellen](../images/quality/subscribe-events/create_integration_start.png)

Der Bildschirm &quot;Neue Integration *erstellen* &quot;wird angezeigt. Wählen Sie &quot;Beinahe-Echtzeit-Ereignis **empfangen**&quot;und klicken Sie dann auf **Weiter**.

![Ereignisse in Echtzeit empfangen](../images/quality/subscribe-events/create_integration_receive_events.png)

Im nächsten Bildschirm finden Sie Optionen zum Erstellen von Integrationen mit verschiedenen Ereignissen, Produkten und Diensten, die Ihrem Unternehmen aufgrund Ihrer Abonnements, Berechtigungen und Berechtigungen zur Verfügung stehen. Wählen Sie für diese Integration **Plattformbenachrichtigungen** unter &quot;Experience Platform&quot;und klicken Sie dann auf **Weiter**.

![Ereignis-Provider auswählen](../images/quality/subscribe-events/create_integration_select_provider.png)

Das Formular *Integrationsdetails* wird angezeigt. Sie müssen einen Namen und eine Beschreibung für die Integration sowie ein Zertifikat mit öffentlichem Schlüssel angeben.

Wenn Sie kein öffentliches Zertifikat haben, können Sie ein Zertifikat im Terminal mit dem folgenden Befehl generieren:

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Nachdem Sie ein Zertifikat generiert haben, ziehen Sie die Datei in das Feld &quot;Zertifikate **mit** öffentlichen Schlüsseln&quot;oder klicken Sie auf &quot;Datei **** auswählen&quot;, um den Dateiordner zu durchsuchen und das Zertifikat direkt auszuwählen.

Nach dem Hinzufügen des Zertifikats wird die Option &quot; *Ereignis-Registrierung* &quot;angezeigt. Klicken Sie auf **Hinzufügen Ereignis Registrierung**.

![Integrationsdetails](../images/quality/subscribe-events/create_integration_details.png)

Das Dialogfeld *Ereignis Registrierungsdetails* wird erweitert und zeigt zusätzliche Steuerelemente an. Hier können Sie Ihre gewünschten Ereignistyp auswählen und Ihren Webhaken registrieren. Geben Sie einen Namen für die Registrierung des Ereignisses, die Webshaken-URL *(optional)* sowie eine kurze Beschreibung ein. Wählen Sie abschließend die Ereignistyp aus, die Sie abonnieren möchten (Benachrichtigung zur Datenaufnahme), und klicken Sie dann auf **Speichern**.

![Ereignisse auswählen](../images/quality/subscribe-events/create_integration_select_event.png)

## Nächste Schritte

Nachdem Sie Ihre E/A-Integration erstellt haben, können Sie alle Benachrichtigungen für diese Integration Ansicht haben. Detaillierte Anweisungen zur Verfolgung Ihrer Ereignis finden Sie im Handbuch [Rückverfolgung von Adobe-E/A-Ereignissen](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) .
