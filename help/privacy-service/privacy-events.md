---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ereignisse zum Schutz der Privatsphäre abonnieren
topic: privacy events
translation-type: tm+mt
source-git-commit: ab29c7771122267634dea24582b07f605abd7ed8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Ereignisse zum Schutz der Privatsphäre abonnieren

Datenschutz-Ereignisse sind vom Adobe Experience Platform Privacy Service bereitgestellte Meldungen, die Adobe-I/O-Ereignis nutzen, die an einen konfigurierten Webhaken gesendet werden, um eine effiziente Auftragsabwicklungsautomatisierung zu ermöglichen. Sie verringern oder beseitigen die Notwendigkeit, die Datenschutzdienst-API abzufragen, um zu prüfen, ob ein Auftrag abgeschlossen ist oder ein bestimmter Meilenstein innerhalb eines Workflows erreicht wurde.

Derzeit gibt es vier Arten von Benachrichtigungen zum Lebenszyklus von Datenschutzaufforderungen:

| Typ | Beschreibung |
--- | ---
| Auftragsabschluss | Alle Experience Cloud-Lösungen wurden in Berichten zurückgegeben und der Gesamtstatus des Auftrags bzw. der globale Status wurde als abgeschlossen markiert. |
| Auftragsfehler | Bei einer oder mehreren Lösungen wurde während der Verarbeitung der Anforderung ein Fehler gemeldet. |
| Produktbeendigung | Eine der Lösungen, die mit diesem Auftrag verbunden ist, hat seine Arbeit abgeschlossen. |
| Produktfehler | Eine der Lösungen meldete einen Fehler bei der Verarbeitung der Anforderung. |

In diesem Dokument wird beschrieben, wie Sie eine Integration für Datenschutzdienstbenachrichtigungen in Adobe I/O einrichten. Eine allgemeine Übersicht über den Datenschutzdienst und dessen Funktionen finden Sie in der Übersicht über den [Datenschutzdienst](home.md).

## Erste Schritte

Dieses Tutorial verwendet **ngrok**, ein Softwareprodukt, das lokale Server über sichere Tunnel dem öffentlichen Internet zugänglich macht. Bitte [installieren Sie ngrok](https://ngrok.com/download) , bevor Sie dieses Tutorial starten, um weiter zu folgen und einen Webhaken zu Ihrem lokalen Computer zu erstellen. Für dieses Handbuch müssen Sie außerdem ein GIT-Repository herunterladen, das einen einfachen [Node.js](https://nodejs.org/) -Server enthält.

## Lokalen Server erstellen

Ihr Node.js-Server muss einen `challenge` Parameter zurückgeben, der von einer Anforderung an den Stamm-Endpunkt (`/`) gesendet wird. Richten Sie Ihre `index.js` Datei mit folgendem JavaScript ein, um dies zu erreichen:

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

Navigieren Sie mit der Befehlszeile zum Stammverzeichnis des Node.js-Servers. Geben Sie dann die folgenden Befehle ein:

1. `npm install`
1. `npm start`

Diese Befehle installieren alle Abhängigkeiten und initialisieren den Server. Bei erfolgreichem Abschluss finden Sie Ihren Server unter http://localhost:3000/.

## Erstellen eines Webhofs mit ngrok

Öffnen Sie ein neues Befehlszeilenfenster und navigieren Sie zu dem Ordner, in dem Sie ngrok zuvor installiert haben. Geben Sie von hier aus den folgenden Befehl ein:

```shell
./ngrok http -bind-tls=true 3000
```

Eine erfolgreiche Ausgabe sieht wie folgt aus:

![ngrok-Ausgabe](images/privacy-events/ngrok-output.png)

Notieren Sie sich die `Forwarding` URL (`https://212d6cd2.ngrok.io`), da diese verwendet wird, um Ihren Webshaken im nächsten Schritt zu identifizieren.

## Neues Projekt in der Adobe Developer Console erstellen

Wechseln Sie zur [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

## Ereignisse zum Schutz der Privatsphäre im Projekt Hinzufügen

Nachdem Sie mit der Erstellung eines neuen Projekts in der Konsole fertig sind, klicken Sie im Bildschirm &quot; **[!UICONTROL Projektübersicht]** &quot;auf _Hinzufügen Ereignis_ .

![](./images/privacy-events/add-event-button.png)

Das Dialogfeld _Hinzufügen Ereignis_ wird angezeigt. Wählen Sie **[!UICONTROL Experience Cloud]** , um die Liste der verfügbaren Ereignistyp zu filtern, und wählen Sie dann die Ereignis **[!UICONTROL des]** Datenschutzdienstes, bevor Sie auf **[!UICONTROL Weiter]** klicken.

![](./images/privacy-events/add-privacy-events.png)

Das Dialogfeld &quot;Registrierung _des Ereignisses_ konfigurieren&quot;wird angezeigt. Wählen Sie die Ereignis aus, die Sie erhalten möchten, indem Sie die entsprechenden Kontrollkästchen aktivieren. Ereignis, die Sie auswählen, werden in der linken Spalte unter &quot; _[!UICONTROL Abonnierte Ereignis]_&quot;angezeigt. Klicken Sie abschließend auf**[!UICONTROL  Weiter ]**.

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

Die Detailseite für Ihr Projekt wird erneut angezeigt, wobei die Ereignisse zum Datenschutz unter den _[!UICONTROL Ereignissen]_im linken Navigationsbereich angezeigt werden.

## Ansicht Ereignis-Daten

Sobald Sie die Ereignisse zum Datenschutz bei Ihrem Projekt registriert haben und Datenschutzaufträge verarbeitet wurden, können Sie alle eingegangenen Benachrichtigungen für diese Registrierung Ansicht haben. Wählen Sie auf der Registerkarte &quot; **[!UICONTROL Projekte]** &quot;in der Developer Console Ihr Projekt aus der Liste aus, um die Seite &quot; _Produktübersicht_ &quot;zu öffnen. Wählen Sie von hier aus im linken Navigationsbereich die Option **[!UICONTROL Datenschutz-Ereignisse]** .

![](./images/privacy-events/events-left-nav.png)

Die Registerkarte &quot; _Registrierungsdetails_ &quot;wird angezeigt, auf der Sie weitere Informationen zur Registrierung Ansicht, die Konfiguration bearbeiten oder die Ereignis, die Sie seit der Aktivierung Ihres Webhofs erhalten haben, in Ansicht setzen können.

![](./images/privacy-events/registration-details.png)

Klicken Sie auf die Registerkarte **[!UICONTROL Debug-Verfolgung]** , um eine Liste der empfangenen Ereignis Ansicht. Klicken Sie auf ein aufgelistetes Ereignis, um dessen Details Ansicht.

![](images/privacy-events/debug-tracing.png)

Der Abschnitt _[!UICONTROL Nutzlast]_enthält Details zum ausgewählten Ereignis, einschließlich dessen Ereignistyp (`com.adobe.platform.gdpr.productcomplete`), wie im Beispiel oben hervorgehoben.

## Nächste Schritte

Sie können die oben genannten Schritte wiederholen, um nach Bedarf neue Integrationen für verschiedene Webgehaken-Adressen hinzuzufügen.