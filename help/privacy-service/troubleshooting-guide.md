---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zu Privacy Services
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---


# [!DNL Privacy Service] Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Firmen bei der Verwaltung von Datenschutzanforderungen für Kunden unterstützen. Mit [!DNL Privacy Service]dieser Funktion können Sie Anfragen zum Zugriff auf und Löschen von privaten oder persönlichen Kundendaten stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Privacy Service]und Informationen zu häufig aufgetretenen Fehlern in der API.

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


## Kann ich Daten [!DNL Privacy Service] bereinigen, an die ich versehentlich gesendet wurde [!DNL Platform]?

Adobe unterstützt nicht die Verwendung [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] ist so konzipiert, dass Sie Ihren Verpflichtungen bezüglich des Zugriffs oder Löschens von Anfragen durch betroffene Personen (oder Verbraucher) nachkommen können. Diese Anfragen sind zeitaufwendig und werden im Zusammenhang mit dem geltenden Datenschutzrecht abgeschlossen. Die Übermittlung von Anfragen, die nicht Gegenstand des Datenzugriffs oder der Anfrage des Verbrauchers sind, oder Löschungsanfragen hat Auswirkungen auf alle [!DNL Privacy Service] Kunden und die Möglichkeit, die entsprechenden rechtlichen Fristen zu unterstützen, [!DNL Privacy Service] zu haben.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um PII- oder Datenprobleme zu koordinieren und eine gewisse Anstrengung zu unternehmen.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage oder meines Auftrags?

Sie können Details zu einem bestimmten Auftrag über die [!DNL Privacy Service] API oder die Benutzeroberfläche abrufen.

### Verwenden der API

Um den Status eines bestimmten Auftrags mithilfe der [!DNL Privacy Service] API abzurufen, fordern Sie mithilfe der Auftrags-ID im Anforderungspfad eine Anforderung an den Stamm-Endpunkt (`GET /`) an. Weitere Informationen finden Sie im Abschnitt zur [Überprüfung des Auftragsstatus](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service] Entwicklerhandbuch.

### Verwenden der UI

Alle aktiven Auftragsanforderungen werden im Widget &quot; **[!UICONTROL Auftragsanforderungen]** &quot;im Dashboard der [!DNL Privacy Service] Benutzeroberfläche aufgelistet. Der Status für jede Auftragsanforderung wird in der Spalte **[!UICONTROL Status]** angezeigt. Weitere Informationen zum Anzeigen von Auftragsanforderungen in der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Sowohl die [!DNL Privacy Service] API als auch die Benutzeroberfläche bieten Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Fordern Sie mithilfe der ID des Auftrags, dessen Ergebnisse Sie im Anforderungspfad herunterladen möchten, eine Anforderung an den Stamm-Endpunkt (`GET /`) in der [!DNL Privacy Service] API an. Wenn der Auftragsstatus abgeschlossen ist, enthält die API ein `downloadURL` Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt zum [Suchen eines Auftrags nach seiner ID](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service] Entwicklerhandbuch.

### Verwenden der UI

Suchen Sie im [!DNL Privacy Service] UI-Dashboard den Auftrag, den Sie herunterladen möchten, im Widget **Auftragsanforderungen** . Klicken Sie auf die ID des Auftrags, um die Seite &quot; _Auftragsdetails_ &quot;zu öffnen. Klicken Sie von hier oben rechts auf **Herunterladen** , um die ZIP-Datei herunterzuladen. Detailliertere Anweisungen finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md) .

## Allgemeine Fehlermeldungen

Die folgende Tabelle enthält einige häufige Fehler in [!DNL Privacy Service]mit Beschreibungen, die bei der Lösung der jeweiligen Probleme helfen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anforderung angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namensraum- und ID-Werte in der Anforderungs-Nutzlast verwenden. Eine genauere Erläuterung finden Sie im Dokument zur [Bereitstellung von Identitätsdaten](./identity-data.md) . |
| Ungültiger Namensraum | Ein bereitgestellter Identitäts-Namensraum für eine Benutzer-ID war ungültig. Eine Liste der zulässigen Namensraum finden Sie im Abschnitt zu [Namensräumen](./api/appendix.md#standard-namespaces) der Standardidentität im [!DNL Privacy Service] Entwicklerhandbuch. Wenn Sie einen benutzerspezifischen Namensraum verwenden, stellen Sie sicher, dass Sie die ID- `type` Eigenschaft auf &quot;benutzerspezifisch&quot;setzen. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen, einige Daten waren jedoch für die jeweilige Anforderung nicht verfügbar und wurden übersprungen. |
| Die Daten haben nicht das erforderliche Format. | Einer oder mehrere Datenwerte für die angegebene Anwendung wurden falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails. |
| Das IMS-Org wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihr IMS-Org nicht bereitgestellt wurde [!DNL Privacy Service]. Wenden Sie sich für weitere Informationen an Ihren Administrator. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um verwendet werden zu können [!DNL Privacy Service]. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten ist ein Problem aufgetreten. | Wenn dieser Fehler auftritt, laden Sie die Zugangsdaten erneut hoch und versuchen Sie es erneut. |
| Die Arbeitslast wurde für die aktuelle Dokument-Rate überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Übermittlungsrate und versuchen Sie es erneut. |