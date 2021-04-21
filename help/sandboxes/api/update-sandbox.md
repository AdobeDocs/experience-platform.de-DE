---
keywords: Experience Platform;Home;beliebte Themen;Update-Sandbox
solution: Experience Platform
title: Aktualisieren einer Sandbox in der API
topic-legacy: developer guide
description: Sie können ein oder mehrere Felder in einer Sandbox aktualisieren, indem Sie eine PATCH anfordern, die den Namen der Sandbox im Anforderungspfad und die Eigenschaft enthält, die in der Anforderungsnutzlast aktualisiert werden soll.
exl-id: a8ef4305-5e0c-4d8f-8663-1933c957f122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 4%

---

# Aktualisieren einer Sandbox in der API

Sie können ein oder mehrere Felder in einer Sandbox aktualisieren, indem Sie eine PATCH-Anforderung ausführen, die das `name` der Sandbox im Anforderungspfad und die Eigenschaft enthält, die in der Anforderungs-Nutzlast aktualisiert werden soll.

>[!NOTE]
>
>Derzeit kann nur die `title`-Eigenschaft einer Sandbox aktualisiert werden.

**API-Format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name`-Eigenschaft der Sandbox, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung aktualisiert die `title`-Eigenschaft der Sandbox mit dem Namen &quot;dev-2&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit den Details der neu aktualisierten Sandbox zurück.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
