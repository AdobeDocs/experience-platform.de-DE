---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox löschen
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 4%

---


# Sandbox löschen

Sie können eine Sandbox löschen, indem Sie eine DELETE-Anforderung ausführen, die die Sandbox `name` im Anforderungspfad enthält.

>[!NOTE] Durch diesen API-Aufruf wird die `status` Eigenschaft der Sandbox auf &quot;Gelöscht&quot;aktualisiert und deaktiviert. GET-Anforderungen können weiterhin die Details der Sandbox abrufen, nachdem sie gelöscht wurden.

**API-Format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name` Sandbox, die Sie löschen möchten. |

**Anfrage**

Die folgende Anforderung löscht eine Sandbox mit dem Namen &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die aktualisierten Details der Sandbox zurückgegeben, die zeigen, dass die Sandbox &quot;gelöscht&quot; `state` ist.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
