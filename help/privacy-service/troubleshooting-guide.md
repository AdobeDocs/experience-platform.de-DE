---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Privacy Services
topic-legacy: troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Privacy Service sowie Informationen zu häufig aufgetretenen Fehlern in der API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# [!DNL Privacy Service] Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] stellt eine RESTful-API und eine Benutzeroberfläche bereit, die Firmen bei der Verwaltung von Datenschutzanforderungen für Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff auf und Löschen von privaten oder persönlichen Kundendaten einreichen, was die automatische Einhaltung der Vorschriften zum Schutz der Privatsphäre in Unternehmen und Rechtsordnungen erleichtert.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Privacy Service] sowie Informationen zu häufig aufgetretenen Fehlern in der API.

## Was ist der Unterschied zwischen einer Benutzer- und einer Benutzer-ID, wenn Sie Datenschutzanforderungen in der API machen? {#user-ids}

Um einen neuen Datenschutzauftrag in der API zu erstellen, muss die JSON-Nutzlast der Anforderung ein `users`-Array enthalten, das für jeden Benutzer, für den die Datenschutzanforderung gilt, spezifische Informationen Liste. Jedes Element im Array `users` ist ein Objekt, das einen bestimmten Benutzer darstellt, der durch seinen `key`-Wert identifiziert wird.

Jedes Benutzerobjekt (oder `key`) enthält wiederum ein eigenes `userIDs`-Array. Dieses Array Liste spezifische ID-Werte **für den jeweiligen Benutzer**.

Betrachten Sie das folgende Beispiel `users`-Array:

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

Das Array enthält zwei Objekte, die einzelne Benutzer darstellen, die mit ihren `key`-Werten (&quot;DavidSmith&quot;und &quot;user12345&quot;) identifiziert werden. &quot;DavidSmith&quot;hat nur eine ID aufgelistet (ihre E-Mail-Adresse), während &quot;user12345&quot;zwei IDs hat (ihre E-Mail-Adresse und ECID).

Weitere Informationen zum Bereitstellen von Informationen zur Benutzeridentität finden Sie im Handbuch [Identitätsdaten für Datenschutzanforderungen](identity-data.md).


## Kann ich [!DNL Privacy Service] verwenden, um Daten zu bereinigen, die versehentlich an [!DNL Platform] gesendet wurden?

Adobe unterstützt nicht die Verwendung von [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] ist so konzipiert, dass Sie Ihren Verpflichtungen bezüglich des Zugriffs oder Löschens von Anfragen durch betroffene Personen (oder Verbraucher) nachkommen können. Diese Anfragen sind zeitaufwendig und werden im Zusammenhang mit dem geltenden Datenschutzrecht abgeschlossen. Die Übermittlung von Anfragen, die nicht Gegenstand/Verbraucher sind, oder Löschanforderungen hat Auswirkungen auf alle [!DNL Privacy Service] Kunden und die Fähigkeit von [!DNL Privacy Service], die entsprechenden gesetzlichen Fristen zu unterstützen.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um PII- oder Datenprobleme zu koordinieren und eine gewisse Anstrengung zu unternehmen.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage oder meines Auftrags?

Sie können Details zu einem bestimmten Auftrag über die [!DNL Privacy Service]-API oder -Benutzeroberfläche abrufen.

### Verwenden der API

Um den Status eines bestimmten Auftrags mithilfe der API abzurufen, fordern Sie eine Anforderung an den Stammendpunkt (`GET /`) unter Verwendung der Auftragskennung im Anforderungspfad an. [!DNL Privacy Service] Weitere Informationen finden Sie im Abschnitt [Überprüfen des Status eines Auftrags](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service]-Entwicklerhandbuch.

### Verwenden der UI

Alle aktiven Auftragsanforderungen werden im Widget **[!UICONTROL Auftragsanforderungen]** im Dashboard [!DNL Privacy Service] der Benutzeroberfläche aufgelistet. Der Status für jede Auftragsanforderung wird unter der Spalte **[!UICONTROL Status]** angezeigt. Weitere Informationen zum Anzeigen von Auftragsanforderungen in der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die API und die Benutzeroberfläche von [!DNL Privacy Service] bieten Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Stellen Sie eine Anforderung an den Stammendpunkt (`GET /`) in der [!DNL Privacy Service]-API mit der ID des Auftrags, dessen Ergebnisse Sie im Anforderungspfad herunterladen möchten. Wenn der Auftragsstatus abgeschlossen ist, enthält die API das Attribut `downloadURL` im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt [Einen Auftrag nach der ID](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service]-Entwicklerhandbuch suchen.

### Verwenden der UI

Suchen Sie im Dashboard [!DNL Privacy Service] der Benutzeroberfläche den Auftrag, den Sie herunterladen möchten, im Widget **Anforderungen für Aufträge**. Wählen Sie die ID des Auftrags aus, um die Seite &quot;Auftragsdetails&quot;zu öffnen. Wählen Sie **Download** in der oberen rechten Ecke aus, um die ZIP-Datei herunterzuladen. Detailliertere Anweisungen finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Allgemeine Fehlermeldungen

In der folgenden Tabelle sind einige häufige Fehler in [!DNL Privacy Service] mit Beschreibungen aufgeführt, die bei der Lösung der jeweiligen Probleme hilfreich sind.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anforderung angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namensraum- und ID-Werte in der Anforderungs-Nutzlast verwenden. Weitere Informationen finden Sie im Dokument [Identitätsdaten](./identity-data.md) bereitstellen. |
| Ungültiger Namensraum | Ein bereitgestellter Identitäts-Namensraum für eine Benutzer-ID war ungültig. Eine Liste der zulässigen Namensraum finden Sie im Abschnitt [Standardidentitäts-Namensraum](./api/appendix.md#standard-namespaces) im [!DNL Privacy Service] Entwicklerhandbuch. Wenn Sie einen benutzerspezifischen Namensraum verwenden, stellen Sie sicher, dass Sie die `type`-Eigenschaft der ID auf &quot;custom&quot;setzen. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen, einige Daten waren jedoch für die jeweilige Anforderung nicht verfügbar und wurden übersprungen. |
| Die Daten haben nicht das erforderliche Format. | Einer oder mehrere Datenwerte für die angegebene Anwendung wurden falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails. |
| Das IMS-Org wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihr IMS-Org nicht für [!DNL Privacy Service] bereitgestellt wurde. Wenden Sie sich für weitere Informationen an Ihren Administrator. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um [!DNL Privacy Service] verwenden zu können. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten ist ein Problem aufgetreten. | Wenn dieser Fehler auftritt, laden Sie die Zugangsdaten erneut hoch und versuchen Sie es erneut. |
| Die Arbeitslast wurde für die aktuelle Dokument-Rate überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Übermittlungsrate und versuchen Sie es erneut. |
