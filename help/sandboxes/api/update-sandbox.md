---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox aktualisieren
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 13%

---


# Sandbox aktualisieren

Sie können ein oder mehrere Felder in einer Sandbox aktualisieren, indem Sie eine PATCH anfordern, die die Sandbox `name` im Anforderungspfad und die Eigenschaft enthält, die in der Anforderungsnutzlast aktualisiert werden soll.

>[!NOTE]
>
>Derzeit kann nur die `title` Eigenschaft einer Sandbox aktualisiert werden.

**API-Format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` property of the sandbox you want to update. |

**Anfrage**

Die folgende Anforderung aktualisiert die `title` Eigenschaft der Sandbox &quot;dev-2&quot;.

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
