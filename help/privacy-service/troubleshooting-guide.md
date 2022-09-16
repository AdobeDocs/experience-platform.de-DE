---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Privacy Services
topic-legacy: troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Privacy Service sowie Informationen zu häufig aufgetretenen Fehlern in der API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# [!DNL Privacy Service] Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Unternehmen Datenschutzanfragen von Kunden verwalten können. Mit [!DNL Privacy Service]können Sie Anfragen zum Zugriff auf und zur Löschung von personenbezogenen oder privaten Kundendaten stellen, was die automatische Einhaltung von organisatorischen und rechtlichen Datenschutzbestimmungen erleichtert.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Privacy Service]sowie Informationen zu häufig aufgetretenen Fehlern in der API.

## Was ist der Unterschied zwischen einer Benutzer- und einer Benutzer-ID bei Datenschutzanfragen in der API? {#user-ids}

Damit ein neuer Datenschutzauftrag in der API ausgeführt werden kann, muss die JSON-Payload der Anfrage eine `users` -Array, das spezifische Informationen für jeden Benutzer auflistet, für den die Datenschutzanfrage gilt. Jedes Element im `users` array ist ein Objekt, das einen bestimmten Benutzer darstellt, der durch seine `key` -Wert.

Jedes Benutzerobjekt (oder `key`) enthält eigene `userIDs` Array. Dieses Array listet bestimmte ID-Werte auf **für einen bestimmten Benutzer**.

Betrachten Sie das folgende Beispiel `users` array:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

Das -Array enthält zwei Objekte, die einzelne Benutzer darstellen, die durch ihre `key` -Werte (&quot;DavidSmith&quot;und &quot;user12345&quot;). &quot;DavidSmith&quot;hat nur eine aufgelistete ID (ihre E-Mail-Adresse), während &quot;user12345&quot;zwei hat (ihre E-Mail-Adresse und ECID).

Weitere Informationen zur Bereitstellung von Benutzeridentitätsdaten finden Sie im Handbuch unter [Identitätsdaten für Datenschutzanfragen](identity-data.md).


## Kann ich [!DNL Privacy Service] , um versehentlich gesendete Daten zu bereinigen [!DNL Platform]?

Adobe unterstützt nicht die Verwendung von [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] unterstützt Sie bei der Erfüllung Ihrer Verpflichtungen bezüglich Zugriffs- oder Löschanfragen von Datensubjekten (oder Verbrauchern). Diese Anfragen sind zeitabhängig und werden im Zusammenhang mit dem geltenden Datenschutzrecht ausgeführt. Die Übermittlung von Anfragen, bei denen es sich nicht um Zugriffs- oder Löschanfragen für Datensubjekte/Verbraucher handelt, wirkt sich auf alle [!DNL Privacy Service] und die Fähigkeit [!DNL Privacy Service] Unterstützung der entsprechenden Fristen.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um Informationen zur Entfernung von personenbezogenen Daten oder Datenproblemen zu erhalten und diese zu koordinieren.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage oder meines Auftrags?

Sie können Details zu einem bestimmten Auftrag abrufen, indem Sie die [!DNL Privacy Service] API oder Benutzeroberfläche.

### Verwenden der API

So rufen Sie den Status eines bestimmten Auftrags mit dem [!DNL Privacy Service] API, stellen Sie eine Anfrage an den Stamm (`GET /`), wobei die Auftrags-ID im Anfragepfad verwendet wird. Weitere Informationen finden Sie im Abschnitt unter [Überprüfen des Auftragsstatus](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service] API-Handbuch.

### Verwenden der Benutzeroberfläche

Alle aktiven Auftragsanfragen werden im **[!UICONTROL Auftragsanforderungen]** Widget im [!DNL Privacy Service] UI-Dashboard. Der Status für jede Auftragsanfrage wird unter dem **[!UICONTROL Status]** Spalte. Weitere Informationen zum Anzeigen von Auftragsanfragen in der Benutzeroberfläche finden Sie unter [Benutzerhandbuch für Privacy Service](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die [!DNL Privacy Service] API und Benutzeroberfläche bieten beide Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Senden Sie eine Anfrage an den Stamm (`GET /`) -Endpunkt im [!DNL Privacy Service] API, unter Verwendung der ID des Auftrags, dessen Ergebnisse Sie im Anfragepfad herunterladen möchten. Wenn der Auftragsstatus abgeschlossen ist, enthält die API eine `downloadURL` -Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt unter [Nachschlagen eines Auftrags anhand seiner ID](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service] API-Handbuch.

### Verwenden der Benutzeroberfläche

Im [!DNL Privacy Service] Dashboard der Benutzeroberfläche, suchen Sie den Auftrag, den Sie herunterladen möchten, über **Auftragsanforderungen** Widget. Wählen Sie die ID des Auftrags aus, um die Seite Auftragsdetails zu öffnen. Wählen Sie von hier aus **Download** oben rechts, um die ZIP-Datei herunterzuladen. Siehe [Benutzerhandbuch für Privacy Service](ui/user-guide.md) für detailliertere Schritte.

## Allgemeine Fehlermeldungen

In der folgenden Tabelle sind einige häufige Fehler in [!DNL Privacy Service]mit Beschreibungen, die bei der Lösung der jeweiligen Probleme helfen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anfrage angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namespace- und ID-Werte in der Anfrage-Payload verwenden. Siehe Dokument unter [Identitätsdaten bereitstellen](./identity-data.md) für eine detailliertere Erläuterung. |
| Ungültiger Namespace | Ein bereitgestellter Identitäts-Namespace für eine Benutzer-ID war ungültig. Siehe Abschnitt zu [Standard-Identitäts-Namespaces](./api/appendix.md#standard-namespaces) im [!DNL Privacy Service] Anhang zum API-Handbuch für eine Liste der zulässigen Namespaces. Wenn Sie einen benutzerdefinierten Namespace verwenden, stellen Sie sicher, dass Sie die ID `type` -Eigenschaft auf &quot;custom&quot;gesetzt. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen, einige Daten waren jedoch für die jeweilige Anfrage nicht anwendbar und wurden übersprungen. |
| Die Daten weisen nicht das erforderliche Format auf. | Einer oder mehrere Datenwerte für die angegebene Anwendung wurden falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails . |
| Die IMS-Organisation wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihre IMS-Organisation nicht für [!DNL Privacy Service]. Wenden Sie sich für weitere Informationen an Ihren Administrator. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um [!DNL Privacy Service]. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten trat ein Problem auf. | Wenn dieser Fehler auftritt, laden Sie die Zugriffsdaten erneut hoch und versuchen Sie es erneut. |
| Die Arbeitslast für das aktuelle Limit der Dokumentrate wurde überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Senderate und versuchen Sie es erneut. |
