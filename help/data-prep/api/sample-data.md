---
keywords: Experience Platform;Startseite;beliebte Themen;Datenvorgabe;API-Leitfaden;Musterdaten
solution: Experience Platform
title: Beispiel-Daten-API-Endpunkt
topic: Musterdaten
description: 'Sie können den Endpunkt "/samples"in der Adobe Experience Platform API verwenden, um Musterdaten programmgesteuert abzurufen, zu erstellen, zu aktualisieren und zu validieren. '
translation-type: tm+mt
source-git-commit: a2c966ae2401faa572cbba974ce6f572d5280a8f
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 8%

---


# Beispiel-Daten-Endpunkt

Musterdaten können beim Erstellen eines Schemas für Ihren Zuordnungssatz verwendet werden. Sie können den Endpunkt `/samples` in der Datenvorgabe-API verwenden, um Beispieldaten programmgesteuert abzurufen, zu erstellen und zu aktualisieren.

## Musterdaten für Listen

Sie können eine Liste aller Musterdaten für Ihre IMS-Organisation abrufen, indem Sie eine GET an den `/samples`-Endpunkt anfordern.

**API-Format**

Der `/samples`-Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Derzeit müssen Sie sowohl die Parameter `start` als auch `limit` als Teil Ihrer Anforderung einbeziehen.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{LIMIT}` | **Erforderlich**. Gibt die Anzahl der zurückgegebenen Musterdaten für die Zuordnung an. |
| `{START}` | **Erforderlich**. Gibt den Versatz der Ergebnisseiten an. Um die erste Ergebnisseite abzurufen, legen Sie den Wert auf `start=0` fest. |

**Anfrage**

Mit der folgenden Anforderung werden die letzten beiden Zuordnungsmuster-Daten in Ihrer IMS-Organisation abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Informationen zu den letzten beiden Objekten der Zuordnung von Musterdaten zurück.

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

## Musterdaten erstellen

Sie können Musterdaten erstellen, indem Sie eine POST an den `/samples`-Endpunkt anfordern.

```http
POST /samples
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Informationen zu Ihren neu erstellten Musterdaten zurück.

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

## Musterdaten durch Hochladen einer Datei erstellen

Sie können Musterdaten mithilfe einer POST erstellen, indem Sie eine Anforderung an den Endpunkt `/samples/upload` stellen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Informationen zu Ihren neu erstellten Musterdaten zurück.

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

## Nachschlagen eines bestimmten Musterdatenobjekts

Sie können ein bestimmtes Objekt mit Musterdaten suchen, indem Sie dessen ID im Pfad einer GET zum `/samples`-Endpunkt angeben.

**API-Format**

```http
GET /samples/{SAMPLE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SAMPLE_ID}` | Die ID des Musterdatenobjekts, das Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Informationen über das Musterdatenobjekt zurück, das Sie abrufen möchten.

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

## Musterdaten aktualisieren

Sie können ein bestimmtes Musterdatenobjekt aktualisieren, indem Sie dessen ID im Pfad einer PUT-Anforderung zum `/samples`-Endpunkt angeben.

**API-Format**

```http
PUT /samples/{SAMPLE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SAMPLE_ID}` | Die ID des Musterdatenobjekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung aktualisiert die angegebenen Musterdaten. Insbesondere wird der Nachname von &quot;Smith&quot;in &quot;Lee&quot;aktualisiert.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Informationen zu den aktualisierten Musterdaten zurück.

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
