---
keywords: Experience Platform;Home;beliebte Themen;Update-Sandbox
solution: Experience Platform
title: Sandbox aktualisieren
topic: developer guide
description: Sie können ein oder mehrere Felder in einer Sandbox aktualisieren, indem Sie eine PATCH anfordern, die den Namen der Sandbox im Anforderungspfad und die Eigenschaft enthält, die in der Anforderungsnutzlast aktualisiert werden soll.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 9%

---


# Sandbox aktualisieren

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
