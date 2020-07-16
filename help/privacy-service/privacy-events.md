---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenschutzereignisse abonnieren
topic: privacy events
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 30%

---


# Abonnieren [!DNL Privacy Events]

[!DNL Privacy Events] sind Meldungen, die von der Adobe Experience Platform bereitgestellt werden [!DNL Privacy Service], die Adobe-I/O-Ereignis nutzen, die an einen konfigurierten WebHook gesendet werden, um eine effiziente Auftragsautomatisierung zu ermöglichen. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached.

Aktuell gibt es vier Arten von Benachrichtigungen im Lebenszyklus der Anfragen von Datenschutzaufträgen:

| Typ | Beschreibung |
--- | ---
| Auftrag abgeschlossen | All [!DNL Experience Cloud] solutions have reported back and the overall or global status of the job has been marked as complete. |
| Auftragsfehler | Bei einer oder mehreren Lösungen wurde bei der Verarbeitung der Anfrage ein Fehler gemeldet. |
| Produkt abgeschlossen | Eine der Lösungen, die mit diesem Auftrag verbunden ist, hat ihren Auftrag abgeschlossen. |
| Produktfehler | Eine der Lösungen hat bei der Verarbeitung der Anfrage einen Fehler gemeldet. |

This document provides steps for setting up an integration for [!DNL Privacy Service] notifications within Adobe I/O. For a high-level overview of [!DNL Privacy Service] and its features, see the [Privacy Service overview](home.md).

## Erste Schritte

Dieses Tutorial verwendet **ngrok**, ein Software-Produkt, das lokale Server über sichere Tunnel dem öffentlichen Internet zugänglich macht. Bitte [installieren Sie ngrok](https://ngrok.com/download), bevor Sie mit diesem Tutorial beginnen, um auf Ihrem lokalen Computer einen Webhook zu erstellen. This guide also requires you to have a GIT repository downloaded that contains a simple [Node.js](https://nodejs.org/) server.

## Lokalen Server erstellen

Ihr Node.js-Server muss einen `challenge`-Parameter zurückgeben, der von einer Anfrage an den Stammendpunkt (`/`) gesendet wird. Richten Sie Ihre `index.js`-Datei mit folgendem JavaScript ein, um dies zu erreichen:

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

Navigieren Sie mit der Befehlszeile zum Stammverzeichnis Ihres Node.js-Servers. Geben Sie dann die folgenden Befehle ein:

1. `npm install`
1. `npm start`

Diese Befehle installieren alle Abhängigkeiten und initialisieren den Server. Bei erfolgreichem Abschluss sehen Sie, dass Ihr Server unter http://localhost:3000/ ausgeführt wird.

## Webhook erstellen mit ngrok

Öffnen Sie ein neues Befehlszeilenfenster und navigieren Sie zu dem Ordner, in dem Sie ngrok zuvor installiert haben. Geben Sie von hier aus den folgenden Befehl ein:

```shell
./ngrok http -bind-tls=true 3000
```

Eine erfolgreiche Ausgabe sieht etwa wie folgt aus:

![ngrok-Ausgabe](images/privacy-events/ngrok-output.png)

Notieren Sie sich die `Forwarding`-URL (`https://212d6cd2.ngrok.io`), da diese dazu dient, Ihren Webhook im nächsten Schritt zu identifizieren.

## Neues Projekt in der Adobe Developer Console erstellen

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) and sign in with your Adobe ID. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

## Ereignisse zum Schutz der Privatsphäre im Projekt Hinzufügen

Nachdem Sie mit der Erstellung eines neuen Projekts in der Konsole fertig sind, klicken Sie im Bildschirm &quot; **[!UICONTROL Projektübersicht]** &quot;auf _Hinzufügen Ereignis_ .

![](./images/privacy-events/add-event-button.png)

The _Add events_ dialog appears. Wählen Sie **[!UICONTROL Experience Cloud]** aus, um die Liste eines verfügbaren Ereignistyps zu filtern, und wählen Sie dann die Ereignis **[!UICONTROL des]** Privacy Service aus, bevor Sie auf **[!UICONTROL Weiter]** klicken.

![](./images/privacy-events/add-privacy-events.png)

