---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zum Datenschutzdienst
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5921f89ce551a4bdec4c5038d579cebd0451f5f2
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Handbuch zur Fehlerbehebung beim Datenschutzdienst

Der Datenschutzdienst für Adobe Experience Platform stellt eine RESTful-API und eine Benutzeroberfläche bereit, die Firmen bei der Verwaltung von Datenschutzanforderungen für Kunden unterstützen. Mit dem Datenschutzdienst können Sie Anfragen zum Zugriff auf und zum Löschen von persönlichen oder privaten Kundendaten stellen, wodurch die automatische Einhaltung der Vorschriften zum Schutz der Privatsphäre in Unternehmen und Rechtsordnungen erleichtert wird.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Datenschutzdienst sowie Informationen zu häufig auftretenden Fehlern in der API.

## Was ist der Unterschied zwischen einer Benutzer- und einer Benutzer-ID, wenn Sie Datenschutzanforderungen in der API machen? {#user-ids}

Um einen neuen Datenschutzauftrag in der API zu erstellen, muss die JSON-Nutzlast der Anforderung ein `users` Array enthalten, das für jeden Benutzer, für den die Datenschutzanforderung gilt, spezifische Informationen Liste. Jedes Element im `users` Array ist ein Objekt, das einen bestimmten Benutzer darstellt, der durch seinen `key` Wert identifiziert wird.

Jedes Benutzerobjekt (oder `key`) enthält wiederum ein eigenes `userIDs` Array. Dieses Array Liste spezifische ID-Werte **für den jeweiligen Benutzer**.

Consider the following example `users` array:

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

Das Array enthält zwei Objekte, die einzelne Benutzer darstellen, die anhand ihrer `key` Werte identifiziert werden (&quot;DavidSmith&quot;und &quot;user12345&quot;). &quot;DavidSmith&quot;hat nur eine ID aufgelistet (ihre E-Mail-Adresse), während &quot;user12345&quot;zwei IDs hat (ihre E-Mail-Adresse und ECID).

Weitere Informationen zum Bereitstellen von Informationen zur Benutzeridentität finden Sie im Handbuch zu [Identitätsdaten für Datenschutzanforderungen](identity-data.md).


## Kann ich den Datenschutzdienst verwenden, um Daten zu bereinigen, die versehentlich an die Plattform gesendet wurden?

Adobe unterstützt nicht die Verwendung des Datenschutzdienstes zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. Der Datenschutzdienst hilft Ihnen bei der Erfüllung Ihrer Pflichten bezüglich des Zugriffs oder Löschens von Anfragen an betroffene Personen (oder Verbraucher). Diese Anfragen sind zeitaufwendig und werden im Zusammenhang mit dem geltenden Datenschutzrecht abgeschlossen. Die Übermittlung von Anfragen, die nicht Gegenstand des Datenschutzes sind, oder von Anfragen zum Löschen von Daten hat Auswirkungen auf alle Kunden des Datenschutzdienstes und die Fähigkeit des Datenschutzdienstes, die entsprechenden gesetzlichen Fristen zu unterstützen.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um PII- oder Datenprobleme zu koordinieren und eine gewisse Anstrengung zu unternehmen.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage oder meines Auftrags?

Sie können Details zu einem bestimmten Auftrag über die Datenschutzdienst-API oder die Benutzeroberfläche abrufen.

### Verwenden der API

Um den Status eines bestimmten Auftrags mithilfe der Datenschutzdienst-API abzurufen, fordern Sie eine Anforderung an den Stamm-Endpunkt (`GET /`) unter Verwendung der Auftrags-ID im Anforderungspfad an. Weitere Informationen finden Sie im Abschnitt zur [Überprüfung des Auftragsstatus](api/privacy-jobs.md#check-the-status-of-a-job) im Developer Guide des Datenschutzdienstes.

### Verwenden der Benutzeroberfläche

Alle aktiven Auftragsanforderungen werden im Widget &quot; **Auftragsanforderungen** &quot;im UI-Dashboard des Datenschutzdienstes aufgelistet. Der Status für jede Auftragsanforderung wird in der Spalte **Status** angezeigt. Weitere Informationen zum Anzeigen von Auftragsanfragen in der Benutzeroberfläche finden Sie im Benutzerhandbuch zum [Datenschutzdienst](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die Datenschutzdienst-API und die Benutzeroberfläche bieten Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Stellen Sie eine Anforderung an den Stamm-Endpunkt (`GET /`) in der Datenschutzdienst-API mit der ID des Auftrags, dessen Ergebnisse Sie im Anforderungspfad herunterladen möchten. Wenn der Auftragsstatus abgeschlossen ist, enthält die API ein `downloadURL` Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt zum [Suchen eines Auftrags nach seiner ID](api/privacy-jobs.md#check-the-status-of-a-job) im Developer Guide des Datenschutzdienstes.

### Verwenden der Benutzeroberfläche

Suchen Sie im Dashboard der Benutzeroberfläche des Datenschutzdienstes den Auftrag, den Sie herunterladen möchten, über das Widget **Auftragsanforderungen** . Klicken Sie auf die ID des Auftrags, um die Seite &quot; _Auftragsdetails_ &quot;zu öffnen. Klicken Sie von hier oben rechts auf **Herunterladen** , um die ZIP-Datei herunterzuladen. Detailliertere Schritte finden Sie im Benutzerhandbuch [zum](ui/user-guide.md) Datenschutzdienst.

## Allgemeine Fehlermeldungen

Die folgende Tabelle enthält einige häufige Fehler im Datenschutzdienst mit Beschreibungen, die zur Lösung der jeweiligen Probleme beitragen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anforderung angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namensraum- und ID-Werte in der Anforderungs-Nutzlast verwenden. Eine genauere Erläuterung finden Sie im Dokument zur [Bereitstellung von Identitätsdaten](./identity-data.md) . |
| Ungültiger Namensraum | Ein bereitgestellter Identitäts-Namensraum für eine Benutzer-ID war ungültig. Eine Liste der zugelassenen Namensraum finden Sie im Abschnitt zu [Namensräumen](./api/appendix.md#standard-namespaces) der Standardidentität im Developer Guide des Datenschutzdienstes. Wenn Sie einen benutzerspezifischen Namensraum verwenden, stellen Sie sicher, dass Sie die ID- `type` Eigenschaft auf &quot;benutzerspezifisch&quot;setzen. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen, einige Daten waren jedoch für die jeweilige Anforderung nicht verfügbar und wurden übersprungen. |
| Die Daten haben nicht das erforderliche Format. | Einer oder mehrere Datenwerte für die angegebene Anwendung wurden falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails. |
| Das IMS-Org wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihr IMS-Org nicht für den Datenschutzdienst bereitgestellt wurde. Wenden Sie sich für weitere Informationen an Ihren Administrator. |
| Zugriff und Berechtigungen sind erforderlich. | Für die Verwendung des Datenschutzdienstes sind Zugriff und Berechtigungen erforderlich. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten ist ein Problem aufgetreten. | Wenn dieser Fehler auftritt, laden Sie die Zugangsdaten erneut hoch und versuchen Sie es erneut. |
| Die Arbeitslast wurde für die aktuelle Dokument-Rate überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Übermittlungsrate und versuchen Sie es erneut. |