---
keywords: Experience Platform;Startseite; beliebte Themen;Datenvorbereitung;API-Handbuch;Beispieldaten;
solution: Experience Platform
title: API-Endpunkt für Beispieldaten
topic-legacy: sample data
description: 'Sie können den Endpunkt „/samples“ in der Adobe Experience Platform-API verwenden, um Beispieldaten von Zuordnungen programmgesteuert abzurufen, zu erstellen, zu aktualisieren und zu validieren. '
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 100%

---


# Endpunkt für Beispieldaten

Beispieldaten können beim Erstellen eines Schemas für Ihren Zuordnungssatz verwendet werden. Sie können den `/samples`-Endpunkt in der Datenvorbereitungs-API verwenden, um Beispieldaten programmgesteuert abzurufen, zu erstellen und zu aktualisieren.

## Auflisten von Beispieldaten

Sie können eine Liste aller Beispieldaten einer Zuordnung für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/samples`-Endpunkt senden.

**API-Format**

Der `/samples`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Aktuell müssen Sie sowohl den Parameter `start` als auch den Parameter `limit` in Ihre Anfrage einbeziehen.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{LIMIT}` | **Erforderlich**. Gibt die Anzahl der zurückgegebenen Beispieldaten für die Zuordnung an. |
| `{START}` | **Erforderlich**. Gibt den Versatz der Ergebnisseiten an. Um die erste Ergebnisseite zu erhalten, setzen Sie den Wert auf `start=0`. |

**Anfrage**

Mit der folgenden Anfrage werden die letzten beiden Beispieldatenobjekte der Zuordnung in Ihrer IMS-Organisation abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu den letzten beiden Objekten der Beispieldaten für die Zuordnung zurück.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## Erstellen von Beispieldaten

Sie können Beispieldaten erstellen, indem Sie eine POST-Anfrage an den `/samples`-Endpunkt senden.

```http
POST /samples
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihren neu erstellten Beispieldaten zurück.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Erstellen von Beispieldaten durch Hochladen einer Datei

Sie können Beispieldaten mithilfe einer Datei erstellen, indem Sie eine POST-Anfrage an den `/samples/upload`-Endpunkt senden.

**API-Format**

```http
POST /samples/upload
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihren neu erstellten Beispieldaten zurück.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Nachschlagen eines bestimmten Beispieldatenobjekts

Sie können ein bestimmtes Beispieldatenobjekt nachschlagen, indem Sie im Pfad einer GET-Anfrage an den `/samples`-Endpunkt dessen Kennung angeben.

**API-Format**

```http
GET /samples/{SAMPLE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SAMPLE_ID}` | Die Kennung des Beispieldatenobjekts, das Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum Beispieldatenobjekt zurück, das Sie abrufen möchten.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Aktualisieren von Beispieldaten

Sie können ein bestimmtes Beispieldatenobjekt aktualisieren, indem Sie im Pfad einer PUT-Anfrage an den `/samples`-Endpunkt dessen Kennung angeben.

**API-Format**

```http
PUT /samples/{SAMPLE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SAMPLE_ID}` | Die Kennung des Beispieldatenobjekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die angegebenen Beispieldaten. Insbesondere wird der Nachname von „Smith“ in „Lee“ geändert.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu den aktualisierten Beispieldaten zurück.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