Das Dialogfeld &quot;Registrierung _des Ereignisses_ konfigurieren&quot;wird angezeigt. Wählen Sie die Ereignis aus, die Sie erhalten möchten, indem Sie die entsprechenden Kontrollkästchen aktivieren. Ereignis, die Sie auswählen, werden in der linken Spalte unter &quot; _[!UICONTROL Abonnierte Ereignis]_&quot;angezeigt. When finished, click**[!UICONTROL  Next ]**.

![](./images/privacy-events/choose-subscriptions.png)

Im nächsten Bildschirm werden Sie aufgefordert, einen öffentlichen Schlüssel für die Registrierung des Ereignisses bereitzustellen. Sie haben die Möglichkeit, automatisch ein Schlüsselpaar zu erstellen oder einen eigenen öffentlichen Schlüssel hochzuladen, der im Terminal generiert wurde.

Für diese Übung wird die erste Option verwendet. Klicken Sie auf das Optionsfeld für **[!UICONTROL Generate a key pair]** und dann unten rechts auf die Schaltfläche **[!UICONTROL Generate keypair]** .

![](./images/privacy-events/generate-key-value.png)

Wenn das Schlüsselpaar generiert wird, wird es automatisch vom Browser heruntergeladen. Sie müssen diese Datei selbst speichern, da sie nicht in der Developer Console beibehalten wird.

Im nächsten Bildschirm können Sie die Details des neu generierten Schlüsselpaars überprüfen. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![](./images/privacy-events/keypair-generated.png)

Geben Sie im nächsten Bildschirm einen Namen und eine Beschreibung für die Registrierung des Ereignisses ein. Best Practice ist, einen eindeutigen, leicht identifizierbaren Namen zu erstellen, um diese Ereignis-Registrierung von anderen im selben Projekt zu unterscheiden.

![](./images/privacy-events/event-details.png)

Weiter unten auf dem gleichen Bildschirm stehen Ihnen zwei Optionen zur Konfiguration des Empfangs von Ereignissen zur Verfügung. Wählen Sie **[!UICONTROL WebHaken]** und geben Sie die `Forwarding` URL für den oben erstellten ngrok-Webhaken unter der _[!UICONTROL WebHook-URL]_ein. Wählen Sie dann den gewünschten Versand-Stil (Einzel- oder Stapelform), bevor Sie auf Konfigurierte Ereignis****speichern klicken, um die Ereignis-Registrierung abzuschließen.

![](./images/privacy-events/webhook-details.png)

Die Detailseite für Ihr Projekt wird erneut angezeigt und [!DNL Privacy Events] wird unter den _[!UICONTROL Ereignissen]_im linken Navigationsbereich angezeigt.

## Ereignisdaten anzeigen

Nachdem Sie sich bei [!DNL Privacy Events] Ihrem Projekt registriert haben und Datenschutzaufträge verarbeitet wurden, können Sie alle eingegangenen Benachrichtigungen für diese Registrierung Ansicht haben. Wählen Sie auf der Registerkarte &quot; **[!UICONTROL Projekte]** &quot;in der Developer Console Ihr Projekt aus der Liste aus, um die Seite &quot; _Produktübersicht_ &quot;zu öffnen. Wählen Sie von hier aus im linken Navigationsbereich die Option **[!UICONTROL Datenschutz-Ereignisse]** .

![](./images/privacy-events/events-left-nav.png)

The _Registration Details_ tab appears, allowing you to view more information about the registration, edit its configuration, or view the actual events that were received since activating your webhook.

![](./images/privacy-events/registration-details.png)

Klicken Sie auf die Registerkarte **[!UICONTROL Debug-Verfolgung]** , um eine Liste der empfangenen Ereignis Ansicht. Klicken Sie auf ein aufgelistetes Ereignis, um dessen Details Ansicht.

![](images/privacy-events/debug-tracing.png)

Der Abschnitt _[!UICONTROL Payload]_enthält Details zum ausgewählten Ereignis, einschließlich dessen Ereignistyp (`com.adobe.platform.gdpr.productcomplete`), wie im Beispiel oben hervorgehoben.

## Nächste Schritte

Sie können die oben beschriebenen Schritte bei Bedarf wiederholen, um für verschiedene Webhook-Adressen neue Integrationen hinzuzufügen.