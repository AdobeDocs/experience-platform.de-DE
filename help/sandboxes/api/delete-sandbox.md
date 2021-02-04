---
keywords: Experience Platform;Startseite;beliebte Themen;Sandbox löschen
solution: Experience Platform
title: Sandbox löschen
topic: developer guide
description: Sie können eine Sandbox löschen, indem Sie eine DELETE-Anforderung ausführen, die den Namen der Sandbox im Anforderungspfad enthält.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 76%

---


# Sandbox löschen

Sie können eine Sandbox löschen, indem Sie eine DELETE-Anfrage ausführen, die den `name` der Sandbox im Anfragepfad enthält.

>[!NOTE]
>
> Durch diesen API-Aufruf wird die `status`-Eigenschaft der Sandbox in „Gelöscht“ geändert und deaktiviert. GET-Anfragen können die Details der Sandbox, nachdem sie gelöscht wurde, weiter abrufen.

**API-Format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Der `name` der Sandbox, die Sie löschen möchten. |

**Anfrage**

Die folgende Anfrage löscht eine Sandbox mit dem Namen „dev-2“.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die aktualisierten Details der Sandbox zurückgegeben; sie zeigen, dass der `state` der Sandbox „gelöscht“ lautet.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
