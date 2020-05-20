---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ereignisse zur Datenerfassung abonnieren
topic: overview
translation-type: tm+mt
source-git-commit: 1498739d753bdb569e0d3e091e4160bdae40a32f
workflow-type: tm+mt
source-wordcount: '851'
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

## Statusbenachrichtigungen zur Datenaufnahme abonnieren

Über [Adobe-E/A-Ereignisse](https://www.adobe.io/apis/experienceplatform/events.html)können Sie mehrere Benachrichtigungstypen über Webhooks abonnieren. In den folgenden Abschnitten werden die Schritte zum Abonnieren von Plattformbenachrichtigungen für Datenverarbeitungs-Ereignis mit der Adobe Developer Console beschrieben.

### Neues Projekt in der Adobe Developer Console erstellen

Wechseln Sie zur [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

### Hinzufügen Ereignisse der Experience Platform zum Projekt

Nachdem Sie ein neues Projekt erstellt haben, navigieren Sie zum Übersichtsbildschirm dieses Projekts. Klicken Sie von hier auf **[!UICONTROL Hinzufügen Ereignis]**.

![](../images/quality/subscribe-events/add-event-button.png)

Das Dialogfeld _[!UICONTROL Hinzufügen Ereignis]_wird angezeigt. Klicken Sie auf**[!UICONTROL  Erlebnisplattform ]**, um die Liste der verfügbaren Optionen zu filtern, und klicken Sie dann auf**[!UICONTROL  Plattformbenachrichtigungen ]**, bevor Sie auf**[!UICONTROL  Weiter ]**klicken.

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

Nachdem Sie Plattformbenachrichtigungen für Ihr Projekt registriert haben, können Sie Ereignis aus dem Dashboard des Projekts Ansicht haben. Detaillierte Anweisungen zur Verfolgung Ihrer Ereignis finden Sie im Handbuch [Rückverfolgung von Adobe-E/A-Ereignissen](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) .
