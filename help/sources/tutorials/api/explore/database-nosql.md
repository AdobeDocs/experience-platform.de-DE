---
keywords: Experience Platform;Startseite;beliebte Themen;Drittanbieter-Datenbank;Datenbankflussdienst
solution: Experience Platform
title: Datenbank mit der Flussdienst-API durchsuchen
topic-legacy: overview
description: In diesem Lernprogramm wird die Flow Service API verwendet, um Inhalt und Dateistruktur einer Drittanbieter-Datenbank zu untersuchen.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 22%

---

# Datenbank mit der API[!DNL Flow Service]

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um den Inhalt und die Dateistruktur einer Datenbank eines Drittanbieters zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um mit der API [!DNL Flow Service] eine Verbindung zu einer Datenbank eines Drittanbieters herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Für dieses Lernprogramm müssen Sie über eine gültige Verbindung mit der Datenbank eines Drittanbieters verfügen, aus der Sie Daten erfassen möchten. Eine gültige Verbindung besteht aus der Verbindungs-ID und der Verbindungs-ID Ihrer Datenbank. Weitere Informationen zum Erstellen einer Datenbankverbindung und zum Abrufen dieser Werte finden Sie in der [Übersicht über die Quellschnittstellen](./../../../home.md#database).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Wenn Sie das Authentifizierungstreutorial abschließen, erhalten Sie die Werte für die einzelnen erforderlichen Kopfzeilen in allen E[!DNL xperience Platform]-API-Aufrufen, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ihre Datentabellen

Mithilfe der Verbindungs-ID für Ihre Datenbank können Sie Ihre Datentabellen durch Ausführen von GET-Anforderungen untersuchen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie überprüfen oder in [!DNL Platform] aufnehmen möchten.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID der Datenbankquelle. |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Tabellenarray aus Ihrer Datenbank zurück. Suchen Sie die Tabelle, die Sie in [!DNL Platform] einbinden möchten, und beachten Sie die `path`-Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect der Tabellenstruktur

Um die Tabellenstruktur aus der Datenbank zu überprüfen, führen Sie eine GET durch und geben Sie dabei den Tabellenpfad als Abfrage-Parameter an.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID einer Datenbankverbindung. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle. |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich innerhalb der Elemente des `columns`-Arrays.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihre Datenbank erforscht, den Pfad der Tabelle gefunden, die Sie in [!DNL Platform] aufnehmen möchten, und Informationen zu ihrer Struktur erhalten. Sie können diese Informationen im nächsten Lernprogramm zu [verwenden, um Daten aus Ihrer Datenbank zu erfassen und in Platform](../collect/database-nosql.md) zu laden.
