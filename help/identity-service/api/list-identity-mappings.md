---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Listen-Identitätszuordnungen
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Listen-Identitätszuordnungen

Eine Zuordnung ist eine Sammlung aller Identitäten in einem Cluster für einen bestimmten Namensraum.

## Abrufen einer Identitätszuordnung für eine einzelne Identität

Rufen Sie alle verwandten Identitäten aus demselben Namensraum ab, der in der Anforderung durch die Identität dargestellt wird.

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Anfrage**

Option 1: Geben Sie die Identität als Namensraum (`nsId`nach ID) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namensraum (`ns`nach Name) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID an (`xid`). Weitere Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem beschrieben wird, wie Sie die XID für eine Identität [abrufen](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Identitätszuordnungen für mehrere Identitäten abrufen

Verwenden Sie die `POST` Methode als Batch-Entsprechung der oben beschriebenen `GET` Methode, um Zuordnungen für mehrere Identitäten abzurufen.

>[!NOTE]
>
>Die Anforderung sollte höchstens 1000 Identitäten enthalten. Anfragen mit mehr als 1000 Identitäten führen zu 400 Statuscodes.

**API-Format**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Einrichtung anfordern**

Option 1: Geben Sie eine Liste von XIDs an, für die Zuordnungen abgerufen werden sollen.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2: Geben Sie eine Liste von Identitäten als Composite-IDs an, wobei jeder den ID-Wert und den Namensraum nach Namensraum-ID benennt. Dieses Beispiel zeigt, wie Sie diese Methode verwenden, während Sie die Standardeinstellung `graph-type` &quot;Privates Diagramm&quot;überschreiben.

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
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
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

Wenn keine verwandten Identitäten mit der bereitgestellten Eingabe gefunden wurden, wird ein `HTTP 204` Antwortcode ohne Inhalt zurückgegeben.

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

- `lastAssociationTime`: Der Zeitstempel, zu dem die Eingaberidentität zuletzt mit dieser Identität verknüpft wurde.
- `regions`: Stellt das `regionId` und `lastAssociationTime` für den Ort bereit, an dem die Identität angezeigt wurde.

## Nächste Schritte

Fahren Sie mit dem nächsten Lernprogramm zur [Liste der verfügbaren Namensraum](./list-namespaces.md)fort.
