---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Privacy Service
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Privacy Service sowie Informationen zu häufig aufgetretenen Fehlern in der API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 89%

---

# [!DNL Privacy Service] – Handbuch zur Fehlerbehebung

Adobe Experience Platform [!DNL Privacy Service] stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Unternehmen kundenseitige Datenschutzanfragen verwalten können. Mit [!DNL Privacy Service] können Sie Anfragen für den Zugriff auf und die Löschung von personenbezogenen oder privaten Kundendaten stellen, was die automatische Einhaltung von unternehmensbezogenen und rechtlichen Datenschutzbestimmungen erleichtert.

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu [!DNL Privacy Service] sowie Informationen zu häufig aufgetretenen Fehlern in der API.

## Was ist der Unterschied zwischen Benutzenden und Benutzer-IDs bei Datenschutzanfragen in der API? {#user-ids}

Für einen neuen Datenschutzauftrag in der API muss die JSON-Payload der Anfrage ein `users`-Array enthalten, das spezifische Informationen für jede Benutzerin und jeden Benutzer auflistet, für die die Datenschutzanfrage gilt. Jedes Element im `users`-Array ist ein Objekt, das eine bestimmte Benutzerin bzw. einen bestimmten Benutzer darstellt, jeweils identifiziert durch den zugehörigen `key`-Wert.

Jedes Benutzerobjekt (oder `key`) enthält ein eigenes `userIDs`-Array. Dieses Array listet bestimmte ID-Werte **für eine bestimmte Benutzerin bzw. einen bestimmten Benutzer** auf.

Siehe folgendes Beispiel für ein `users`-Array:

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

Das Array enthält zwei Objekte, die einzelne durch ihre `key`-Werte („DavidSmith“ und „user12345“) identifizierte Benutzende darstellen. „DavidSmith“ hat nur eine aufgelistete ID (die E-Mail-Adresse), während „user12345“ zwei aufweist (die E-Mail-Adresse und ECID).

Weiterführende Informationen zur Bereitstellung von Informationen zu Benutzeridentitäten finden Sie im Handbuch zu [Identitätsdaten für Datenschutzanfragen](identity-data.md).


## Kann ich [!DNL Privacy Service] verwenden, um Daten zu bereinigen, die versehentlich an [!DNL Platform] gesendet wurden?

Adobe unterstützt nicht die Verwendung von [!DNL Privacy Service] zum Löschen von Daten, die versehentlich an ein Produkt gesendet wurden. [!DNL Privacy Service] unterstützt Sie bei der Erfüllung Ihrer Verpflichtungen bezüglich Auskunfts- oder Löschanfragen von betroffenen Personen (oder Verbraucherinnen und Verbrauchern). Jegliche andere Verwendung von Privacy Service für die Datenbereinigung oder -wartung wird nicht unterstützt und ist nicht zulässig.

Diese Anfragen sind zeitkritisch und werden gemäß dem geltenden Datenschutzrecht ausgeführt. Die Übermittlung von Anfragen, bei denen es sich nicht um Anfragen zum Zugriff auf Daten oder zur Löschung von Daten von Betroffenen oder Verbraucherinnen und Verbrauchern handelt, wirkt sich auf alle Kundinnen und Kunden von [!DNL Privacy Service] und auf die Fähigkeit von [!DNL Privacy Service] aus, die entsprechenden rechtlichen Fristen einzuhalten. Es gibt jetzt eine feste tägliche Upload-Grenze, um einen Missbrauch des Dienstes zu verhindern.

Wenden Sie sich an Ihr Adobe-Accountteam, um die Entfernung von personenbezogenen Daten oder die Beseitigung von Datenproblemen koordinieren zu lassen.

## Wie erhalte ich Informationen über den Status meiner Datenschutzanfrage bzw. meines Auftrags?

Sie können Details zu einem bestimmten Auftrag über die [!DNL Privacy Service]-API oder -Benutzeroberfläche abrufen.

### Verwenden der API

