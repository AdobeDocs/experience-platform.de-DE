---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Privacy Services
topic-legacy: troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Privacy Service sowie Informationen zu häufig aufgetretenen Fehlern in der API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# [!DNL Privacy Service] Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Unternehmen bei der Verwaltung von Datenschutzanfragen von Kunden unterstützt. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff auf und zur Löschung von privaten oder persönlichen Kundendaten einreichen, was die automatische Einhaltung von organisatorischen und rechtlichen Datenschutzbestimmungen erleichtert.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Privacy Service] sowie Informationen zu häufig aufgetretenen Fehlern in der API.

## Was ist der Unterschied zwischen einer Benutzer- und einer Benutzer-ID bei Datenschutzanfragen in der API? {#user-ids}

Damit ein neuer Datenschutzauftrag in der API ausgeführt werden kann, muss die JSON-Payload der Anfrage ein `users`-Array enthalten, das für jeden Benutzer, für den die Datenschutzanfrage gilt, spezifische Informationen auflistet. Jedes Element im Array `users` ist ein Objekt, das einen bestimmten Benutzer darstellt, der durch seinen `key` -Wert identifiziert wird.

Jedes Benutzerobjekt (oder `key`) enthält ein eigenes `userIDs`-Array. Dieses Array listet bestimmte ID-Werte **für diesen bestimmten Benutzer** auf.

Betrachten Sie das folgende Beispiel `users` -Array:

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

Das Array enthält zwei Objekte, die einzelne Benutzer darstellen, die durch ihre `key`-Werte (&quot;DavidSmith&quot;und &quot;user12345&quot;) identifiziert werden. &quot;DavidSmith&quot;hat nur eine aufgelistete ID (ihre E-Mail-Adresse), während &quot;user12345&quot;zwei hat (ihre E-Mail-Adresse und ECID).

Weitere Informationen zur Bereitstellung von Informationen zur Benutzeridentität finden Sie im Handbuch zu [Identitätsdaten für Datenschutzanfragen](identity-data.md).


## Kann ich [!DNL Privacy Service] verwenden, um Daten zu bereinigen, die versehentlich an [!DNL Platform] gesendet wurden?

Adobe unterstützt nicht die Verwendung von [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] unterstützt Sie bei der Erfüllung Ihrer Verpflichtungen bezüglich Zugriffs- oder Löschanfragen von Datensubjekten (oder Verbrauchern). Diese Anfragen sind zeitabhängig und werden im Zusammenhang mit dem geltenden Datenschutzrecht ausgeführt. Die Übermittlung von Anfragen, bei denen es sich nicht um Zugriffs- oder Löschanfragen für Datensubjekte/Verbraucher handelt, wirkt sich auf alle [!DNL Privacy Service]-Kunden aus und die Fähigkeit von [!DNL Privacy Service], die entsprechenden gesetzlichen Zeitpläne zu unterstützen.

Wenden Sie sich an Ihren Kundenbetreuer (CDM), um Informationen zur Entfernung von personenbezogenen Daten oder Datenproblemen zu erhalten und diese zu koordinieren.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage oder meines Auftrags?

Sie können Details zu einem bestimmten Auftrag über die [!DNL Privacy Service] -API oder -Benutzeroberfläche abrufen.

### Verwenden der API

Um den Status eines bestimmten Auftrags mithilfe der API [!DNL Privacy Service] abzurufen, stellen Sie eine Anfrage an den Root-Endpunkt (`GET /`) unter Verwendung der Auftrags-ID im Anfragepfad. Weitere Informationen finden Sie im Abschnitt [Überprüfen des Status eines Auftrags](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service]-Entwicklerhandbuch.

### Verwenden der UI

Alle aktiven Auftragsanfragen werden im Widget **[!UICONTROL Vorgangsanforderungen]** im Dashboard der [!DNL Privacy Service]-Benutzeroberfläche aufgelistet. Der Status für jede Auftragsanfrage wird in der Spalte **[!UICONTROL Status]** angezeigt. Weitere Informationen zum Anzeigen von Auftragsanfragen in der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die API und die Benutzeroberfläche von [!DNL Privacy Service] bieten beide Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Stellen Sie mithilfe der Kennung des Auftrags, dessen Ergebnisse Sie im Anfragepfad herunterladen möchten, eine Anfrage an den Root-Endpunkt (`GET /`) in der [!DNL Privacy Service]-API. Wenn der Auftragsstatus abgeschlossen ist, enthält die API ein `downloadURL`-Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Informationen finden Sie im Abschnitt zu [Nachschlagen eines Auftrags anhand seiner ID](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service]-Entwicklerhandbuch.

### Verwenden der UI

Suchen Sie im Dashboard der Benutzeroberfläche [!DNL Privacy Service] den Auftrag, den Sie herunterladen möchten, über das Widget **Auftragsanforderungen** . Wählen Sie die ID des Auftrags aus, um die Seite Auftragsdetails zu öffnen. Wählen Sie von hier aus **Download** in der oberen rechten Ecke aus, um die ZIP-Datei herunterzuladen. Detailliertere Schritte finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Allgemeine Fehlermeldungen

In der folgenden Tabelle sind einige häufige Fehler in [!DNL Privacy Service] mit Beschreibungen aufgeführt, die bei der Lösung der jeweiligen Probleme helfen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anfrage angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namespace- und ID-Werte in der Anfrage-Payload verwenden. Eine genauere Erläuterung finden Sie im Dokument [Bereitstellen von Identitätsdaten](./identity-data.md) . |
| Ungültiger Namespace | Ein bereitgestellter Identitäts-Namespace für eine Benutzer-ID war ungültig. Eine Liste der zulässigen Namespaces finden Sie im Abschnitt zu [Standard-Identitäts-Namespaces](./api/appendix.md#standard-namespaces) im Entwicklerhandbuch zu [!DNL Privacy Service] . Wenn Sie einen benutzerdefinierten Namespace verwenden, stellen Sie sicher, dass Sie die Eigenschaft `type` der ID auf &quot;custom&quot;setzen. |
| Teilweise abgeschlossen | Der Auftrag wurde erfolgreich abgeschlossen, einige Daten waren jedoch für die jeweilige Anfrage nicht anwendbar und wurden übersprungen. |
| Die Daten weisen nicht das erforderliche Format auf. | Einer oder mehrere Datenwerte für die angegebene Anwendung wurden falsch formatiert. Weitere Informationen finden Sie in den Auftragsdetails . |
| Die IMS-Organisation wurde nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihre IMS-Organisation nicht für [!DNL Privacy Service] bereitgestellt wurde. Wenden Sie sich für weitere Informationen an Ihren Administrator. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um [!DNL Privacy Service] verwenden zu können. Wenden Sie sich an Ihren Administrator, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugangsdaten trat ein Problem auf. | Wenn dieser Fehler auftritt, laden Sie die Zugriffsdaten erneut hoch und versuchen Sie es erneut. |
| Die Arbeitslast für das aktuelle Limit der Dokumentrate wurde überschritten. | Wenn dieser Fehler auftritt, reduzieren Sie die Senderate und versuchen Sie es erneut. |
