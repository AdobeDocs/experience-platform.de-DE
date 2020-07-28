---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abrufen des Clusterverlaufs einer Identität
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 53%

---


# Abrufen des Clusterverlaufs einer Identität

Identitäten können Cluster über den Verlauf verschiedener Gerätediagramme verschieben. [!DNL Identity Service] ermöglicht die Sichtbarkeit der Clusterzuordnungen einer bestimmten Identität im Laufe der Zeit.

Verwenden Sie einen optionalen `graph-type` Parameter, um den Ausgabetyp anzugeben, aus dem der Cluster abgerufen werden soll. Die Optionen sind:

- `None` - Keine Identitätszuordnung durchführen.
- `Private Graph` - Führen Sie Identitätszuordnungen auf Basis Ihres persönlichen Identitätsdiagramms durch. Wenn kein `graph-type` angegeben wird, ist dies der Standardwert.

## Abrufen des Clusterverlaufs einer einzelnen Identität

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Anfrage**

Option 1: Geben Sie die Identität als Namespace (`nsId`, nach Kennung) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namespace (`ns`, nach Name) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID (`xid`) an. Weiterführende Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem es um das [Abrufen der XID für eine Identität](./list-native-id.md) geht.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Abrufen des Clusterverlaufs von mehreren Identitäten

Use the `POST` method as a batch equivalent of the `GET` method described above to return the cluster histories of multiple identities.

>[!NOTE]
>
> Die Anfrage darf höchstens 1.000 Identitäten zurückgeben. Anfragen mit mehr als 1.000 Identitäten führen zu 400-Status-Codes.

**API-Format**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Anfrageinhalt**

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

**Stub-Anfrage**

Durch Verwendung der Kopfzeile `x-uis-cst-ctx: stub` wird eine Stub-Antwort zurückgegeben. Dies ist eine vorübergehende Lösung, um den Fortschritt bei der frühzeitigen Integration zu unterstützen, während Dienste fertig gestellt werden. Diese Lösung wird veralten, sobald sie nicht mehr benötigt wird.

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

>[!NOTE]
>
>Die Antwort enthält stets einen Eintrag für jede XID, die in der Anfrage angegeben ist, unabhängig davon, ob die XIDs einer Anfrage demselben Cluster angehören oder ob eine bzw. mehrere von ihnen überhaupt einem Cluster zugeordnet sind.

## Nächste Schritte

Proceed to the next tutorial to [list identity mappings](./list-identity-mappings.md)