Um den Status eines bestimmten Auftrags über die [!DNL Privacy Service]-API abzurufen, stellen Sie eine Anfrage an den Stammendpunkt (`GET /`), wobei die Auftrags-ID im Anfragepfad verwendet wird. Weitere Details finden Sie im Abschnitt zum [Überprüfen des Auftragsstatus](api/privacy-jobs.md#check-the-status-of-a-job) im [!DNL Privacy Service]-API-Handbuch.

### Verwenden der Benutzeroberfläche

Alle aktiven Auftragsanfragen werden im Dashboard der [!DNL Privacy Service]-Benutzeroberfläche im Widget **[!UICONTROL Auftragsanfragen]** aufgelistet. Der Status für jede Auftragsanfrage wird in der Spalte **[!UICONTROL Status]** angezeigt. Weiterführende Informationen zum Anzeigen von Auftragsanfragen in der Benutzeroberfläche finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Wie lade ich die Ergebnisse meiner abgeschlossenen Datenschutzaufträge herunter?

Die [!DNL Privacy Service]-API und -Benutzeroberfläche bieten beide Methoden zum Herunterladen der Ergebnisse abgeschlossener Aufträge im ZIP-Format.

### Verwenden der API

Senden Sie in der [!DNL Privacy Service]-API eine Anfrage an den Stammendpunkt (`GET /`) und verwenden Sie dabei die ID des Auftrags, dessen Ergebnisse Sie im Anfragepfad herunterladen möchten. Bei abgeschlossenem Auftragsstatus umfasst die API ein `downloadURL`-Attribut im Antworttext. Dieses Attribut enthält eine URL, die Sie in die Adressleiste Ihres Browsers einfügen können, um die ZIP-Datei herunterzuladen.

Weitere Details finden Sie im [!DNL Privacy Service]-API-Handbuch im Abschnitt zum [Suchen eines Auftrags anhand der ID](api/privacy-jobs.md#check-the-status-of-a-job).

### Verwenden der Benutzeroberfläche

Suchen Sie im Dashboard der [!DNL Privacy Service]-Benutzeroberfläche den Auftrag, den Sie herunterladen möchten, über das Widget **Auftragsanfragen**. Wählen Sie die ID des Auftrags aus, um die Seite „Auftragsdetails“ zu öffnen. Wählen Sie hier oben rechts die Option **Herunterladen** aus, um die ZIP-Datei herunterzuladen. Ausführliche Anweisungen finden Sie im [Privacy Service-Benutzerhandbuch](ui/user-guide.md).

## Allgemeine Fehlermeldungen {#common-error-messages}

In der folgenden Tabelle sind einige häufige Fehler in [!DNL Privacy Service] mit Beschreibungen aufgeführt, die bei der Lösung der jeweiligen Probleme helfen.

| Fehlermeldung | Beschreibung |
| --- | --- |
| Benutzer-IDs wurden nicht gefunden. | Einige der in der Anfrage angegebenen Benutzer-IDs konnten nicht gefunden werden und wurden übersprungen. Stellen Sie sicher, dass Sie die richtigen Namespace- und ID-Werte in der Anfrage-Payload verwenden. Ausführlichere Erläuterungen finden Sie im Dokument zum [Bereitstellen von Identitätsdaten](./identity-data.md). |
| Ungültiger Namespace. | Ein für eine Benutzer-ID bereitgestellter Identity-Namespace war ungültig. Eine Liste der zulässigen Namespaces finden Sie im Anhang des [!DNL Privacy Service]-API-Handbuchs im Abschnitt zu [Standard-Identity-Namespaces](./api/appendix.md#standard-namespaces). Wenn Sie einen benutzerdefinierten Namespace verwenden, stellen Sie sicher, dass Sie die `type`-Eigenschaft der ID als benutzerdefiniert festlegen. |
| Teilweise abgeschlossen. | Der Auftrag wurde erfolgreich abgeschlossen. Einige Daten waren jedoch für die jeweilige Anfrage nicht anwendbar und wurden übersprungen. |
| Die Daten haben nicht das erforderliche Format. | Einer oder mehrere Datenwerte für die angegebene Anwendung haben nicht das korrekte Format. Weitere Informationen finden Sie in den Auftragsdetails. |
| IMS-Organisation nicht bereitgestellt. | Diese Meldung tritt auf, wenn Ihre Organisation nicht für [!DNL Privacy Service] bereitgestellt wurde. Weiterführende Informationen erhalten Sie von Ihren Admins. |
| Zugriff und Berechtigungen sind erforderlich. | Zugriff und Berechtigungen sind erforderlich, um [!DNL Privacy Service] verwenden zu können. Wenden Sie sich an Ihre Admins, um Zugriff zu erhalten. |
| Beim Hochladen und Archivieren der Zugriffsdaten ist ein Problem aufgetreten. | Laden Sie bei diesem Fehler die Zugriffsdaten erneut hoch und versuchen Sie es erneut. |
| Arbeitslast für aktuelles Limit der Dokumentzahl überschritten. | Reduzieren Sie bei diesem Fehler die Übermittlungsrate und versuchen Sie es erneut. |
| Zu viele Anforderungen<br>(HTTP 429-Fehler) | Wenn Ihre Sendemuster die überwachte Grenze der zulässigen Aufträge für betroffene Personen überschreiten, erhalten Sie als Reaktion auf anhaltenden Traffic von Ihrem Unternehmen einen HTTP-429-Fehler. Privacy Service ist für die Verarbeitung von Datenschutzanfragen der betroffenen Person vorgesehen. Sie darf nicht für die Datenbereinigung verwendet werden. Wenn Sie HTTP 429-Fehler erhalten, werden Einschränkungen für Einschränkungen und Anfragen implementiert, um Adobe vor Missbrauch zu schützen, der die ordnungsgemäße Einhaltung gefährden könnte.<br>Alternative Methoden zur Minimierung Ihrer Daten finden Sie unter [Festlegen von Ablaufplänen für Datensätze](../hygiene/ui/dataset-expiration.md) und unter Verwendung der [Funktion zum Löschen von Datensätzen](../hygiene/ui/record-delete.md). Weitere Informationen zur Anwendung dieser Funktionen finden Sie in der entsprechenden Dokumentation . |
