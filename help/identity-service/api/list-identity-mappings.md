---
keywords: Experience Platform; home; beliebte Themen; identity; Identity
solution: Experience Platform
title: Auflisten von Identitätszuordnungen
description: Eine Zuordnung (ein Mapping) ist eine Sammlung aller Identitäten in einem Cluster für einen bestimmten Namespace.
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 92%

---

# Auflisten von Identitätszuordnungen

Eine Zuordnung (ein Mapping) ist eine Sammlung aller Identitäten in einem Cluster für einen bestimmten Namespace.

## Abrufen einer Identitätszuordnung für eine einzelne Identität

Rufen Sie bei gegebener Identität alle zugehörigen Identitäten aus demselben Namespace ab, der durch die Identität in der Anfrage repräsentiert wird.

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Anfrage**

Option 1: Geben Sie die Identität als Namespace (`nsId`, nach Kennung) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namespace (`ns`, nach Name) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID (`xid`) an. Weiterführende Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem es um das [Abrufen der XID für eine Identität](./list-native-id.md) geht.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Abrufen von Identitätszuordnungen für mehrere Identitäten

Verwenden Sie die `POST`-Methode als Batch-Äquivalent zu der oben beschriebenen `GET`-Methode, um Zuordnungen für mehrere Identitäten abzurufen.

>[!NOTE]
>
>Die Anfrage sollte maximal 1.000 Identitäten angeben. Anfragen mit mehr als 1.000 Identitäten führen zu 400-Status-Codes.

**API-Format**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Anfrageinhalt**

Option 1: Geben Sie eine Liste von XIDs an, für die Zuordnungen abgerufen werden sollen.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2: Geben Sie eine Liste von Identitäten als zusammengesetzte IDs an, wobei jede den ID-Wert und den Namespace nach Namespace-ID benennt. Dieses Beispiel zeigt, wie Sie diese Methode verwenden, während Sie die Standardeinstellung „Privates Diagramm“ von `graph-type` überschreiben.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Anfrage**

**Verwenden von XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Verwenden von UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Wenn mit der bereitgestellten Eingabe keine verwandten Identitäten gefunden wurden, wird ein `HTTP 204`-Antwort-Code ohne Inhalt zurückgegeben.

**Antwort**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: Der Zeitstempel, zu dem die Eingabeidentität zuletzt mit dieser Identität verknüpft wurde.
- `regions`: Stellt die `regionId` und `lastAssociationTime` für den Ort bereit, an dem die Identität angezeigt wurde.

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial zum [Auflisten der verfügbaren Namespaces](./list-namespaces.md) fort.
