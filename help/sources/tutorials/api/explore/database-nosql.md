---
title: Erkunden einer Datenbank mithilfe der Flow Service-API
description: In diesem Tutorial wird die Flow Service-API verwendet, um den Inhalt und die Dateistruktur einer Drittanbieterdatenbank zu untersuchen.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 46e1a62e558a209ffed4a693cfd71ad5e76d7d98
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 9%

---

# Erkunden einer Datenbank mithilfe der [!DNL Flow Service]-API

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um den Inhalt und die Dateistruktur einer Drittanbieterdatenbank zu untersuchen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Flow Service]-API erfolgreich mit einer Drittanbieterdatenbank verbinden zu können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../landing/api-guide.md).

## Erkunden von Datentabellen

Mithilfe der Verbindungs-ID für Ihre Datenbank können Sie Ihre Datentabellen untersuchen, indem Sie GET-Anfragen ausführen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie überprüfen oder in Experience Platform aufnehmen möchten.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID Ihrer Datenbankquelle. |

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Tabellen aus Ihrer Datenbank zurück. Suchen Sie die Tabelle, die Sie in Experience Platform importieren möchten, und notieren Sie sich die `path` Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um die Struktur zu überprüfen.

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

## Überprüfen der Tabellenstruktur

Um die Tabellenstruktur in Ihrer Datenbank zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Pfad einer Tabelle als Abfrageparameter an.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der angegebenen Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen des `columns`-Arrays.

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
    },
    "data": [],
    "cdcMetadata": {
      "columnDetected": true
    }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihre Datenbank untersucht, den Pfad der Tabelle gefunden, die Sie in Experience Platform aufnehmen möchten, und Informationen über ihre Struktur erhalten. Sie können diese Informationen im nächsten Tutorial verwenden[ um Daten aus Ihrer Datenbank zu erfassen und in Experience Platform zu ](../collect/database-nosql.md).
