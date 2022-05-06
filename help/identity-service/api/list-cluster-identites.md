---
keywords: Experience Platform; Startseite; beliebte Themen; Listen-Identitäten; Listencluster
solution: Experience Platform
title: Alle Identitäten in einem Cluster auflisten
topic-legacy: API guide
description: Identitäten, die in einem Identitätsdiagramm miteinander verwandt sind, werden unabhängig vom Namespace als Teil desselben „Clusters“ in dem Identitätsdiagramm betrachtet. Folgende Optionen bieten die Möglichkeit, auf alle Cluster-Mitglieder zuzugreifen.
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 95%

---

# Alle Identitäten in einem Cluster auflisten

Identitäten, die in einem Identitätsdiagramm miteinander verwandt sind, werden unabhängig vom Namespace als Teil desselben „Clusters“ in dem Identitätsdiagramm betrachtet. Folgende Optionen bieten die Möglichkeit, auf alle Cluster-Mitglieder zuzugreifen.

## Verknüpfte Identitäten für eine bestimmte Identität abrufen

Rufen Sie alle Cluster-Mitglieder für eine bestimmte Identität ab.

Sie können den optionalen `graph-type`-Parameter verwenden, um das Identitätsdiagramm anzugeben, aus dem der Cluster abgerufen werden soll. Die Optionen sind:

- Keine – Keine Identitätszusammenfügung durchführen.
- Privates Diagramm – Eine Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen. Wenn kein `graph-type` angegeben wird, ist dies der Standardwert.

**API-Format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Anfrage**

Option 1: Geben Sie die Identität als Namespace (`nsId`, nach Kennung) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 2: Geben Sie die Identität als Namespace (`ns`, nach Name) und Kennungswert (`id`) an.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Option 3: Geben Sie die Identität als XID (`xid`) an. Weiterführende Informationen zum Abrufen der XID einer Identität finden Sie im Abschnitt dieses Dokuments, in dem es um das [Abrufen der XID für eine Identität](./list-native-id.md) geht.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Verknüpfte Identitäten für mehrere Identitäten abrufen

Verwenden Sie `POST` als Batch-Entsprechung der oben beschriebenen `GET`-Methode, um die Identitäten in Clustern mit mehreren Identitäten zurückzugeben.

>[!NOTE]
>
> Die Anfrage darf höchstens 1.000 Identitäten zurückgeben. Anfragen mit mehr als 1.000 Identitäten führen zu 400-Status-Codes.

**API-Format**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Anfrage**

Die folgende Anfrage veranschaulicht die Bereitstellung einer Liste von XIDs, für die Cluster-Mitglieder abgerufen werden.

**Stub-Anfrage**

Durch Verwendung der Kopfzeile `x-uis-cst-ctx: stub` wird eine Stub-Antwort zurückgegeben. Dies ist eine vorübergehende Lösung, um den Fortschritt bei der frühzeitigen Integration zu unterstützen, während Dienste fertig gestellt werden. Diese Lösung wird veralten, sobald sie nicht mehr benötigt wird.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**„Stub“-Antwort**

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

>[!NOTE]
>
>Die Antwort enthält stets einen Eintrag für jede XID, die in der Anfrage angegeben ist, unabhängig davon, ob die XIDs einer Anfrage demselben Cluster angehören oder ob eine bzw. mehrere von ihnen überhaupt einem Cluster zugeordnet sind.

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial fort, um den [Cluster-Verlauf einer Identität aufzulisten](./list-cluster-history.md).
