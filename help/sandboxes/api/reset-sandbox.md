---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zurücksetzen einer Sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---


# Zurücksetzen einer Sandbox

Entwicklungs-Sandboxen verfügen über eine Funktion zum Zurücksetzen der Factory, mit der alle nicht standardmäßigen Ressourcen aus einer Sandbox gelöscht werden. Sie können eine Sandbox zurücksetzen, indem Sie eine PUT-Anforderung erstellen, die die Sandbox `name` im Anforderungspfad enthält.

**API-Format**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SANDBOX_NAME}` | Die `name` Eigenschaft der Sandbox, die Sie zurücksetzen möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine Sandbox mit dem Namen &quot;dev-2&quot;zurückgesetzt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `action` | Dieser Parameter muss in der Anforderungs-Nutzlast mit dem Wert &quot;reset&quot;angegeben werden, damit die Sandbox zurückgesetzt werden kann. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Sandbox zurück und zeigt an, dass sie &quot;zurückgesetzt&quot; `state` ist.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sobald eine Sandbox zurückgesetzt wurde, dauert es etwa 15 Minuten, bis sie vom System bereitgestellt wird. Nach der Bereitstellung `state` wird die Sandbox &quot;aktiv&quot;oder &quot;fehlgeschlagen&quot;.