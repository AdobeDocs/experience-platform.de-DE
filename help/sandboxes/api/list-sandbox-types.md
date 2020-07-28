---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Auflisten unterstützter Sandbox-Typen
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 100%

---


# Auflisten unterstützter Sandbox-Typen

Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/sandboxTypes` senden.

**API-Format**

```http
GET /sandboxTypes
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Sandbox-Typen zurück, die für Ihr Unternehmen unterstützt werden.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
