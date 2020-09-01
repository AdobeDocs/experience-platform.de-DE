---
keywords: Experience Platform;home;popular topics;namespace list;list namespace
solution: Experience Platform
title: Verfügbare Namensräume auflisten
topic: API guide
description: Liste aller verfügbaren Namensraum.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 59%

---


# Verfügbare Namensräume auflisten

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein Array von Objekten, wobei jedes Objekt einen verfügbaren Namensraum darstellt. Namespaces with a &quot;[!UICONTROL custom]&quot; value of &quot;[!UICONTROL false]&quot; are standard namespaces, while those with a &quot;[!UICONTROL custom]&quot; value of &quot;[!UICONTROL true]&quot; are namespaces that your organization has created.

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