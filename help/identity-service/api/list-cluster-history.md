---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abrufen des Clusterverlaufs einer Identität
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---


# Abrufen des Clusterverlaufs einer Identität

Identitäten können Cluster über den Verlauf verschiedener Gerätediagramme verschieben. [!DNL Identity Service] ermöglicht die Sichtbarkeit der Clusterzuordnungen einer bestimmten Identität im Laufe der Zeit.

Verwenden Sie einen optionalen `graph-type` Parameter, um den Ausgabetyp anzugeben, aus dem der Cluster abgerufen werden soll. Die Optionen sind:

- `None` - Keine Identitätszuordnung durchführen.
- `Private Graph` - Führen Sie Identitätszuordnungen auf Basis Ihres persönlichen Identitätsdiagramms durch. Wenn kein Wert angegeben `graph-type` wird, ist dies der Standardwert.

## Abrufen des Clusterverlaufs einer einzelnen Identität

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Anfrage**

Option 1: Geben Sie die Identität als Namensraum (`nsId`nach ID) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namensraum (`ns`nach Name) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID an (`xid`). Weitere Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem beschrieben wird, wie Sie die XID für eine Identität [abrufen](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Abrufen des Clusterverlaufs von mehreren Identitäten

Verwenden Sie die `POST` Methode als Batch-Entsprechung der oben beschriebenen `GET` Methode, um die Cluster-Historien mehrerer Identitäten zurückzugeben.

>[!NOTE] Die Anforderung sollte höchstens 1000 Identitäten enthalten. Anfragen mit mehr als 1000 Identitäten führen zu 400 Statuscodes.

**API-Format**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Einrichtung anfordern**

Option 1: Geben Sie eine Liste von XIDs an, für die Clustermitglieder abgerufen werden sollen.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2: Geben Sie eine Liste von Identitäten als Composite-IDs an, wobei jeder den ID-Wert und den Namensraum nach Namensraum-Code benennt.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Anfrage**

**Stufenanfrage**

Die Verwendung des `x-uis-cst-ctx: stub` Headers gibt eine gestubelte Antwort zurück. Dies ist eine vorübergehende Lösung, um den Fortschritt bei der frühzeitigen Integration zu erleichtern, während die Dienstleistungen fertig gestellt werden. Dies wird veraltet, wenn es nicht mehr benötigt wird.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Verwenden von XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Verwenden von UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
        "graph-type": "Private Graph"
      }' | json_pp
```

**Reaktion**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE] Die Antwort enthält immer einen Eintrag für jede XID, die in der Anforderung bereitgestellt wird, unabhängig davon, ob die XIDs einer Anforderung demselben Cluster angehören oder ob einem oder mehreren Clustern überhaupt zugeordnet sind.

## Nächste Schritte

Fahren Sie mit der nächsten Übung zu [Liste-Identitätszuordnungen fort](./list-identity-mappings.md)