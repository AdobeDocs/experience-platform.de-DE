---
keywords: Experience Platform;Profil;Echtzeit-Kundenbericht;Fehlerbehebung;API;Berichte;Datenüberschneidungsbericht;Profil-Daten
title: Bericht "Datenüberschneidung erstellen"
type: Tutorial
description: In diesem Lernprogramm werden die Schritte erläutert, die zum Generieren des Berichts zur Datenüberschneidung mithilfe der Echtzeit-Profil-API für Kunden erforderlich sind.
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# Bericht zur Datenüberschneidung erstellen

Der Bericht zur Datenüberschneidung bietet einen Einblick in die Zusammensetzung des [!DNL Profile]-Speichers Ihres Unternehmens, indem er die Datensätze offen legt, die am meisten zu Ihrer adressierbaren Audience (Profilen) beitragen.

Dieser Bericht bietet Ihnen nicht nur Einblicke in Ihre Daten, sondern kann Ihnen auch bei der Optimierung Ihrer Lizenznutzung helfen, z. B. bei der Festlegung einer Beschränkung der Lebensdauer bestimmter Daten.

In diesem Lernprogramm werden die Schritte erläutert, die zum Generieren des Berichts zur Datenüberschneidung mithilfe der API [!DNL Real-time Customer Profile] und zur Interpretation der Ergebnisse für Ihr Unternehmen erforderlich sind.

## Erste Schritte

