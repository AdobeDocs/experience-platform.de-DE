---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verfügbare Namensraum zur Liste
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 5%

---


# Verfügbare Namensraum zur Liste

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

Die Antwort enthält ein Array von Objekten, wobei jedes Objekt einen verfügbaren Namensraum darstellt. Namensraum mit dem Wert &quot;[!UICONTROL custom]&quot;[!UICONTROL false]sind Standard-Namensraum, während solche mit dem Wert &quot;[!UICONTROL custom]&quot;von &quot;[!UICONTROL true]&quot;Namensraum sind, die von Ihrem Unternehmen erstellt wurden.

>[!NOTE]
>
>Diese Antwort wurde für den Weltraum abgeschnitten.

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

Fahren Sie mit der nächsten Übung fort, um einen benutzerdefinierten Namensraum zu [erstellen](./create-custom-namespace.md)