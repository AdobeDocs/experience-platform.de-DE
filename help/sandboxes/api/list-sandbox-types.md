---
keywords: Experience Platform;Home;beliebte Themen;Liste-Sandboxen
solution: Experience Platform
title: Von Liste unterstützte Sandbox-Typen in der API
topic-legacy: developer guide
description: Sie können eine Liste der unterstützten Sandbox-Typen für Ihr Unternehmen abrufen, indem Sie eine GET an den Endpunkt /sandboxTypes anfordern.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 48%

---

# Von der Liste unterstützte Sandbox-Typen in der API

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
