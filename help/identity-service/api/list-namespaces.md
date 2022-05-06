---
keywords: Experience Platform; Startseite; beliebte Themen; Namespace-Liste; Listennamespace
solution: Experience Platform
title: Verfügbare Identitäts-Namespaces auflisten
topic-legacy: API guide
description: Liste aller verfügbaren Namespaces.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 44%

---

# Verfügbare Identitäts-Namespaces auflisten

**API-Format**

```http
GET /idnamespace/identities
```

**Anfrage**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein Array von Objekten, wobei jedes Objekt einen verfügbaren Namensraum darstellt. Namespaces mit einem &quot;&quot;[!UICONTROL custom]&quot; value of &quot;[!UICONTROL false]&quot; sind Standard-Namespaces, während diejenigen mit einem &quot;[!UICONTROL custom]&quot; value of &quot;[!UICONTROL true]&quot; sind Namespaces, die Ihre Organisation erstellt hat.

>[!NOTE]
>
>Diese Antwort wurde aus Platzgründen abgeschnitten.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial fort, um einen [benutzerdefinierten Namensraum zu erstellen](./create-custom-namespace.md).
