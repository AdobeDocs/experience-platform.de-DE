---
keywords: Experience Platform;Startseite;beliebte Themen;Identitäten;Cluster-Verlauf
solution: Experience Platform
title: Cluster-Verlauf einer Identität abrufen
description: Identitäten können Cluster im Verlauf verschiedener Gerätediagramm-Ausführungen verschieben. Identity Service bietet Einblicke in die Cluster-Verknüpfungen einer bestimmten Identität im Zeitverlauf.
role: Developer
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 35%

---

# Abrufen des Cluster-Verlaufs einer Identität

Identitäten können Cluster im Verlauf verschiedener Gerätediagramm-Ausführungen verschieben. [!DNL Identity Service] bietet Einblick in die Cluster-Verknüpfungen einer bestimmten Identität im Zeitverlauf.

Verwenden Sie den optionalen `graph-type`, um den Ausgabetyp anzugeben, von dem der Cluster abgerufen werden soll. Die Optionen sind:

- `None` - Keine Identitätszuordnung durchführen.
- `Private Graph` - Führen Sie eine Identitätszuordnung anhand Ihres privaten Identitätsdiagramms durch. Wenn kein `graph-type` angegeben wird, ist dies der Standardwert.

## Abrufen des Cluster-Verlaufs einer einzelnen Identität

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namespace (`ns`, nach Name) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID (`xid`) an. Weiterführende Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem es um das [Abrufen der XID für eine Identität](./list-native-id.md) geht.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Abrufen des Cluster-Verlaufs mehrerer Identitäten

Verwenden Sie die `POST`-Methode als Batch-Äquivalent der oben beschriebenen `GET`-Methode, um die Cluster-Verläufe mehrerer Identitäten zurückzugeben.

>[!NOTE]
>
>Die Anfrage sollte höchstens 1.000 Identitäten angeben. Anfragen mit mehr als 1.000 Identitäten führen zu 400-Status-Codes.

**API-Format**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Anfrageinhalt**

Option 1: Geben Sie eine Liste der XIDs an, für die Cluster-Mitglieder abgerufen werden sollen.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Option 2: Geben Sie eine Liste der Identitäten als zusammengesetzte IDs an, wobei jede den ID-Wert und den Namespace nach Namespace-Code benennt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Antwort**

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
>Die Antwort hat immer einen Eintrag für jede XID in der Anfrage, unabhängig davon, ob die XIDs einer Anfrage zum selben Cluster gehören oder ob einem oder mehreren Cluster überhaupt zugeordnet sind.

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial fort, um [Identitätszuordnungen auflisten](./list-identity-mappings.md)
