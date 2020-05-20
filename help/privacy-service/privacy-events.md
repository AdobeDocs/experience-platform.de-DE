---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ereignisse zum Schutz der Privatsphäre abonnieren
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60
workflow-type: tm+mt
source-wordcount: '778'
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

Dieses Tutorial verwendet **ngrok**, ein Softwareprodukt, das lokale Server über sichere Tunnel dem öffentlichen Internet zugänglich macht. Bitte [installieren Sie ngrok](https://ngrok.com/download) , bevor Sie dieses Tutorial starten, um weiter zu folgen und einen Webhaken zu Ihrem lokalen Computer zu erstellen. Für dieses Handbuch müssen Sie außerdem ein GIT-Repository herunterladen, das einen einfachen Server enthält, der in [Node.js](https://nodejs.org/)geschrieben ist.

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

Geben Sie in demselben Ordner und in einem neuen Befehlszeilenfenster den folgenden Befehl ein:

```shell
ngrok http -bind-tls=true 3000
```

Eine erfolgreiche Ausgabe sieht wie folgt aus:

![ngrok-Ausgabe](images/privacy-events/ngrok-output.png)

Notieren Sie sich die `Forwarding` URL (`https://e142b577.ngrok.io`), da diese verwendet wird, um Ihren Webshaken im nächsten Schritt zu identifizieren.

## Neue Integration mit der Adobe I/O-Konsole erstellen

Melden Sie sich bei der [Adobe-E/A-Konsole](https://console.adobe.io) an und klicken Sie auf die Registerkarte **Integrationen** . Das Fenster _Integrationen_ wird angezeigt. Klicken Sie von hier auf **Neue Integration**.

![Ansicht-Integrationen in der Adobe I/O-Konsole](images/privacy-events/integrations.png)

Das Fenster *Neue Integration* erstellen wird angezeigt. Wählen Sie &quot;Beinahe-Echtzeit-Ereignis **empfangen**&quot;und klicken Sie dann auf **Weiter**.

![Neue Integration erstellen](images/privacy-events/new-integration.png)

Im nächsten Bildschirm finden Sie Optionen zum Erstellen von Integrationen mit verschiedenen Ereignissen, Produkten und Diensten, die Ihrem Unternehmen aufgrund Ihrer Abonnements, Berechtigungen und Berechtigungen zur Verfügung stehen. Wählen Sie für diese Integration die Ereignisse **des** Datenschutzdienstes und klicken Sie dann auf **Weiter**.

![Datenschutzeinstellungen auswählen](images/privacy-events/privacy-events.png)

Das Formular *Integrationsdetails* wird angezeigt. Sie müssen einen Namen und eine Beschreibung für die Integration sowie ein Zertifikat mit öffentlichem Schlüssel angeben.

![Integrationsdetails](images/privacy-events/integration-details.png)

Wenn Sie kein öffentliches Zertifikat haben, können Sie ein Zertifikat mit dem folgenden Befehl &quot;Terminal&quot;generieren:

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Nachdem Sie ein Zertifikat generiert haben, ziehen Sie die Datei in das Feld &quot;Zertifikate **mit** öffentlichen Schlüsseln&quot;oder klicken Sie auf &quot;Datei **** auswählen&quot;, um den Dateiordner zu durchsuchen und das Zertifikat direkt auszuwählen.

Nach dem Hinzufügen des Zertifikats wird die Option &quot; *Ereignis-Registrierung* &quot;angezeigt. Klicken Sie auf **Hinzufügen Ereignis Registrierung**.

![Hinzufügen Ereignis-Registrierung](images/privacy-events/add-event-registration.png)

Das Dialogfeld wird erweitert, um zusätzliche Steuerelemente anzuzeigen. Hier können Sie Ihre gewünschten Ereignistyp auswählen und Ihren Webhaken registrieren. Geben Sie einen Namen für die Registrierung des Ereignisses, die Webshaken-URL (die `Forwarding` Adresse, die Sie beim [Erstellen des Webhofs](#create-a-webhook-using-ngrok)zurückgegeben haben) sowie eine kurze Beschreibung ein. Wählen Sie abschließend die Ereignistyp aus, die Sie abonnieren möchten, und klicken Sie dann auf **Speichern**.

![Ereignis-Registrierungsformular](images/privacy-events/event-registration-form.png)

Nachdem das Ereignis-Registrierungsformular ausgefüllt wurde, klicken Sie auf Integration **erstellen** und die E/A-Integration ist abgeschlossen.

![Integration erstellen](images/privacy-events/create-integration.png)

## Ansicht Ereignis-Daten

Nachdem Sie Ihre E/A-Integrations- und Datenschutzaufträge erstellt haben, können Sie alle Benachrichtigungen für diese Integration Ansicht haben. Navigieren Sie auf der Registerkarte **Integrationen** in der E/A-Konsole zu Ihrer Integration und klicken Sie auf **Ansicht**.

![Integration von Ansichten](images/privacy-events/view-integration.png)

Die Detailseite für die Integration wird angezeigt. Klicken Sie auf **Ereignis** , um die Ereignis-Registrierungen für die Integration Ansicht. Suchen Sie nach der Registrierung für die Ereignisse zum Datenschutz und klicken Sie auf **Ansicht**.

![Registrierung für Ansicht Ereignis](images/privacy-events/view-registration.png)

Das Fenster &quot; *Ereignis-Details* &quot;wird angezeigt, in dem Sie weitere Informationen zur Registrierung Ansicht, die Konfiguration bearbeiten oder die Ereignis, die Sie seit der Aktivierung Ihres Webhofs erhalten haben, Ansicht vornehmen können. Sie können die Details des Ereignisses Ansicht und zur **Debug-Ablaufverfolgung** navigieren.

![Debugging-Verfolgung](images/privacy-events/debug-tracing.png)

Der Abschnitt **Nutzlast** enthält Details zum ausgewählten Ereignis, einschließlich dessen Ereignistyp (`"com.adobe.platform.gdpr.productcomplete"`), wie im Beispiel oben hervorgehoben.

## Nächste Schritte

Sie können die oben genannten Schritte wiederholen, um nach Bedarf neue Integrationen für verschiedene Webgehaken-Adressen hinzuzufügen.