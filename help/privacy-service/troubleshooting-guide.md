---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Privacy Services
topic-legacy: troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Privacy Service sowie Informationen zu häufig aufgetretenen Fehlern in der API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# [!DNL Privacy Service] Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] stellt eine RESTful-API und eine Benutzeroberfläche zur Verfügung, die Firmen bei der Verwaltung von Kundendatendatenschutzanforderungen unterstützen. Mit [!DNL Privacy Service], können Sie Anfragen zum Zugriff auf und Löschen privater oder persönlicher Kundendaten stellen und so die automatische Einhaltung der organisatorischen und rechtlichen Datenschutzbestimmungen erleichtern.

Dieses Dokument beantwortet häufig gestellte Fragen zu [!DNL Privacy Service]sowie Informationen zu häufig aufgetretenen Fehlern in der API.

## Was ist der Unterschied zwischen einer Benutzer- und einer Benutzer-ID, wenn Sie Datenschutzanforderungen in der API stellen? {#user-ids}

Um einen neuen Datenschutzauftrag in der API zu erstellen, muss die JSON-Nutzlast der Anforderung eine `users` -Array, das spezifische Informationen für jeden Benutzer Liste, für den die Datenschutzanforderung gilt. Jedes Element im `users` array ist ein Objekt, das einen bestimmten Benutzer darstellt, der durch `key` Wert.

Jedes Benutzerobjekt (oder `key`) enthält eigene `userIDs` Array. Dieses Array Liste spezifische ID-Werte **für einen bestimmten Benutzer**.

Betrachten Sie das folgende Beispiel `users` Array:

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

Das Array enthält zwei Objekte, die einzelne Benutzer darstellen, die durch ihre `key` Werte (&quot;DavidSmith&quot; und &quot;user12345&quot;). &quot;DavidSmith&quot; hat nur eine aufgeführte ID (ihre E-Mail-Adresse), während &quot;user12345&quot; zwei hat (ihre E-Mail-Adresse und ECID).

Weitere Informationen zum Bereitstellen von Informationen zur Benutzeridentität finden Sie im Handbuch zu [Identitätsdaten für Datenschutzanfragen](identity-data.md).


## Kann ich [!DNL Privacy Service] um Daten zu bereinigen, die versehentlich gesendet wurden an [!DNL Platform]?

Adobe unterstützt nicht die Verwendung von [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] wurde entwickelt, um Ihnen bei der Erfüllung Ihrer Verpflichtungen für den Zugriff auf Daten (oder für Verbraucher) oder das Löschen von Anforderungen zu helfen. Diese Anfragen sind zeitaufwendig und werden im Zusammenhang mit dem geltenden Datenschutzrecht ausgeführt. Die Einreichung von Anträgen, bei denen es sich nicht um den Zugriff von Daten/Verbrauchern oder die Löschung von Anträgen handelt, wirkt sich alle auf alle Fälle aus. [!DNL Privacy Service] und die Fähigkeit [!DNL Privacy Service] Unterstützung der angemessenen Fristen für die Rechtsetzung.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um PII- oder Datenprobleme zu koordinieren und zu beheben.

## Wie erhalte ich Informationen zum Status meiner Datenschutzanfrage oder meines Jobs?

Sie können Details zu einem bestimmten Auftrag abrufen, indem Sie [!DNL Privacy Service] API oder Benutzeroberfläche.

### Verwenden der API

So rufen Sie den Status eines bestimmten Auftrags mit der [!DNL Privacy Service] API, eine Anfrage an den Stamm (`GET /`), wobei die Auftrags-ID im Anforderungspfad verwendet wird. Weitere Informationen finden Sie im Abschnitt über [den Status eines Auftrags überprüfen](api/privacy-jobs.md#check-the-status-of-a-job) in [!DNL Privacy Service] API-Handbuch.

### Verwenden der UI

Alle aktiven Auftragsersuchen sind in **[!UICONTROL Auftragsersuchen]** Widget auf [!DNL Privacy Service] UI-Dashboard. Der Status für jede Auftragsanfrage wird angezeigt unter **[!UICONTROL Status]** Spalte. Weitere Informationen zum Anzeigen von Auftragsanfragen in der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die [!DNL Privacy Service] API und Benutzeroberfläche bieten beide Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Anfrage an den Stamm senden (`GET /`) Endpunkt im [!DNL Privacy Service] API, die die ID des Auftrags verwendet, dessen Ergebnisse Sie im Anforderungspfad herunterladen möchten. Wenn der Auftragsstatus abgeschlossen ist, enthält die API eine `downloadURL` Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt über [Job nach ID suchen](api/privacy-jobs.md#check-the-status-of-a-job) in [!DNL Privacy Service] API-Handbuch.

### Verwenden der UI

Auf [!DNL Privacy Service] UI-Dashboard, finden Sie den Auftrag, den Sie herunterladen möchten über **Auftragsersuchen** Widget. Wählen Sie die ID des Auftrags aus, um die Seite Auftragsdetails zu öffnen. Wählen Sie von hier aus **Herunterladen** in der rechten oberen Ecke, um die ZIP-Datei herunterzuladen. Siehe [Privacy Service-Benutzerhandbuch](ui/user-guide.md) für detailliertere Schritte.

## Allgemeine Fehlermeldungen

In der folgenden Tabelle werden einige häufige Fehler in [!DNL Privacy Service], mit Beschreibungen, die zur Lösung der jeweiligen Probleme beitragen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anforderung angegebenen Benutzer-IDs wurden nicht gefunden und übersprungen. Stellen Sie sicher, dass Sie die richtigen Namensraum und ID-Werte in der Anforderungs-Nutzlast verwenden. Dokument anzeigen auf [Identitätsdaten bereitstellen](./identity-data.md) für eine ausführlichere Erläuterung. |
| Ungültiger Namensraum | Ein bereitgestellter Identitäts-Namensraum für eine Benutzer-ID war ungültig. Siehe Abschnitt über [Standard-Identitäts-Namensraum](./api/appendix.md#standard-namespaces) in [!DNL Privacy Service] API-Leitfaden für eine Liste der zugelassenen Namensraum. Wenn Sie einen benutzerspezifischen Namensraum verwenden, stellen Sie sicher, dass Sie die IDs `type` Eigenschaft zu &quot;custom&quot;. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen. Einige Daten waren für die angegebene Anforderung jedoch nicht gültig und wurden übersprungen. |
| Die Daten haben nicht das erforderliche Format. | Mindestens ein Datenwert für die angegebene Anwendung wurde falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails. |
| Die IMS-Organisation wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihr IMS-Org nicht bereitgestellt wurde für [!DNL Privacy Service]. Wenden Sie sich an Ihren Administrator, um weitere Informationen zu erhalten. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um [!DNL Privacy Service]. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten ist ein Problem aufgetreten. | Laden Sie die Zugriffsdaten erneut hoch, wenn dieser Fehler auftritt, und versuchen Sie es erneut. |
| Die Arbeitslast wurde für die aktuelle Dokument-Ratengrenze überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Übermittlungsrate und versuchen Sie es erneut. |