Um Adobe Experience Platform-APIs verwenden zu können, müssen Sie zunächst das [Authentifizierungstutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen, um die Werte zu erfassen, die Sie für die erforderlichen Kopfzeilen benötigen. Weitere Informationen zu Experience Platformen-APIs finden Sie in der [Dokumentation zu den ersten Schritten mit Plattform-APIs](../../landing/api-guide.md).

Die erforderlichen Kopfzeilen für alle API-Aufrufe in diesem Lernprogramm sind:

* `Authorization: Bearer {ACCESS_TOKEN}`: Für die  `Authorization` Kopfzeile ist ein Zugriffstoken erforderlich, dem das Wort vorangestellt wird  `Bearer`. Ein neuer Zugriffstoken-Wert muss alle 24 Stunden generiert werden.
* `x-api-key: {API_KEY}`: Der Wert  `API Key` wird auch als ein Wert bezeichnet  `Client ID` und ist ein Wert, der nur einmal generiert werden muss.
* `x-gw-ims-org-id: {IMS_ORG}`: Die  `IMS Org` wird auch als eine bezeichnet  `Organization ID` und muss nur einmal generiert werden.

Nachdem Sie das Authentifizierungstraining abgeschlossen und die Werte für die erforderlichen Kopfzeilen gesammelt haben, können Sie mit dem Aufrufen der Echtzeit-Kunden-API beginnen.

## Generieren von Datenüberschneidungsberichten über die Befehlszeile

Wenn Sie mit der Verwendung der Befehlszeile vertraut sind, können Sie die folgende cURL-Anforderung verwenden, um den Bericht &quot;Datenüberschneidung&quot;zu generieren, indem Sie eine GET für `/previewsamplestatus/report/dataset/overlap` durchführen.

**Anfrage**

Die folgende Anforderung verwendet den Parameter `date`, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler &quot;HTTP-Status 404 (nicht gefunden)&quot;zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Antwort**

Bei einer erfolgreichen Anforderung werden HTTP-Status 200 (OK) und der Bericht zur Datenüberschneidung zurückgegeben. Der Bericht enthält ein `data`-Objekt, das kommagetrennte Listen von Datensätzen und deren jeweilige Profil-Anzahl enthält. Weitere Informationen zum Lesen des Berichts finden Sie im Abschnitt [Interpretieren der Berichtsdaten zur Datenüberschneidung](#interpret-the-report) weiter unten in diesem Lernprogramm.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Erstellen Sie einen Bericht zur Datenüberschneidung mit Postman.

Postman ist eine kooperative Plattform für die API-Entwicklung und nützlich für die Visualisierung von API-Aufrufen. Es kann kostenlos von der [Postman-Website](https://www.postman.com) heruntergeladen werden und bietet eine benutzerfreundliche Benutzeroberfläche für API-Aufrufe. Die folgenden Screenshots verwenden die Postman-Schnittstelle.

**Anfrage**

Gehen Sie wie folgt vor, um den Bericht zur Datenüberschneidung mit Postman anzufordern:

* Wählen Sie mithilfe der Dropdownliste GET als Anforderungstyp aus.
* Geben Sie die erforderlichen Kopfzeilen in die Spalte `KEY` ein:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Geben Sie die Werte, die Sie bei der Authentifizierung generiert haben, in die Spalte `VALUE` ein, wobei die Klammern (`{{ }}`) und alle Inhalte in den Klammern ersetzt werden.
* Geben Sie den Anforderungspfad mit oder ohne den optionalen Parameter `date` ein:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   oder
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler &quot;HTTP-Status 404 (nicht gefunden)&quot;zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. <br/>Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

Nachdem der Anforderungstyp, die Header, Werte und der Pfad abgeschlossen sind, wählen Sie **Senden**, um die API-Anforderung zu senden und den Bericht zu generieren.

![](../images/dataset-overlap-report/postman-request.png)

**Antwort**

Bei einer erfolgreichen Anforderung werden HTTP-Status 200 (OK) und der Bericht zur Datenüberschneidung zurückgegeben. Der Bericht enthält ein `data`-Objekt, das kommagetrennte Listen von Datensätzen und deren jeweilige Profil-Anzahl enthält. Weitere Informationen zum Lesen des Berichts finden Sie im Abschnitt [Interpretieren der Berichtsdaten zur Datenüberschneidung](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpretieren der Berichtsdaten zur Datenüberlappung {#interpret-the-report}

Der Bericht zur Datenüberschneidung bietet einen Zeitstempel, der das Datum und die Uhrzeit des Berichts sowie ein Datenobjekt anzeigt, das eindeutige Kombinationen aus Datensatz-IDs als kommagetrennte Listen enthält. Die folgenden Abschnitte enthalten zusätzliche Informationen zu den Komponenten des Berichts.

### Bericht-Zeitstempel

`reportTimestamp` entspricht dem in der API-Anforderung angegebenen Datum oder, falls kein Datum angegeben wurde, dem Zeitstempel des letzten Berichts.

### Liste der DataSet-IDs

Das `data`-Objekt enthält eindeutige Kombinationen aus DataSet-IDs als kommagetrennte Listen mit der entsprechenden Profil-Anzahl für diese Datasetkombination.

>[!NOTE]
>
>Die Summe aller Profil-Zahlen, die mit jeder Zeile des Datensatzüberschneidungsberichts verknüpft sind, sollte der Gesamtanzahl der Profile in Ihrer Organisation entsprechen.

Um die Ergebnisse des Berichts zu interpretieren, beachten Sie das folgende Beispiel:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dieser Bericht enthält die folgenden Informationen:
* Es gibt 123 Profile aus Daten aus den folgenden Datensätzen: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 454.412 Profile, die aus Daten aus diesen beiden Datensätzen bestehen: `5d92921872831c163452edc8` und `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 107 Profil, die nur aus Daten aus dem Datensatz `5eeda0032af7bb19162172a7` bestehen.
* Die Einrichtung hat insgesamt 454 642 Profile.

## Nächste Schritte

Nach Abschluss dieses Lernprogramms können Sie jetzt den Bericht zur Datenüberschneidung mit der Echtzeit-Kunden-Profil-API generieren. Um mehr über die Arbeit mit Profil-Daten in der API und der Benutzeroberfläche der Experience Platform zu erfahren, lesen Sie zunächst die [Profil-Übersichtsdokumentation](../home.md).