---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Liste-Cluster-Identitäten
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---


# Liste aller Identitäten in einem Cluster

Identitäten, die in einem Identitätsdiagramm verwandt sind, werden unabhängig vom Namensraum als Teil desselben &quot;Clusters&quot;in diesem Identitätsdiagramm betrachtet. Die folgenden Optionen bieten die Möglichkeit, auf alle Clustermitglieder zuzugreifen.

## Verknüpfte Identitäten für eine einzelne Identität abrufen

Rufen Sie alle Clustermitglieder für eine einzelne Identität ab.

Sie können den optionalen `graph-type` Parameter verwenden, um das Identitätsdiagramm anzugeben, aus dem der Cluster abgerufen werden soll. Die Optionen sind:

- Keine - Keine Identitätszuordnung durchführen.
- Privates Diagramm - Führen Sie Identitätszuordnungen basierend auf Ihrem privaten Identitätsdiagramm durch. Wenn kein Wert angegeben `graph-type` wird, ist dies der Standardwert.

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Anfrage**

Option 1: Geben Sie die Identität als Namensraum (`nsId`nach ID) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namensraum (`ns`nach Name) und ID-Wert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID an (`xid`). Weitere Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem beschrieben wird, wie Sie die XID für eine Identität [abrufen](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Verknüpfte Identitäten für mehrere Identitäten abrufen

Verwenden Sie `POST` als Batch-Entsprechung der oben beschriebenen `GET` Methode, um die Identitäten in den Clustern mehrerer Identitäten zurückzugeben.

>[!NOTE] Die Anforderung sollte höchstens 1000 Identitäten enthalten. Anfragen mit mehr als 1000 Identitäten führen zu 400 Statuscodes.

**API-Format**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Anfrage**

Die folgende Anforderung veranschaulicht die Bereitstellung einer Liste von XIDs, für die Clustermitglieder abgerufen werden sollen.

**Stufenanfrage**

Die Verwendung des `x-uis-cst-ctx: stub` Headers gibt eine gestubelte Antwort zurück. Dies ist eine vorübergehende Lösung, um den Fortschritt bei der frühzeitigen Integration zu erleichtern, während die Dienstleistungen fertig gestellt werden. Dies wird veraltet, wenn es nicht mehr benötigt wird.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Aufruf mit XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Aufruf mit UIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Antwort**

**&#39;Stubbed&#39;-Antwort**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Vollständige Antwort**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE] Die Antwort enthält immer einen Eintrag für jede XID, die in der Anforderung bereitgestellt wird, unabhängig davon, ob die XIDs einer Anforderung demselben Cluster angehören oder ob einem oder mehreren Clustern überhaupt zugeordnet sind.

## Nächste Schritte

Fahren Sie mit dem nächsten Lernprogramm fort, um den Cluster-Verlauf einer Identität zu [Liste.](./list-cluster-history.md)